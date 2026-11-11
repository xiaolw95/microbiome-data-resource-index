# 微生物组资源目录与问题导向数据集发现：开发计划

> **执行说明：** 本文将作为第一阶段的工作顺序和验收依据。执行时逐项完成并更新复选框、检索日期、资源状态与证据链接。第一阶段以资料检索、分类、轻量索引和使用指导为目标，不开发后续 accession-to-metadata 自动检索引擎。

**目标：** 建立一个轻量、可维护、可供研究者和开发者使用的 GitHub 项目，系统索引已发表的微生物组相关数据资源，并帮助用户从具体研究问题发现可用的公开研究/数据集。

**架构：** 使用一个机器可读的轻量目录作为记录源，配套资源详情页、专题数据集索引和任务导向检索指南。首版只保存描述性信息、公开 accession、来源证据和外部链接；测序 reads、大型矩阵和外部数据库副本留在原始资源中。

**技术形式：** Markdown + CSV/TSV（必要时 YAML）；GitHub 仓库为主要交付形式。先用 README 和文档页验证信息架构，再决定是否用 GitHub Pages 发布静态搜索/筛选页面。不建设后端或中央数据库。

**执行状态（首版验收：2026-11-11）：** 阶段 1A–1F 的首版交付条件已完成。阶段 1B 形成 116 条可追溯候选资源：97 条 `active_verified`、11 条 `active_partial`、8 条 `legacy`，当前没有 `unverified` 条目；这是一份广覆盖的可维护目录，不声称穷尽所有资源。阶段 1C 有 89 张重点资源卡、工具目录 37 项、标准目录 8 项；bio.tools 已完成 microbiome 全分页及 accession/sample-metadata 定向扫描，NAR Database Issue、FAIRsharing、re3data 等发现入口已纳入资源导航。仍无法直接验证的 API、交互页或下载权限继续标 `active_partial`，具体缺口记在资源卡、目录注释和带时间戳日志中。阶段 1D 已有母婴、CRC 和饮食/营养—菌群指南；13 条代表性索引为 10 verified、2 unresolved、1 candidate。HPP 候选分别记录论文 10,068 名分析参与者和 EGA 页面 7,190 份粪便宏基因组样本，数量/映射尚未解决。阶段 1E 的导航、关系图、贡献规范和结构化目录已完成。阶段 1F 复盘见 [docs/phase1_completion_review.md](docs/phase1_completion_review.md)。目录、资源链接和服务状态继续滚动更新；第二阶段的 accession-to-metadata 实现尚未开始。

---

## 1. 项目定位与工作边界

第一阶段服务三种起点：

1. **找资源**：了解哪些公共归档、微生物组平台、整理型数据库、文献入口和工具存在，以及如何查询。
2. **从问题找数据集**：例如从“母婴人群不同身体位点”或“CRC 相关菌群数据”出发，筛选公开项目和论文。
3. **按 accession 查信息的资源导航**：说明已有哪些资源能查样本/测序 metadata。真正自动解析 ID、访问多个 API、处理论文补充材料并生成证据化样本结果，属于后续自研工具阶段。

### 纳入范围

- 已发表或有正式维护记录的微生物组相关数据库、归档、平台、数据集、服务、软件和标准。
- 原始 reads/测序项目归档、样本 metadata 平台、微生物组分析平台、宿主/疾病/身体位点整理数据集。
- 可辅助查论文、数据可用性或补充材料的文献服务和数据存储库。
- 分类、功能、菌株或生态系统数据库可以纳入扩展目录，但需标明其与样本宿主 metadata 的关联度。
- 公开研究/项目的轻量级索引记录：项目 accession、论文链接、研究人群/疾病、样本部位、assay、样本规模统计口径、数据下载入口和证据状态。

### 不纳入范围

- 不下载、不托管或重新分发 FASTQ/SRA、大型 BIOM/丰度矩阵、完整外部数据库快照或文章 PDF。
- 不把研究中未明确标注的数据推断为某个单独样本的属性。
- 不把“资源收录了某研究”写成“该资源一定包含年龄/性别/饮食等字段”。
- 不承诺目录能穷尽所有已发表资源；必须公开搜索渠道、纳入规则、更新时间和未核实状态。
- 不在第一阶段实现自动化样本 ID 补充检索、LLM 抽取、自动 crosswalk 或面向用户的运行服务。

## 2. 第一阶段交付物

| 交付物 | 建议路径 | 内容 |
|---|---|---|
| 项目首页 | `README.md` | 项目定位、三类用户入口、分类入口、限制、如何引用/贡献 |
| 资源目录 | `catalog/resources.csv` | 每条数据库/归档/平台等资源一行，结构化属性和链接 |
| 工具目录 | `catalog/tools.csv` | 只收录直接服务于检索、查询、下载、解析或标准化的工具/API 客户端 |
| 标准目录 | `catalog/standards.csv` | 数据报告标准、受控词表和 ontology，不与数据库混类 |
| 候选数据集目录 | `catalog/datasets.csv` | 公开研究/项目轻量索引，不保存序列或大型分析数据 |
| 字段字典 | `catalog/schema.md` | 列定义、枚举值、空值含义、命名和统计单位规范 |
| 资源详情 | `docs/resources/<resource_id>.md` | 重点资源的用途、数据对象、实际字段、查询方法和限制 |
| 检索指南 | `docs/guides/<topic>.md` | 按研究问题组织的检索词、筛选逻辑、候选项目、下载入口和注意事项 |
| 资源关系说明 | `docs/resource-pathways.md` | 原始归档、平台、论文、补充材料与整理库之间的连接图 |
| 贡献/更新规范 | `CONTRIBUTING.md` | 如何添加、核验、更新或标记失效资源 |

### 推荐仓库结构

```text
sequencing-sample-metadata/
├── README.md
├── CONTRIBUTING.md
├── CITATION.cff
├── catalog/
│   ├── resources.csv
│   ├── tools.csv
│   ├── standards.csv
│   ├── datasets.csv
│   └── schema.md
├── docs/
│   ├── resource-categories.md
│   ├── resource-pathways.md
│   ├── how-to-choose.md
│   ├── resources/
│   └── guides/
└── examples/
    └── example-catalog-row.csv
```

实际执行时先检查当前项目仓库现有文件，再按现有命名与目录调整；本结构是目标建议，不要求为符合树形结构而搬动已有记录。

## 3. 资源分类体系

资源主表的 `resource_type` 使用以下受控类别：

1. `archive`：公共序列/样本归档，例如 NCBI SRA/BioSample/BioProject、ENA、DDBJ。
2. `microbiome_platform`：微生物组数据浏览、提交或分析平台，例如 MGnify、MG-RAST、Qiita。
3. `curated_dataset`：针对特定宿主、疾病、body site 或 assay 整理的数据集/数据库，例如 Microbiome Repo、curatedMetagenomicData、GMrepo、GutBiomeDB、PRIME、HumanMetagenomeDB。
4. `literature_supplement`：论文、全文、补充材料或研究关联入口，例如 Europe PMC、PubMed/PMC、PMC BioC supplements。
5. `microbial_knowledgebase`：菌株、分类学、基因、功能、代谢通路、生态或培养资源。
6. `standard_ontology`：MIxS/MIMARKS、ENVO、UBERON、DOID 等报告标准、受控词表和 ontology。
7. `software_api`：检索/下载/解析/标准化工具，通过 `tools.csv` 维护，并链接其服务的资源。

另设 `relevance_to_sample_metadata` 标记：`direct`（直接有样本/宿主 metadata）、`supporting`（可提供关联、分析或文献线索）、`indirect`（背景或术语标准）、`out_of_scope_for_metadata`（与本任务无直接关系但属于微生物组资源目录）。

## 4. 目录数据模型

### 4.1 `catalog/resources.csv`

一行一个资源。至少包含：

```text
resource_id,name,aliases,resource_type,priority_tier,host_scope,ecosystem_or_body_sites,assays,omics_types,data_unit,metadata_domains,accepted_ids,query_modes,api_url,download_url,auth_required,access_model,license_or_terms,official_url,primary_publication,documentation_url,relevance_to_sample_metadata,status,last_checked,discovery_sources,discovery_date,evidence_basis,notes
```

字段规则：

- `resource_id` 稳定且唯一；使用小写 ASCII slug，例如 `ncbi_sra`、`mgnify`。
- `priority_tier`：`core`、`extended` 或 `legacy`。
- `data_unit` 允许多值，但需从 `study`、`sample`、`subject`、`experiment`、`run`、`analysis`、`taxon` 等枚举中选择。
- `metadata_domains` 记录资源实际可含的类别，如 `host`、`body_site`、`age`、`sex`、`disease`、`collection`、`sequencing`、`taxonomy`、`function`；不等同于每条记录都有这些字段。
- `accepted_ids` 记录可查询或互链的 ID 类型，不能仅凭格式推测支持情况。
- `status`：`active_verified`、`active_partial`、`legacy`、`unavailable`、`unverified`。
- `last_checked` 用 ISO 日期 `YYYY-MM-DD`；验证访问与查询能力时注明核验范围。
- 多个值使用 `|` 分隔，避免同一字段内使用逗号；可解析的复杂对象可在后续改用 JSONL/YAML，但首版优先保持易读。

### 4.2 `catalog/tools.csv`

建议字段：

```text
tool_id,name,tool_type,resource_ids,input_ids,input_formats,outputs,main_use,limitations,installation_or_api_url,source_code_url,license,maintenance_status,last_checked
```

收录范围限于与数据库发现、accession 解析、metadata 查询、论文/附件检索、表格解析或字段规范化直接相关的工具。分析微生物组数据但不服务本目录任务的通用软件不作为优先目录对象。

### 4.3 `catalog/standards.csv`

建议字段：

```text
standard_id,name,standard_type,domain,fields_or_terms,resource_ids,official_url,version_or_release,license,last_checked,notes
```

### 4.4 `catalog/datasets.csv`

一行一个研究/项目级候选数据集，首版不要求保存逐样本临床/人口学信息。建议字段：

```text
dataset_id,title,project_accessions,publication_ids,host_or_population,condition_or_phenotype,body_sites,study_design,assays,omics_types,reported_sample_count,sample_count_unit,raw_data_available,processed_data_available,metadata_domains,paired_or_longitudinal,access_conditions,download_links,evidence_links,search_topic,screening_status,screening_notes,last_checked
```

- `reported_sample_count` 必须搭配 `sample_count_unit`，区分 participant、BioSample、specimen、Run、library 或 analysis。
- `body_sites` 和 `condition_or_phenotype` 保留原文术语，并另行填规范标签；无法确认时填 `unknown`，不能擅自推断。
- `screening_status`：`candidate`、`verified`、`excluded`、`unresolved`。排除记录建议保留简要原因，避免重复筛查。
- 记录数据在何处获取，但不在仓库保存原始文件或大规模派生表。

## 5. 资源和数据集的发现方法

### 5.1 候选资源发现

按类别分别搜索，至少结合：

- 数据和标准注册库：FAIRsharing；
- 研究数据仓库注册库：re3data；
- 生物信息软件、数据库和服务目录：bio.tools；
- 数据库论文集合：Nucleic Acids Research Database Issue / Molecular Biology Database Collection；
- 文献检索：PubMed/Europe PMC，组合 `microbiome`、`microbiota`、`metagenome` 与 `database`、`resource`、`repository`、`portal`、`catalog`、`cohort` 等；
- 已发现资源的 reference/citation chasing、官网 related resources、API docs 和 release pages。

每次检索记录数据库名称、检索日期、精确检索式、筛选阶段和候选数。元资源注册表作为发现入口，不直接代替原始论文和官方页面核验。NAR Database Issue 可系统发现高价值数据库论文，但应与其他渠道结合，不宣称只查此来源即穷尽。

### 5.2 候选资源筛选

按以下顺序逐项核查：

1. 资源确实与微生物组数据、metadata、分析或标准相关；
2. 有可定位的资源官网、论文、API 文档或档案页；
3. 确认类型与对象单位；
4. 确认可访问的查询方式、认证和下载条件；
5. 判断对样本/数据集发现的相关性；
6. 查重名称、别名、并入/迁移关系；
7. 标注活跃/历史/未验证状态和日期。

### 5.3 主题数据集发现

每个主题先定义可复查的纳入/排除条件，再检索资源库和文献：

1. 把用户问题拆成 host/population、condition、body site、assay、study design、accession/data availability 条件；
2. 在适用的归档、平台、整理型数据库和文献入口分别搜索；
3. 合并同一研究的不同记录，并通过 accession/DOI/PMID/研究标题等标识去重；
4. 核查原始数据论文与复用数据论文，尽可能确认它们和项目的关系；
5. 对每项候选按纳入标准筛选，记录理由、字段缺口、是否可下载；
6. 输出项目级索引以及主题指南，不复制数据文件。

## 6. 专题指南的标准结构

每个专题页使用相同结构：

1. **研究问题**：用普通语言说明用户想找什么。
2. **范围定义**：宿主/人群、疾病或表型、body site、测序类型、研究设计和年份等。
3. **纳入标准**：候选至少具备什么证据。
4. **排除标准**：明确排除哪些人群、样本、实验或无关的复用研究。
5. **检索词/资源组合**：主题同义词、常见缩写、资源入口、检索日期。
6. **标准化规则**：例如将 stool/feces 保留原文并映射到标准标签；不能由泛化描述推断具体部位。
7. **候选研究表**：链接项目 accession、论文、数据下载位置、样本规模单位、metadata 覆盖和状态。
8. **筛选决策记录**：逐项列入、排除或 unresolved 的理由。
9. **获取和使用说明**：从外部资源下载什么、如何确认样本与 Run 的关系、许可/受控访问注意事项。
10. **局限**：检索遗漏风险、缺少样本 crosswalk、原始数据不公开、字段层级不明确等。

### 6.1 样板主题：母婴、多身体位点微生物组

搜索和分类字段：

- 人群：孕妇/母亲、新生儿、婴儿/儿童；是否存在明确母婴配对；
- 身体位点：母亲和婴儿分别记录 stool/gut、vaginal、oral、skin、breast milk、placenta 等；
- 时间：孕期、分娩、产后、婴儿周/月龄、纵向采样时间点；
- assay：16S/amplicon、shotgun、metatranscriptomics，以及多组学；
- 设计：paired dyad、longitudinal、cross-sectional、case-control；
- 可用性：公开项目 accession、Run/sample 清单、配对/别名 crosswalk、补充表、raw reads 与处理结果。

最重要的筛选点是母亲与婴儿样本是否能分开识别、配对关系是否明确、每个 body site 是否落实到具体样本。论文只提到“母亲和婴儿样本”而没有表格/ID 对应时，保留研究级描述，不做样本级推断。

### 6.2 样板主题：CRC 微生物组数据

搜索和分类字段：

- 条件：CRC、colorectal adenoma、healthy control 等分开标记，不默认合并；
- 样本部位：stool/feces、tumor tissue、adjacent normal mucosa、normal mucosa、oral 等分开筛选；
- 设计：病例对照、配对肿瘤/邻近组织、治疗前后、筛查或纵向队列；
- assay：16S、shotgun、宏转录组及相关多组学分开记录；
- 临床/宿主字段：stage、年龄、性别、治疗、病例/对照状态等只按明确来源标注；
- 可用性：project/run IDs、原始 reads、处理结果、临床/样本表、访问限制和下载链接。

指南应支持细分问题，例如“CRC 粪便 shotgun 病例对照”或“配对肿瘤与邻近黏膜 16S”，避免只输出一个无法直接使用的宽泛资源清单。

## 7. 展示方案

### 7.1 README 首页

首页包含：

- 一句话项目定位和“本仓库不存放大规模数据”的说明；
- 三个入口：找资源、找数据集、按 accession 查 metadata（后者标注为后续工具阶段）；
- 按任务划分的快速导航；
- Core 资源摘要表；
- 资源目录、主题数据集表、检索指南的下载链接；
- 数据来源、更新日期、覆盖边界和贡献方式。

### 7.2 目录筛选列

资源目录至少展示：名称、类别、宿主/生态系统、assay、数据对象、可提供信息、支持的 ID、查询/下载方式、访问条件、状态、核查日期。

数据集目录至少展示：主题标签、研究/项目、论文、body site、assay、设计、样本计数及单位、metadata 可用性、数据下载、筛选状态和来源证据。

### 7.3 页面技术演进

- **首版：** README + 分类 Markdown 页面 + 可下载 CSV/TSV；通过 GitHub 搜索和表格链接使用。
- **后续静态页：** 在信息结构稳定后用 GitHub Pages 展示；从同一份 CSV/YAML 生成页面，提供全文搜索和按类别/标签过滤。
- **不建设：** 第一阶段不搭建账号体系、在线数据库、上传系统、用户云端查询或大型文件托管。

## 8. 分步执行计划

### 阶段 1A：冻结目录边界和分类

- [x] 阅读并确认本开发计划与 `RESOURCE_CATALOG_PLAN.md` 的一致性。
- [x] 建立资源类型、优先级、相关性、状态、样本单位和主题标签的受控词表。
- [x] 为样本主表/数据集索引确定“样本、受试者、BioSample、specimen、Run”不得混用的计数规则。
- [x] 确认专题索引首批采用母婴多位点与 CRC 作为样板。

**完成条件：** 字段定义足以让不同人以相同规则分类一项资源或候选研究；无法判断时允许 `unknown/unresolved` 并要求写理由。

### 阶段 1B：建立资源候选清单

- [x] 从 FAIRsharing、re3data、bio.tools、NAR Database Issue 和文献检索生成首轮候选资源清单；完整注册库遍历仍需后续扩展。
- [x] 对首轮资源名称去重；别名、旧名称、并入/迁移关系在逐资源核验时继续补充。
- [x] 将首轮候选分为 Core、Extended、Legacy，并标注直接/辅助/间接相关度。
- [x] 为每条候选记录记录官网、论文/DOI、访问入口、发现来源和检索日期；无当前一方入口或原始论文的条目在 `notes` 中明确说明缺口和证据来源。
- [x] 暂时无法核实的候选保留为 `unverified`，不把猜测写成已验证事实。

**完成条件：** 候选目录可审计，每条记录都有发现来源；重点项进入下一阶段的官方核查。

### 阶段 1C：核查重点资源并编写详情

- [x] 从公共归档、文献入口和已讨论的微生物组平台/整理库开始核查。
- [x] 对资源核查真实对象单位、ID 类型、字段来源、API/下载入口、登录限制和当前访问证据；不能直接验证的能力明确保留为 `active_partial`，并在资源卡/日志记录具体缺口（不把文档证据写成已实测）。
- [x] 查看官方文档和原始论文，分清 archive 字段、平台分析结果、curation 和论文文本挖掘。
- [x] 按详情页模板编写 Core 资源说明；MiCoDa 作为一项 Extended 示例也已建立详情页。
- [x] 已核查条目标记证据来源和日期；待核实条目保留 `unverified`，继续随逐项核查更新。

**完成条件：** 用户能从详情页判断资源能提供什么、如何查询，以及它对本项目目标的限制。

### 阶段 1D：建立问题导向检索规则与专题索引

- [x] 为母婴、CRC 和饮食/营养—菌群主题建立纳入/排除标准、同义词和过滤字段；HPP 的公开 EGA 数与论文参与者数冲突时标为 unresolved。
- [x] 组合归档、平台、整理库、论文和补充材料检索路径，记录具体来源与检索日期。
- [x] 汇总候选研究 accession、论文、样本类型、assay、设计、数据状态和 metadata 证据。
- [x] 按公开性、相关性、样本映射、样本类型和 assay 标记候选、已核实、排除或未解决。
- [x] 对统计数量标注原文/归档来源和单位，避免将 Runs 误报为 biological samples。
- [x] 生成候选数据集 CSV/TSV 和专题使用指南；未下载或提交原始测序数据。

**完成条件：** 读者可以按主题筛选候选项目，查看每项纳入/排除依据，并沿 accession/论文链接到外部数据。

### 阶段 1E：发布结构和维护流程

- [x] 编写 README 的三条任务入口、分类导航、限制和贡献说明；项目引用方式待维护者身份/仓库信息确定后补入。
- [x] 建立资源分类导航；GitHub Pages 暂不启用。
- [x] 建立新增资源/数据集的提交和更新规范。
- [x] 检查内部链接、字段一致性、状态标签、数据计数单位、引用和主要下载路径；在线状态按重点入口抽样核对，非重点候选保留待查状态。
- [x] 生成首版清单和更新日期；标出未核实条目与已知覆盖缺口。

**完成条件：** GitHub 页面可以从“找资源”或“找主题数据集”入口找到下一步，CSV/TSV 可下载且字段含义清楚。

### 阶段 1F：第一阶段复盘和第二阶段输入

- [x] 总结收录资源类别、主题数据集数量、字段覆盖、未解决问题和搜索盲区。
- [x] 汇总对未来 ID-to-metadata 工具最有帮助的 API、稳定链接、可用 ID 和数据映射问题。
- [x] 把需要自研的能力与可复用外部工具分开，形成下一阶段技术需求。

**完成条件：** 已有一份可维护的资源/数据集目录，并有证据说明后续自动化工具应优先接哪些接口和匹配哪些失败模式。

## 9. 质量控制、证据和状态规则

### 资源状态

- `active_verified`：已核对官方页面/文档，至少一条核心查询/下载能力可确认。
- `active_partial`：资源可访问，但 API、数据覆盖或某些能力未充分核实。
- `legacy`：历史上有正式资源或论文，但当前维护/内容状态有限或存在迁移。
- `unavailable`：核查时官网或服务不可用；保留最后可确认的来源和日期。
- `unverified`：仅发现候选信息，尚未完成官网/论文核实。

### 数据集筛选状态

- `candidate`：关键词或平台初筛命中，尚未充分确认范围。
- `verified`：论文、数据记录和目标条件有明确可追溯的支持。
- `excluded`：不符合已写明的纳入标准；记录排除原因。
- `unresolved`：关键字段或数据对应关系无法判定。

### 证据优先级

1. 官方数据库/归档记录与下载页面；
2. 原始数据论文和作者提供的补充表；
3. 官方项目说明、仓库或维护团队文档；
4. 次级综述/引用作为发现线索，不能单独支持关键字段结论。

所有研究级描述、样本级信息和候选标签须区分。目录中不因 PubMed 关联或关键词命中而推断样本级 host traits。

## 10. 维护与使用条件

- 每条资源/数据集都保存最近核查日期。
- 建议每季度进行链接和服务状态检查；每年复核 Core 资源的功能、字段范围和版本。实际节奏可按首版工作量调整。
- 记录资源官方 license/terms；仓库仅保存资源描述、链接、必要的 accession 和短的证据摘要，不复制外部原始数据。
- 数据库/工具引用其原始论文和官方站点；项目自身提供 `CITATION.cff`、版本号和发行说明。
- 若候选中含受控访问或潜在个人信息，目录只记录访问条件和官方入口，不尝试绕过权限或导出身份信息。

## 11. 第一阶段总流程

```mermaid
flowchart LR
    accTitle: 资源目录与问题导向数据集发现
    accDescr: 先系统发现并核查资源，再从具体研究问题构建轻量候选数据集索引和检索指南，最后以GitHub文档、表格和静态目录发布。

    scope[定义范围与分类] --> discover[注册库与文献发现候选资源]
    discover --> verify[核查官网、论文、API和访问条件]
    verify --> resource_index[建立资源、工具和标准目录]
    question[提出人群疾病或位点问题] --> criteria[拆解筛选条件和检索词]
    resource_index --> criteria
    criteria --> search[跨归档平台整理库和文献检索]
    search --> screen[筛选、去重并记录证据状态]
    screen --> dataset_index[形成轻量级项目与数据集索引]
    dataset_index --> guides[编写专题指南和外部下载路线]
    resource_index --> publish[GitHub文档与静态索引]
    guides --> publish

    classDef input fill:#fef3c7,stroke:#ca8a04,color:#713f12
    classDef process fill:#dbeafe,stroke:#2563eb,color:#1e3a5f
    classDef output fill:#dcfce7,stroke:#16a34a,color:#14532d
    class question,scope input
    class discover,verify,criteria,search,screen process
    class resource_index,dataset_index,guides,publish output
```

## 12. 主要风险和对应做法

| 风险 | 做法 |
|---|---|
| “所有已发表资源”数量大且持续变化 | 公开发现来源、检索式和日期；Core 深核查，Extended 轻记录，Legacy 单列；不宣称绝对穷尽 |
| 同一项目有多个名称和数据库 ID | 保存别名及多个 accession；用项目 accession、论文 DOI/PMID 与样本 ID 作为交叉核验键 |
| sample/run/participant 数量容易混淆 | 每个样本量必须带单位和来源；按目标场景说明 biological sample 与 Run 的区别 |
| 论文/队列信息容易被错误归到个体样本 | 记录信息 scope；没有明确 crosswalk 时只标研究级或 unresolved |
| 资源链接或 API 变化 | 保存官方文档、版本/状态、最后核查日期；旧入口不直接静默覆盖 |
| 专题检索召回不全或术语不一致 | 保存检索式、同义词、资源范围、纳入/排除理由和未解决项；分别保留原文和规范标签 |
| GitHub 目录逐渐变成数据镜像 | 明文限制只收轻量索引、短证据摘录和链接；大文件全部指向上游资源 |

## 13. 发布前验收清单

- [x] README 能分别引导“找资源”“找数据集”和未来的“按 accession 查询”。
- [x] 数据库、归档、平台、数据集、工具和标准分开分类。
- [x] 每个 Core 资源有官方入口、论文/文档、数据单位、查询方式、适用场景和限制；尚未实测的能力保持待核状态。
- [x] 每条专题候选数据有项目/论文链接、主题标签、body site、assay、设计、计数单位、可用性和筛选状态；未统一合并的项目不强行报告总数。
- [x] 母婴指南能区分母亲/婴儿、body site、时间点和配对关系。
- [x] CRC 指南能区分疾病类型、病例对照、组织/粪便位点、assay 和访问条件。
- [x] 未确认内容被标为 `unverified`、`candidate` 或 `unresolved`，不写成确定结论。
- [x] 结构化目录可下载，且没有大型 reads、丰度矩阵或外部库快照。
- [x] 已核实的状态/数据 availability 带有日期和来源；未核实候选有 discovery source/date 并明确保持 `unverified`。
- [x] 贡献者能按模板补充资源，不会因添加单条记录而破坏目录字段和类别规范。

## 14. 关键发现入口

- [FAIRsharing](https://fairsharing.org/)：数据库、标准和数据政策的策展注册库。
- [re3data](https://www.re3data.org/about)：跨学科研究数据仓库注册库，带筛选和 API。
- [bio.tools](https://bio.tools/)：生命科学软件、数据库、服务和工作流注册目录。
- [NAR Database Issue](https://academic.oup.com/nar/pages/ms_prep_database)：发表数据库的年度重要入口之一。
- [NCBI SRA metadata overview](https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/)：SRA Study/Sample/Experiment/Run 对象模型。
- [ENA programmatic access](https://ena-docs.readthedocs.io/en/latest/retrieval/programmatic-access.html)：ENA 搜索、记录与文件程序化访问说明。
- [PMC BioC supplementary materials API](https://www.ncbi.nlm.nih.gov/research/bionlp/APIs/FAIR-SMART/)：可用的 PMC Open Access 补充材料机器可读入口。

## 15. 后续执行约定

开始执行后先完成阶段 1A 的分类和数据字典，再进行候选发现；不先批量抓取数据。每完成一阶段，就更新本计划的复选框、相应目录文件和简短进度记录。专题索引先以母婴和 CRC 验证分类设计，确认字段可复用后再扩展主题。第一阶段完成后再根据实际目录和检索盲区制定第二阶段 accession-to-metadata 工具计划。
