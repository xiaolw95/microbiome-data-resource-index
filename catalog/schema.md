# 目录字段字典与受控值

**状态：** 第一阶段 1A 基线版本。实际检索后如需增删字段，须更新本文件和对应目录表头，并在变更记录中说明原因。

## 文件分工

| 文件 | 一行代表什么 | 保存内容 |
|---|---|---|
| `resources.csv` | 一个数据库、归档、平台或其他数据资源 | 资源范围、对象单位、metadata 领域、访问方式和维护状态 |
| `tools.csv` | 一个软件、API 客户端或直接辅助检索的服务工具 | 输入、输出、用途、资源关联和限制 |
| `standards.csv` | 一个报告标准、术语表或 ontology | 适用领域、字段/术语和版本 |
| `datasets.csv` | 一个项目级/研究级候选公开数据集 | 研究类型、body site、assay、accession、论文、访问条件和筛选证据 |

## 通用格式

- 文件编码：UTF-8；首行是字段名；一行一条记录；空值留空，不使用 `NA`、`n/a`、`0` 混作同一种含义。
- 需要表达“已检查但未提供”时，使用对应状态字段/说明列，而不是把空字段解释为确定不存在。
- 多值字段以竖线 `|` 分隔，例如 `16S|shotgun`；字段值本身包含竖线时使用转义或在说明列解释。
- 每个外部数据声明尽可能保留来源 URL、论文 ID、表格/章节定位和核查日期。
- 每轮检索的精确时间、查询式、来源、文件改动和未解决问题追加到 `docs/research_update_log.md`；CSV 中的 `last_checked` 只表示对应记录的最近核查日。
- 原始表述与规范化标签应同时保存：原文不被规范词覆盖；不确定时用 `unknown` 或 `unresolved` 并解释。
- 不保存大体量序列、丰度矩阵、全篇 PDF 或外部资源数据快照。

## 受控值

### `resource_type`

`archive`、`microbiome_platform`、`curated_dataset`、`literature_supplement`、`microbial_knowledgebase`、`standard_ontology`、`software_api`、`resource_discovery_portal`。`resource_discovery_portal` 表示跨多个原始仓库发现数据/工具并汇总其 metadata 的索引门户；它本身通常不托管被索引数据。

### `priority_tier`

- `core`：直接关联公共测序 accession、样本 metadata、宿主/疾病队列数据或样本级证据检索。
- `extended`：微生物组研究相关，但对象/范围更窄，或只提供特定类别数据。
- `legacy`：历史数据库、已迁移或当前维护有限的资源；保留历史用途并注明状态。

### `relevance_to_sample_metadata`

- `direct`：可直接提供样本、host、body site、phenotype 或 accession metadata。
- `supporting`：可提供关联关系、测序/分析数据、论文或补充材料线索。
- `indirect`：提供分类、功能、术语/标准或其他背景信息，不直接恢复样本属性。
- `out_of_scope_for_metadata`：列入微生物组资源全景，但对样本 metadata 检索无直接用途。

### `status`

- `active_verified`：核对了官方入口和文档，并确认至少一项核心查询/下载能力。
- `active_partial`：资源可访问，但API、数据范围或关键功能尚未完整核实。
- `legacy`：曾正式发表/使用，但当前维护、覆盖或访问能力有限。
- `unavailable`：核查时主页/服务不可用；应记录核查日期和最后有效入口。
- `unverified`：仅为候选，尚未完成官网或原始文献核对。

### `screening_status`（数据集）

- `candidate`：检索初筛命中，尚待验证研究范围或数据关系。
- `verified`：候选研究符合专题标准，主要判断有可追溯来源支持。
- `excluded`：不符合已公开的纳入标准；在 `screening_notes` 说明原因。
- `unresolved`：关键字段、归属或访问状态无法判定。

### `sample_count_unit`

`participant`、`subject`、`dyad`、`biological_sample`、`biosample_record`、`specimen`、`library`、`experiment`、`run`、`analysis`、`unknown`。母婴研究的配对人数可用 `dyad`；若论文原文采用其他单位，先记录原文并在说明中保留，不应把 Run 数直接称为受试者或 biological sample 数。

### `access_model`

建议使用简短可组合值：`open_public`、`registration_required`、`controlled_access`、`request_to_author`、`mixed`、`unknown`。在 `notes` 说明实际限制和链接。

### 主题标签

专题数据集 `search_topic` 使用小写稳定 slug，例如 `maternal_infant`、`crc`；多个主题以 `|` 分隔。疾病、宿主、body site 和 assay 的规范标签表后续按检索实际需要扩充；不能用自由文本同义词直接覆盖作者原文。

## 资源表主要字段解释

| 字段 | 规则 |
|---|---|
| `resource_id` | 唯一稳定 ID，小写 ASCII slug；不因 URL 变化而改名。 |
| `aliases` | 旧名称/缩写，以 `|` 分隔。 |
| `official_url` | 当前第一方主页/服务入口。若已检索但未找到现行官方入口，保持空值，并在 `notes` 说明检索结论；不要用综述或第三方索引冒充官方 URL。历史论文和第三方发现入口分别记入 `primary_publication` 与 `discovery_sources`。 |
| `data_unit` | 用受控对象单位表达资源能查询的实体；多个值用 `|`。 |
| `metadata_domains` | 可包含的字段类别标签，不代表每条记录都有该字段。 |
| `accepted_ids` | 经文档/接口确认可查询或互链的 ID 类型。 |
| `query_modes` | 例如 `web_search`、`rest_api`、`bulk_download`、`cli`、`manual_submission`。 |
| `auth_required` | `yes`、`no`、`partial`、`unknown`；不同功能权限不同则用 `partial`。 |
| `last_checked` | ISO 日期 `YYYY-MM-DD`；写入最后实际核对日。 |
| `discovery_sources` | 本条资源最初从哪里发现（FAIRsharing、re3data、bio.tools、NAR、综述/论文、官方资源互链等）；多值以 `|` 分隔。 |
| `discovery_date` | ISO 日期 `YYYY-MM-DD`；记录候选资源进入目录的日期，与官方核验日期 `last_checked` 分开。 |
| `evidence_basis` | 当前条目事实依据类别，例如 `official_docs`、`primary_paper`、`secondary_review`、`registry_record`；多来源用 `|`。 |

## 工具表主要字段解释

| 字段 | 规则 |
|---|---|
| `tool_id` | 唯一稳定 ID，小写 ASCII slug；工具改名或仓库迁移时尽量保留原 ID。 |
| `resource_ids` | 关联 `resources.csv` 中的 `resource_id`；多项以 `|` 分隔。通用工具没有明确单一资源关联时可留空。 |
| `input_ids` / `input_formats` | 分别记录接受的 accession/标识符类型和输入形式；不要把“理论上能解析”写成已支持。 |
| `outputs` | 记录可交付的 metadata、ID 关系、samplesheet、下载链接或 sequence files；区分元数据输出和原始读段。 |
| `limitations` | 明确归档字段依赖提交者、补充文件/临床 crosswalk 缺失、速率限制、登录和下载边界。 |
| `maintenance_status` | `active`：官方代码/文档当前可访问，且核心用途有直接依据；`active_partial`：工具或功能有依据，但维护状态、当前端点或覆盖范围尚未完整核实；`legacy`：历史工具或当前维护有限；`unknown`：状态证据不足。此字段不代表工具对本项目全部需求的覆盖率。 |
| `last_checked` | ISO 日期 `YYYY-MM-DD`；表示本目录最后检查工具来源/功能说明的日期，不等于自动化运行测试日期。 |

## 数据集表范围解释

`datasets.csv` 是**项目级发现索引**，不是样本主表。优先保存研究/项目 accession、论文、研究分类、样本部位、实验类型、可用数据、筛选依据和状态。它不应复制逐受试者临床表，也不代替未来样本级 evidence ledger。

`metadata_domains` 应标注“论文/归档声称可以提供的字段类别”及信息范围；如记录中不能核实，就标 `unknown`。`raw_data_available` 与 `processed_data_available` 可用 `yes`、`no`、`partial`、`unknown`，并分别给出链接/依据。受控访问数据可记录项目和申请入口，不尝试下载或绕过权限。

## 样本单位与信息层级

以下对象不能互换：

```text
participant/subject (人或宿主个体)
└── biological sample/specimen (一次采集的生物样本)
    └── BioSample record (归档样本登记记录；不必然与唯一受试者一一对应)
        ├── Experiment/library (实验或文库设置)
        │   └── Run (一次测序数据文件/数据单元)
        └── 可能关联其他项目、实验、Run 或分析记录
```

具体关系依数据提交而异。计数时按来源和对象粒度记录；研究文中人数、归档 BioSample 数、Run 数和进入分析的样本数分别保存，不能互相代换。

metadata claim 的信息层级至少区分：`sample`、`subject`、`visit`、`group`、`study`、`cohort`、`run_or_library`。只有明确的样本映射支持时，才将 subject/visit 数据连到对应样本；否则维持原有层级。

## 可接受证据来源

优先级建议：

1. 官方数据库/API 的记录页或下载的结构化字段；
2. 原始研究论文的 Methods、Results、Data availability；
3. 论文补充文件中的具体表、sheet、row 或列；
4. 官方项目页面/流程文档和 curated resource 的字段证据；
5. 综述或第三方网页仅用于发现候选，不能单独支撑关键纳入判断。

无明确个体 crosswalk 时，队列层描述保持 `study`/`cohort` scope，不下推到样本。
