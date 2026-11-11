# 开发策略讨论稿：以 BioSample 为锚点的证据化元数据恢复

**版本：** 2026-11-10（讨论稿）  
**状态：** 策略阶段；未检索任何测试样本，未编写或运行采集程序。

## 1. 目标定义

给定一个或多个测序 accession，解析其公共数据库对象关系，并尽可能从归档、关联论文、补充表和适用的人工整理资源中找回样本及宿主上下文。每个字段必须能回到具体来源和证据位置；“未检索到”不得等同于“作者未报告”，研究级描述也不能未经证据就赋给每个样本。

**核心边界（用户已明确）：输入端经常只有一个或多个测序样本/Run ID；受试者、宿主、采样事件和表型没有现成的完整 crosswalk。发现论文、找到补充文件、识别作者使用的样本别名，并判断这些别名能否连回归档 accession，都是工具要完成的主要工作。** 这里不能把现有 BioSample 字段当成已知宿主画像，也不能假设 accession → paper → sample row 的连接天然存在。

建议把“所有信息”定义为：**在允许访问的公开来源中可检索到、且能够对样本归属提供可审计证据的信息**。不同研究会有不同缺失，工具应输出覆盖情况和未解决状态，而非承诺每个样本都有年龄、饮食等信息。

## 2. 确认的数据模型

用户已确认样本主表以 BioSample/生物学样本为主，Experiment 和 Run 分开保存。建议落成以下关系：

```text
Input ID → BioSample/archive Sample → Experiment → Run → file(s)
                  │                    │
                  ├── biological specimen / sampling event
                  ├── subject / visit / timepoint (only when evidenced)
                  └── BioProject/Study ↔ publication(s) ↔ supplement(s)
```

- `biosample`：以 NCBI BioSample 或 ENA Sample accession 为归档记录键；保留 primary、secondary accession、alias、title 与原始属性。若 BioSample 的生物学单位明显是 pool、composite 或范围性样本，额外标注单位类型，不强行当作一个个体/一次采样。
- `biological_sample` / `sampling_event`：可选的解释层。一个生物学样本可能有多个归档别名；一个受试者也可能有多次采样。它与 BioSample 的合并必须有明确 crosswalk 证据，不能仅因名称相似而合并。
- `experiment` 与 `run`：各自一行；同一个 BioSample 可以关联多个 Experiment/Run。技术属性保持在相应层级，避免误把某个 Run 的 library 信息写成整个生物样本属性。
- `study` 与 `publication`：保留 project–paper 关联类型，如 `generated_own_data`、`reused_data`、`declared_by_archive`、`accession_mentioned`。复用既有数据的文章不自动视为原始样本描述来源。
- `subject/visit/group`：作为可选实体，不从样本名或 accession 排序直接推断。一个 subject 下的多次采样、一个 BioSample 下的多个 Runs，应分别表达。

BioSample 是稳定且实用的归档锚点，但不保证总能与“一名受试者的一份独立生物材料”一一对应。应同时保存归档样本和生物学样本解释，避免为满足一行一人而丢失 pool、混样或多次测序情况。

## 3. 建议的检索分层

### A. Accessions 与归档信息

1. 先识别输入类型（BioSample、Experiment、Run、BioProject、ENA accession 或 DOI/PMID）。
2. 通过 NCBI SRA/BioSample、E-utilities 和 ENA API 做精确 accession 解析；获取完整 accession crosswalk 和对象关系。
3. 查询 BioSample 的全部属性，以及 Experiment/Run 的 library、assay、instrument、layout、read/base counts 和文件描述。保留原始响应、请求时间、状态码和来源 URL；ENA、SRA 字段冲突时并列记录。
4. 默认获取文件 URL、大小、checksum 等描述 metadata，不拉取 FASTQ；若文件链接会过期或源站策略不同，记录检索日期和状态。

### B. 论文与补充材料发现

按证据强度递进地寻找关联论文：归档中的 declared publication、BioProject/DOI/PMID 交叉引用、Europe PMC 的 accession text-mining/cross-reference，再用 accession、study title、作者和 cohort 名称补充检索。论文链接需保存链接方法与关系类型；仅提及 accession 的论文不能直接当作原始研究。

实际需要的链路是 `输入 ID → archive sample/run → study/project → 原始数据论文 → supplement/作者表 → 作者样本别名/subject ID → 可验证的 sample-level 或 cohort-level claim`。其中每个箭头都要有匹配证据和关系类别；若文章只在正文提到某 BioProject，且没有样本级表格/交叉引用，所得宿主信息通常只能标为 study/cohort scope。

对可访问全文和补充材料：先列出可用文件，再确定哪些文件含样本 crosswalk 或宿主字段。表格解析优先使用 CSV/TSV/XLSX 中明确的 accession/alias 列；PDF/扫描表格或非结构化文本需保存页码、表号、行列定位，并列为更需要复核的抽取路径。严格校验表格标识符和归档 accession/alias 的连接，未匹配行留在 unmatched 队列。

NCBI PMC BioC Supplementary Materials API 可按 PMID/PMCID 列出并检索 PMC Open Access 子集中的可文本化补充材料；Europe PMC 可提供文献记录、全文可用链接、ENA 等数据库交叉引用和文本挖掘的 accession。PMC Article Dataset 在 2026-08 完成迁移到公开 AWS `pmc-oa-opendata`；旧 FTP/Cloud 文件已移除，因此开发时应按现行接口和文件清单实现，不依赖旧路径。许可范围和是否能自动下载应按来源逐一确认。

### C. 宿主/采样属性恢复

建议先定义 field dictionary，再检索/归一化。初始字段候选：

| 字段组 | 字段举例 | 关键限制 |
|---|---|---|
| 个体人口学 | 年龄、年龄单位/采集时年龄、性别、生命阶段、人口/地理信息 | 年龄和性别可能是个体级或 cohort 级；地理位置粒度需保留原始表述 |
| 健康与暴露 | 疾病/健康状态、BMI、药物、抗生素、吸烟、妊娠、既往史 | 必须区分诊断、作者定义的组别和数据库标签；健康对照也需正面证据 |
| 生活方式/饮食 | 饮食模式、特定食物/补充剂、运动、吸烟/饮酒、居住/职业 | “研究讨论了饮食”不等于个体饮食值；抽象描述不可自动赋给每位受试者 |
| 采样与实验设计 | body site/material、采样日期/方式、visit/timepoint、treatment arm、subject pairing | 精确到样本的跨表连接是关键；研究层信息要标记为 study-wide |
| 测序技术 | assay、library strategy/source/selection、instrument、layout、read count、file info | Experiment/Run 层；不作为宿主属性 |

MIxS/MIMARKS 可作为采样与测序上下文字段的标准参照；对疾病、饮食和生活方式等宿主变量，再按字段需要采用适当受控词表或保留文本标签。每一字段都保留 `raw_value` 与 `normalized_value`；无法可靠映射时只保留原值并标注 `normalization_unresolved`。

### D. 从“只有 ID”开始的映射等级

| 等级 | 实际找到的链接 | 可以输出的粒度 |
|---|---|---|
| A | 输入 ID 精确解析到 Run/Experiment/BioSample，archive 关系完整 | archive 和技术属性；只输出 archive 里直接给出的样本属性 |
| B | BioProject 关联到描述原始数据的论文，论文/补充表以精确 accession 标记样本行 | 样本级宿主/采样/组别字段，可附表格行证据 |
| C | 论文使用自定义 sample alias，另有明确的 accession↔alias crosswalk | 在 crosswalk 证据完整时可恢复样本级字段；否则保持 candidate |
| D | 找到 subject/participant ID 与样本的对应，且论文表列出 subject 属性 | 允许经已验证的 sample→subject→属性链输出，并标明 subject-level 来源 |
| E | 只找到 cohort-level 论文描述，缺少个体样本连接 | 输出 study/cohort-level evidence；不复制为个体样本值，除非内容明确适用于全部纳入样本且适用范围可核验 |
| F | accession 有效，但原始论文/补充表无公开或无法映射的宿主信息 | 记录已查来源、无对应证据/未公开/不可访问状态，不制造个体信息 |

这个等级表达可验证的对象链接，不等同于一般 confidence 分数。缺少样本 crosswalk 时，文章仍可能提供重要的研究背景，但不能据此断言某个 accession 对应某个患者、组别或 timepoint。

## 4. 字段级证据账本与保守决策

不建议设计一个对所有字段都有效的简单来源优先级。每一条发现都先保存为 `claim`：

`entity_id · field · raw_value · normalized_value · scope · source · locator · quote · join_method · route · confidence_tier · status · retrieved_at`

- `scope` 至少区分 sample、subject、visit、experiment、run、study/cohort。
- `source/locator` 记录数据库 URL/accession，或论文 DOI/PMID、章节/页码、表格名、文件名、sheet/row/column。
- `join_method` 记录 exact accession、secondary accession、author alias、subject crosswalk 或人工确认；模糊匹配只生成 candidate。
- 多个来源冲突时保留全部 claims 和冲突类型；对有实质冲突的字段可暂不写入最终规范值，等待复核。
- 将“作者未报告”“在已访问来源中未找到”“来源不可访问”“查询失败”“映射不确定”“不适用”作为不同状态。
- 模型/NLP 只用于候选发现、文段定位或值规范化；最终写入需要证据原文、定位和范围校验。Confidence 是路线/规则的等级，不能默认解释成概率；应按字段在验证集上的精确率来定发布门槛。

Microbiome Repo 的最新做法可作设计参照：区分归档属性、补充表、全文和摘要路线；表格仅在样本标识符能连接时采用，研究级陈述另外标 scope，并把冲突值记录下来。不过它标注的 confidence 明确是离散等级而非校准概率，且覆盖率仍不完整，不能把其路线分值直接照搬成新工具的正确率。

## 5. 建议的交付表

1. `input_manifest`：原始输入、类型、批次、检索状态。
2. `biosample_master`：一行一个 BioSample/ENA Sample 记录，保存原始 archive attributes 和标准化结果。
3. `biological_sample_crosswalk`：归档 sample ↔ 生物学材料/采样事件/subject/visit 的证据关系。
4. `experiments`、`runs`、`files`：技术对象分表及 run–sample–experiment 关系。
5. `studies_publications`：BioProject/Study 与论文的关联、链接依据、own-data/reuse 类型。
6. `sample_metadata_claims`：长表形式的字段级 evidence ledger；每条记录可回到来源。
7. `conflicts_unmatched`：互相矛盾的 claim、supplement 未匹配行、候选 alias 和待人工审核项。
8. `sample_master_wide`：便于分析的汇总视图；每个标准化字段仍附 route/source/status，不替代 claim 长表。
9. `retrieval_manifest_qc`：来源版本、时间、文件 hash、请求记录、missingness、匹配率、抽取复核统计。

## 6. 来源与资源的角色

| 来源/资源 | 建议角色 | 适用限制 |
|---|---|---|
| NCBI SRA/BioSample、ENA | ID 关系和测序技术信息的主来源 | submitter metadata 不齐、同义字段和自由文本仍需规范化 |
| 研究论文及其补充表/作者公开表 | 恢复 host、cohort、分组、样本别名、时间点和饮食等信息的关键原始证据 | 论文可能只给 cohort-level 信息；supplement 未必有 sample crosswalk；许可/可访问性不同 |
| curatedMetagenomicData 3 | 人类 shotgun 的高质量二级对照；22,710 个样本、94 cohorts，扩展人工整理 100+ 个受试者特征 | 覆盖面有限于其纳入研究，不能视为任何输入 ID 都有记录 |
| GMrepo v3、PRIME、GutBiomeDB | 人类肠道 16S/shotgun 的病种/表型/群体层二级核验资源 | 领域/测序类型受限；PRIME 以 Run 为样本单位，不能直接替代 BioSample 主表 |
| Microbiome Repo (2026-11 新发布) | 最贴近“跨 archive、supplement、paper 自动恢复”问题的实践参考，也可作为有来源的二级数据 | 当前是新兴项目资源；范围主要 human-associated shotgun DNA/RNA；公开说明的覆盖率字段间差异大，置信等级非校准概率 |
| MetaHQ (2026 预印本/社区注释库) | 了解如何查询与整合来自多个已有整理库的注释 | 不是单一原始证据；其数据库有 CC BY-NC 4.0 限制，纳入新项目/分发前需核对来源许可证 |

以上 curated resources 应作为额外 evidence route，而不是无条件覆盖 BioSample 或原始论文。整合时记录原资源版本、sample accession join key、record URL 和许可证。

## 7. 实施阶段门（等待样本后再进入）

**阶段 0：字段与范围对齐。** 确认首批数据类型/研究域、目标字段、输入 accession 类别、是否需要文件链接字段，以及是否接受研究级但显式标 scope 的信息。

**阶段 1：小样本审计。** 用户提供一批包含不同 accession 类型和难度的测试样本；为每例生成完整对象图、论文/补充材料线索、字段 claims、冲突/缺失和人工复核结果。此时不扩大运行规模。

**阶段 2：验收和性能评估。** 构建人工核对的 gold set，按字段与证据路线计算 accession 关系准确率、sample-level precision/recall、source locator validity、冲突召回率、覆盖率及错误归属率。对疾病、饮食、timepoint、arm、subject pairing 等容易错误下推的字段单独评估。

**阶段 3：批量采集。** 沿用历史项目中验证过的队列、缓存、限速/重试、断点续跑、原始响应留存、manifest/QC 和人工审核门；候选不得无审计地自动晋级为正式样本属性。

## 8. 当前建议的取舍

建议把**通用 accession graph + evidence ledger**作为稳定核心，把具体属性解析拆成 profile。当前不预设工具只处理人类微生物组；首个领域 profile 应由稍后提供的测试 accession、研究类型和宿主范围决定。如果首批主要是宿主相关微生物组，年龄/性别/body site/疾病/抗生素/采样可先定义字段，饮食和生活方式也纳入目标字段，但只有在样本级或可证明适用的 cohort 级证据下输出。后续增加非人宿主、bulk RNA-seq、空间组学或其他测序类型时，不重做 ID/证据底层。

用户稍后提供样本表/accession 后，再依据其 accession 类型和研究范围决定 v1 profile；不要求先提供大批样本。确认主表和证据边界后，用少量样本进入审计阶段。

## 参考来源

- [NCBI SRA metadata and submission overview](https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/)
- [NCBI BioSample attributes](https://www.ncbi.nlm.nih.gov/biosample/docs/attributes/)
- [ENA Portal API documentation](https://ena-docs.readthedocs.io/en/latest/retrieval/programmatic-access/advanced-search.html)
- [NCBI PMC BioC supplementary-material API](https://www.ncbi.nlm.nih.gov/research/bionlp/APIs/FAIR-SMART/)
- [Europe PMC REST API](https://dev.europepmc.org/RestfulWebService)
- [PMC Article Dataset AWS transition and current access](https://pmc.ncbi.nlm.nih.gov/tools/pmcaws/)
- [MIxS specification](https://genomicsstandardsconsortium.github.io/mixs/)
- [curatedMetagenomicData 3 paper](https://doi.org/10.1038/s41467-025-66888-1)
- [GMrepo v3 paper](https://doi.org/10.1093/nar/gkaf1190)
- [PRIME paper](https://doi.org/10.1093/nar/gkaf1057)
- [GutBiomeDB paper](https://doi.org/10.1093/nar/gkag1125)
- [Microbiome Repo README](https://microbiomerepo.com/docs/README.html), [Methods](https://microbiomerepo.com/about/methods.html), [Fields and data dictionary](https://microbiomerepo.com/fields/index.html)
- [MetaHQ preprint](https://arxiv.org/abs/2602.07805), [MetaHQ repository/license](https://github.com/krishnanlab/meta-hq)
