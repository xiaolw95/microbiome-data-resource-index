# 第一阶段执行复盘与下一阶段输入

**盘点日期：** 2026-11-11　**依据：** `FIRST_PHASE_DEVELOPMENT_PLAN.md`　**当前判断：** 第一阶段首版验收完成，后续按时间戳日志滚动维护；`active_partial` / `legacy` 是公开记录的访问或历史边界，不阻止首版目录交付。第二阶段尚未启动。

## 1. 当前目录

| 内容 | 当前状态 | 使用边界 |
|---|---:|---|
| `catalog/resources.csv` | 116 条；97 `active_verified`、11 `active_partial`、8 `legacy`、0 `unverified` | 资源候选索引，不是所有数据库的穷尽清单；资源类型与状态以 schema 为准 |
| 资源详情卡 | 89 张 | 说明重点资源能提供什么、如何访问和已知限制 |
| `catalog/datasets.csv` | 13 条：母婴 5 条、CRC 7 条、饮食/菌群 1 条；10 `verified`、2 `unresolved`、1 `candidate` | 研究/项目级发现索引，不是 BioSample 主表，也不是样本数清单 |
| `catalog/tools.csv` | 37 项：新增资源注册库查询、MGnify API v2、Microbiome Repo 静态 API 等工具/接口入口 | 覆盖 accession 关联解析、metadata 查询/整理、manifest 下载、samplesheet 生成、raw-read 下载及通用 omics 注释检索 |
| `catalog/standards.csv` | 8 项：新增 Microbiome Research Data Toolkit、NFDI4Health Metadata Schema | 用于字段设计/报告和术语标准化；不会提供样本值 |
| 使用文档 | README、类别导航、选择指南、资源关系图、母婴指南、CRC 指南、贡献规范 | 能从“找资源”或“按研究问题找数据”进入；输入 accession 的自动查询仍未实现 |

资源类别数为：11 个 archive、48 个 curated dataset、2 个 literature/supplement 入口、30 个 microbial knowledgebase、19 个 microbiome platform、2 个 resource discovery portal。分类是为发现与使用而设，并不意味着不同类别互斥或功能等价。

## 2. 数据与字段覆盖

专题数据集记录包括项目 accession、论文 ID、host/population、疾病/表型、body site、study design、assay/omics、报告计数及单位、raw/processed availability、metadata domains、配对/纵向信息、访问条件、下载链接、证据链接、筛选状态和最后核查日。当前 13 行均有 accession、论文证据、计数单位、筛选说明和核查日期；同一主题中保留论文报告数、EGA dataset 数、BioSample/Experiment/Run 数等各自原始口径。HPP 新增条目将论文 10,068 participants 与 EGA 当前列出 7,190 粪便宏基因组样本标为 unresolved，等待数据版本和样本映射核对。

`metadata_domains` 描述来源中声称或论文报告可提供的信息类别，不承诺每个样本都有字段。只要缺少 BioSample/subject/visit crosswalk，队列年龄、饮食、病情或生活方式只能保持 `study`/`cohort` 层级，不能批量复制成样本属性。

当前最明确的未解决示例是 MUIS/PRJNA833324：论文报告 2,453 samples，BioProject narrative 报告 2,319，而当前 NCBI 项目页列出 1,842 BioSamples 与 1,842 SRA Experiments；归档还说明部分 reads 曾在其他 BioProjects 发布。此记录继续标为 `unresolved`，需按 BioSample accession 跨项目去重，再检查补充表和 assay 关系。

## 3. 重点来源与复用接口

后续工具优先采用有明确对象关系、官方文档和可审计输出的路径：

| 来源/工具 | 可复用用途 | 当前限制或核查重点 |
|---|---|---|
| NCBI Entrez / EDirect | BioProject、BioSample、SRA Experiment/Run 记录与链接查询；批量获取 XML/JSON | 字段质量受提交者 metadata 约束；本身不恢复文章 supplement 中的 host crosswalk |
| ENA Portal API | 按 accession/研究查询 INSDC project、sample、experiment、run 和文件信息 | 需核实字段映射、返回格式与 NCBI 记录差异 |
| Europe PMC REST API、PMC BioC Supplementary Materials | DOI/PMID、OA 全文、supplement 和 accession mentions 的候选发现 | supplement 结构多样；文件出现不代表其中的 subject ID 能精确连回 BioSample |
| EGA Public Metadata API | 公开 Study/Sample/Experiment/Run/Dataset 等 metadata 与跨对象引用 | 临床或问卷字段可能受控，需 DAC/数据使用批准；公开 API 不会绕过访问条件 |
| MGnify API、MG-RAST API、Qiita | 命中平台内部已收录的样本、项目和分析对象，补充 archive 之外的线索 | 平台内部 ID 与 INSDC accession 的互链需记录，不把平台命中当作全量覆盖 |
| MAMI、Microbiome Repo、curatedMetagenomicData、GutBiomeDB、Metalog、Meta2DB | 已整理范围内的主题候选、样本/研究映射、metadata 和 profiles；可用作二级检索或交叉核验 | 各自有宿主、assay、body site 或测序类型边界；版本与 ID crosswalk 必须逐资源确认 |
| EDirect、PySRAdb、SRA Toolkit | 复用现有命令行工具完成查询/解析或用户明确需要的 reads 下载 | SRA Toolkit 不负责论文/补充表抽取；初期不自动下载大体量数据 |

`ffq` 是目前工具目录中最接近“输入 ID 后展开归档关联”的 CLI：它从 GEO/SRA/ENA/DDBJ/BioSample 记录递归列出下游 accession，个别版本也支持 DOI；它仍只返回上游 archive 已暴露的字段。`nf-core/fetchngs` 可从 SRA/ENA/DDBJ/GEO ID 列表获取 ENA metadata、生成 samplesheet 并下载 FASTQ；`fastq-dl`、ENA Browser Tools 和 SRA Explorer 更偏向 accession 到 Run/文件的元数据与下载。新增的 Kingfisher/iSeq 扩展多归档查询与 reads 获取，iSeq 覆盖 GSA；`metatools_ncbi`、`grabseqs`、GEOfastq 和 SRA Run Selector 分别覆盖 NCBI 批量 metadata、SRA/MG-RAST、GEO→ENA 及官方 RunInfo 导出路径。以上工具可以复用为 archive 层基线，不能代替论文正文、补充材料中 sample-to-subject crosswalk 的发现和证据审计。完整输入类型、输出和限制见 [tools.csv](../catalog/tools.csv)。

近期纳入的 [GutBiomeDB 论文](https://doi.org/10.1093/nar/gkag1125)报道人类肠道 16S 样本整理、profiles/metadata 下载和 REST endpoints；API schema 尚未逐一实测。[gutDBase 论文](https://doi.org/10.1093/nar/gkag1136)确认疾病/数据类型浏览和处理后结果下载，因此状态已为 `active_verified`，但 sample crosswalk 与许可仍待单独检查。NIBN JMD 公开页报告 2,273 个样本/2,068 名参与者，并说明饮食、营养、活动字段的公开范围及登录限制；MicrobeAtlas 官网 Sample Groups 页面提供浏览/下载入口，但完整 schema 和单 accession 查询未实测。gutMDisorder 官网记录 v3.0 于 2026-06 发布。dbGaP 可提供公开研究变量及受控个体表型，并在提交结构中设有 subject-sample mapping；NMDC 提供环境样本 metadata 和 REST API，但官方不支持 human microbiome；GOLD/IMG/M/JGI Data Portal 提供项目 metadata、生态分类、功能分析或 JGI 文件检索下载。SPIRE/Ocean-M 支持 shotgun 与海洋环境样本上下文发现；HRGM2、MRGM、MOMD 是微生物参考基因组资源，不应当作临床样本 metadata 来源。MicrobiomeDB 有按 MIxS/custom ontology 查询样本描述的设计和 2024 年 shotgun release 公告，但当前研究表未初始化，仍为 `active_partial`。2026 年 NAR Database Issue 补入 ResMicroDb、gutMSNP、VIRE 和 PanGBank；BacDive 提供菌株来源与序列上下文。另核实了 GEO/BioStudies、HumanMetagenomeDB、AncientMetagenomeDir、动物 metagenome 资源、HMP DACC、MetaSRA、eHOMD、BugSigDB、African Human Microbiome Portal 和 MetaHQ。OAGR 的 re3data 状态标为 2022 年离线；Adelaide/Research Data Australia 保留了其古代人类 genome/microbiome 研究数据的 DOI 目录记录，因此现作为 `legacy` 历史入口保留。

## 4. 面向 accession-to-metadata 工具的需求

### 4.1 数据实体与输出

- 主记录以 BioSample/生物学样本为中心；BioProject/Study、Experiment、Run 和文件单独保留并用关系表连接。
- 建议首版输出拆成 `biosamples.csv`、`experiments.csv`、`runs.csv`、`metadata_claims.csv`、`unmatched_links.csv` 与 `retrieval_log.csv`，让“一样本多文库/多 Run”和“样本 ID 不匹配”可审计。
- 每条 metadata claim 保存原文值、规范值、属性、信息层级、来源 URL、表/worksheet/行或段落定位、提取日期、访问状态、映射方式和审阅状态。
- 仅在明确 crosswalk 支持时将 subject/visit/组别字段连接到样本；无映射、冲突或仅 cohort-level 的信息要保留原层级。

### 4.2 检索路线

1. 识别输入 ID 类型并查询 NCBI/ENA/EGA 等官方 archive；递归展开 BioProject/Study → BioSample → Experiment → Run，但保留各自 ID 和多对多关系。
2. 用项目论文、publication link、Europe PMC/PMC 和 data availability 声明寻找原始研究，区分原始数据文章与二次分析文章。
3. 发现论文 supplement 和关联数据文件；优先对精确 accession、作者 sample ID、library ID 做可追溯 join，保留未匹配行。
4. 只在直接映射不足时产生候选文本匹配；候选必须有定位和审阅状态，不能把模糊字符串匹配自动写成样本事实。
5. 对每个字段保存来源和访问条件，分别输出 public、controlled、request-to-author、missing、conflict 和 unresolved。

### 4.3 需要纳入的失败模式

- Project narrative、论文、BioSample、Experiment 和 Run 的计数不同；
- 一个 biological specimen 对应多个 BioSample/Experiment/Run，或一个研究拆在多个 BioProjects；
- supplement 列名变化、PDF/图片表、不同 sheet 的 ID 别名和重复样本；
- 论文提供 cohort demographics 但未提供 participant/sample crosswalk；
- 原始 reads public，但问卷或临床 metadata 需 EGA/dbGaP 授权；
- accession 页面/论文缺失、链接不可读、记录更新或 API response schema 变化。

## 5. 验收与待办

### 已完成的本地一致性核对

- 资源、数据集 CSV 均能按 CSV 导入，字段名与 schema 对齐；资源 ID 和 dataset ID 均无重复。
- 数据集筛选状态、资源状态分布、sample count unit 与 README 当前快照一致。
- 本地 Markdown 相对链接检查没有发现失效目标；重点官方入口已抽样在线打开。
- 没有下载或把外部原始数据复制进项目，也没有把工具实现或示例 accession 测试混入第一阶段。

### 首版完成后的持续维护项

- 当前目录有 116 条资源：97 `active_verified`、11 `active_partial`、8 `legacy`。未解决项保留其真实状态，不要求为了“清零”而把无法在线验证的 API 或历史站点误标为可用。11 条 `active_partial` 为 MicrobiomeDB、CNGBdb MDB、AnimalMetaOmics、MICROBE Data Portal、AgMicrobiomeBase、The Microbe Directory、MetaSUB Reproducible Metadata、MetaVR、metaTraits、metagRoot 和 Celeri；各自原因见目录备注和资源卡。2026-11-11 抽查将 PLaBAse、OMDB、Microbiota Vault、VirJenDB、AMRnet 更新为 `active_verified`，但未调用 API 或实际下载文件。
- 资源发现可以继续增补：本目录结合 NAR Database Issue、FAIRsharing、re3data、bio.tools、官方项目网站及原始论文，作为广覆盖起点，不声称穷尽。bio.tools 的定向查询与 microbiome 分页结果已归档，但更宽关键词和全库未穷尽；FAIRsharing 的认证 GraphQL 检索未执行。它们是后续维护路线，不阻塞目前首版作为可用索引交付。
- 在线核验仍为重点抽样；所有资源页面可能变化。Celeri 当前页面显示暂无更新且表格仍在加载；Metalog 受 anti-bot 限制，部分 portal/API 无法被当前浏览工具解析。8 条 `legacy` 是历史入口记录，具体旧文件、替代入口或迁移信息应在实际复用前再核验。
- 专题表目前以母婴、CRC 和饮食/营养—菌群为可审计样例，不代表专题候选完整。PRJNA833324 仍需按 BioSample 去重并审核 supplement crosswalk；PRJNA943491 保留 candidate；HPP 论文参与者数与当前 EGA 样本数、diet-log 的申请范围仍 unresolved。
- 已为首版准备 [CC BY 4.0 目录/文档许可说明](../LICENSE)、未来代码用 [MIT 许可](../LICENSES/MIT.txt) 和 [CITATION.cff](../CITATION.cff)，署名使用已连接 GitHub handle。GitHub 账号连接可读，但目标仓库尚不存在，当前没有 `.git`、remote 或公开 release。

这些条目纳入带时间戳的滚动维护日志；目前第一阶段首版可以供浏览、过滤、专题检索和外链使用。第二阶段的样本 ID 自动解析与论文/补充文件 metadata 回收尚未开始，等待用户明确开始并提供测试样本表或 accession。
