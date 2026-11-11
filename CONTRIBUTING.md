# 贡献与更新规范

本仓库采用轻量、证据优先的维护方式。请先阅读 [字段字典](catalog/schema.md)，并以 CSV 为结构化目录的记录源。

原创文档和整理目录按仓库根目录 [LICENSE](LICENSE) 采用 CC BY 4.0；代码（新增后）按 [LICENSES/MIT.txt](LICENSES/MIT.txt) 采用 MIT。提交或发布第三方内容前，必须确认来源许可允许相应使用，并保留要求的署名和链接；仅有公开 URL 不代表可以复制其数据或页面内容。

## 新增/更新资源

每个资源记录应包含：

- 稳定唯一的 resource_id、正式名称与别名；
- 官方入口；如能找到，附原始数据库论文、文档、API 和下载页面；
- 资源类型、host/ecosystem/body-site、assay、数据对象层级；
- 支持的 ID 类型和实际查询方式；
- 访问模型、认证要求、许可或使用条款；
- status、last_checked、discovery_sources、evidence_basis 和说明；
- 对 sample metadata 相关性和已知字段缺口的准确描述。

**状态规则：** active_verified 表示已核对官方页面/文档并确认至少一种核心能力；active_partial 表示资源可访问但关键范围/API/权限仍需核查；legacy、unavailable、unverified 应保留候选线索并说明原因。不要仅凭论文发表就标为活跃。

## 新增/更新专题数据集

每行代表一个研究/项目或清楚定义的 curated compilation。记录：

- Project/Study/BioProject/ENA/DDBJ accession 和论文 DOI/PMID；
- host/population、condition、body site、assay、omics 和设计；
- reported_sample_count 与明确 unit；
- raw/processed data 是否可用、下载位置、授权要求；
- metadata_domains、pairing/longitudinal 证据；
- screening_status 与理由、证据链接、日期。

同一研究有多个项目 accession 时都保留，但说明其是否重复纳入。计数必须区分 participant/subject/dyad/specimen/BioSample/Experiment/Run/analysis。不能把论文提到的变量无依据地扩展到每个样本。

## 证据和引文

- 官方资源记录/API/文档优先，其次是原始研究论文和 supplement。
- 对关键样本级字段，写清证据定位，例如 DOI/URL、supplement 文件名、worksheet/table、ID 列。
- 综述、注册目录和第三方网站用来发现候选；无法回到原始页面时保持 unverified。
- 多值字段用竖线分隔；CSV 遵循 UTF-8 和标准引号格式。
- 不复制 FASTQ、完整 abundance matrices、临床个人数据或外部数据库快照。

## 状态更新和维护

- 页面、API、下载与许可信息变化时更新 last_checked 和 notes。
- 外部服务无法访问时，重试并记录失效日期/替代入口；不要无依据地删除历史记录。
- 发现相同项目、标题别名或迁移/合并时先做 accession/DOI 对照，再合并或标注关联。
- 每次更新同步修改资源详情页、专题指南和 [research_update_log.md](docs/research_update_log.md)；候选发现和跨轮次状态快照也同步到 [resource_discovery_log.md](docs/resource_discovery_log.md)。
- 变更较大时在 pull request 中说明新增范围、关键证据和未解决项。

## 新资源记录模板

复制并填写 catalog/resources.csv 中一行相同字段结构的记录，再添加 docs/resources/<resource_id>.md 资源卡（对 Core 或专题关键资源）。

## 新数据集记录模板

复制并填写 catalog/datasets.csv 的一行；将来源链接加入 evidence_links，筛选理由写入 screening_notes。若没有可靠的某字段，留空或标注 unknown/unresolved，并说明原因。
