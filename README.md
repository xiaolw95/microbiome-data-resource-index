# Microbiome Data Resource Index & Dataset Discovery

本项目为微生物组公共数据的**资源目录与问题导向数据集发现**工作台。它聚合已发表/维护的数据库、归档、分析平台、专题整理数据、工具和标准，并提供按研究问题查找公开数据集的可审计索引。

> 本仓库保存轻量目录、accession、证据链接和操作说明；不存储 FASTQ/SRA、丰度矩阵或外部数据库快照。首阶段已实现资源导航和主题数据集索引；“输入样本 ID 后自动补全论文/补充材料 metadata”的自研工具属于后续阶段，当前尚未实现。

## 从哪里开始

| 你的任务 | 从这里开始 |
|---|---|
| 了解可用的微生物组数据库、归档、平台、文献入口 | [按资源类别浏览](docs/resource-categories.md) 或筛选 [resources.csv](catalog/resources.csv) |
| 先寻找数据库、仓库、软件、标准等入口 | [资源发现注册库指南](docs/guides/resource_discovery_indexes.md) |
| 从研究问题找公开数据 | [母婴多身体位点指南](docs/guides/maternal_infant_multisite.md) · [CRC 指南](docs/guides/crc_microbiome.md) · [饮食/营养与菌群指南](docs/guides/diet_nutrition_microbiome.md) · 筛选 [datasets.csv](catalog/datasets.csv) |
| 判断该从哪个 archive/platform 开始 | [检索选择指南](docs/how-to-choose.md) |
| 理解论文、补充材料、归档和整理库如何连接 | [资源关系与证据链](docs/resource-pathways.md) |
| 了解后续 accession-to-metadata 自动化方向 | [开发策略](DEVELOPMENT_STRATEGY.md) · [第一阶段实施计划](FIRST_PHASE_DEVELOPMENT_PLAN.md) |

## 当前目录快照

核查日期：**2026-11-11**

- resources.csv：116 个候选资源，状态为 97 个 active_verified、11 个 active_partial、8 个 legacy；当前没有 `unverified` 条目。新增 FAIRsharing、re3data、bio.tools、NAR Collection 四个二级发现入口，并记录其与数据仓库/样本数据库的区别。
- docs/resources/：89 张重点资源卡，介绍真实数据对象、信息范围、查询方式和限制。
- datasets.csv：13 条主题候选记录，涵盖母婴、CRC 和饮食/菌群；已验证 10 条、未解决 2 条、候选 1 条。新增 HPP 饮食—菌群候选，并保留论文参与者数与当前 EGA dataset 样本数的未解决差异。
- tools.csv：37 个工具入口，新增资源注册库查询 API、MGnify API v2 和 Microbiome Repo 静态 metadata API；覆盖 accession 解析、metadata 查询/整理、manifest 文件下载及多类 API/CLI。
- standards.csv：8 个标准入口，新增 Microbiome Research Data Toolkit 和 NFDI4Health Metadata Schema，涵盖菌群研究与健康/营养研究字段规范。

这是通过文献、官方平台和注册目录多路扩展的可追溯首版目录，不声称穷尽所有微生物组资源或数据集。`active_verified` 表示至少一项核心浏览/查询/下载能力有官方入口或文档依据，不代表本项目实测了 API、文件或逐 accession 映射；`active_partial` 与 `legacy` 条目保留了明确的访问核验缺口或历史可用性边界。检索更新按时间戳持续记录，后续可逐步纳入新资源与维护变化。

## 快速浏览

- [资源类别目录](docs/resource-categories.md)
- [字段字典与受控值](catalog/schema.md)
- [资源发现日志](docs/resource_discovery_log.md)
- [带时间戳的检索更新日志](docs/research_update_log.md)
- [资源发现注册库使用指南](docs/guides/resource_discovery_indexes.md)
- [第一阶段执行复盘与下一阶段输入](docs/phase1_completion_review.md)
- [母婴多身体位点数据集指南](docs/guides/maternal_infant_multisite.md)
- [CRC 微生物组数据集指南](docs/guides/crc_microbiome.md)
- [资源关系流程图](docs/resource-pathways.md)
- [贡献与更新规范](CONTRIBUTING.md)

## 信息和计数原则

- BioProject/Study、BioSample、subject/participant、specimen、Experiment/library 和 Run 是不同层级，数量不相互替代。
- 论文、archive、专题整理库的数字分别保留其原始单位和来源；跨项目汇总必须说明去重规则。
- 论文提到的年龄、性别、饮食、健康状态或生活方式，只有找到对应样本/受试者的 ID crosswalk 才可标为样本级字段。
- 开放 reads 不表示临床问卷 metadata 也公开；受控访问入口标记为 mixed/controlled，并遵守 DAC 与数据使用协议。
- 原文术语与规范化标签并列保存；不能确定时使用 candidate/unresolved，而不是猜测。

## 项目范围

**当前第一阶段：** 资源发现与分类、重点资源卡、工具/标准索引、母婴/CRC/饮食—菌群主题数据集发现及检索指南。

**后续阶段：** 以 BioSample 为主表并关联 Experiment/Run 的 accession-to-metadata 流程；从 archive、论文和补充文件中提取并记录证据、字段层级和访问状态。后续工具不应把没有明确样本映射的信息自动写成样本属性。

## 许可与引用

本项目原创的说明文档和整理目录采用 [CC BY 4.0](LICENSE)；未来加入的源代码采用 [MIT License](LICENSES/MIT.txt)。这两项许可不覆盖此处链接或描述的第三方数据库、论文、数据和工具；复用时请查看对应来源的原始许可与使用条款。引用信息见 [CITATION.cff](CITATION.cff)。

## 参与维护

添加或更新条目之前，请阅读 [CONTRIBUTING.md](CONTRIBUTING.md)。目录字段和状态定义以 [catalog/schema.md](catalog/schema.md) 为准。
