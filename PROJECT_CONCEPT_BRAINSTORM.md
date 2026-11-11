# 集合型工具与资源仓库：初步构想

**日期：** 2026-11-10  
**状态：** 初步 brainstorming 记录，尚非最终规格；本轮仅讨论，不实施、不建 GitHub 仓库。

## 1. 目标理解

项目不是把若干网页链接堆在一起，也不是要重建所有菌群数据数据库。目标是形成一个对自己和其他开发者都可用的开放项目，包含：

1. **资源目录**：菌群数据存储库、整合数据库、文献/补充文件 API、ontology/标准的链接和使用说明。
2. **工具目录**：可查询/下载菌群数据、metadata、处理数据或访问 repository API 的软件，标清它们解决什么问题。
3. **自研检索工作流**：从测序 accession 出发，发现关联研究和公开材料，建立 accession ↔ 作者样本 ID/subject ID 的可审计 crosswalk，再整理对应 metadata。

核心差异化能力应是第 3 项：已有 archive 和平台提供了很多 metadata，但它们不会普遍替用户完成“ID → 原始论文/supplement → 作者定义的样本 ID → 样本级 host/采样字段”的关系恢复。

## 2. 可行的项目形态

### 方案 A：静态资源清单

仓库只维护数据源、数据库、API 和工具链接，附说明、安装/使用示例。优点是最快发布、维护成本低；局限是不能直接解决输入样本 ID、找论文、解析 supplement、匹配作者样本名的核心工作，容易变成普通链接列表。

### 方案 B：资源目录 + 自研可追溯检索工具（推荐）

同一 GitHub 项目里维护资源/工具 catalog，同时提供 accession resolver、文献发现、补充材料获取、crosswalk 建立、evidence ledger 和本地导出。目录可以先给用户直接价值，工具逐步实现核心任务，结果可审计，外部数据继续由原提供方托管。代价是要维护不同 archive/API 连接器，论文与补充表的格式差异也会要求复核和迭代。

### 方案 C：中心化、持续更新的样本 metadata 数据库

除 catalog 和工具，还把大规模 accession 整理结果累积、版本化并发布为统一数据库/API。它能减少重复整理，但会带来第三方数据许可、错误更正、外部字段变化、存储与服务可用性、长期人工审核和更新责任。本项目还没有测试 accession 来证明当前就应承担这项长期运维。

**已确认首版选择：方案 B 的轻量形态——资源目录 + 本地结果。** 仓库暂不复制第三方原始数据，也不建设中央样本库。以后若用户和社区需要共享整理结果，可另设许可和治理明确的 curated release。

## 3. 建议的仓库分层

```text
resource-catalog/       数据库、平台、标准、API 的结构化登记与说明
tool-catalog/           检索、下载、解析、分析工具的用途、输入/输出和限制
schema/                 accession graph、sample entity、claim/evidence、状态模式
connectors/             SRA/ENA/BioSample、Europe PMC/PMC、MGnify、Qiita 等适配层
workflow/               ID 解析 → 论文发现 → supplement → crosswalk → claims → QC/export
profiles/               按研究域配置字段、词表和解析规则
docs/                   安装、资源选择、示例、常见错误、贡献规范
examples/               脱敏或合成输入输出，不放受限制的用户样本/数据
evaluation/             人工 gold set 规范、linking/QC 指标和评估报告模板
```

首页应清楚区分：可查数据资源、可检索/下载工具、metadata 规范化/抽取工具。SRA Toolkit（下载/转换 reads）、MetaSRA（规范 archive metadata）和 curatedMetagenomicData（已整理样本数据包）应属于不同类别。

## 4. Resource/tool catalog 应登记什么

每条记录建议保存：名称、类别、维护方、官方 URL、论文/DOI、支持的数据/样本域、主要 accession 类型、sample unit（BioSample/Run/Study）、metadata 字段、API/CLI/网页/批量下载入口、认证/限速、数据更新时间、license/使用限制、是否下载 reads、典型输入输出、已知限制、最近核查日期和维护状态。

资源目录可按以下类别扩展：原始 reads 与样本档案（NCBI SRA、ENA、DDBJ、BioSample/BioProject、GEO）；微生物组数据与分析平台（MGnify、Qiita、MG-RAST）；curated sample/phenotype catalog（Microbiome Repo、GMrepo、PRIME、curatedMetagenomicData、HumanMetagenomeDB、GutBiomeDB）；论文与附件 API；standards/ontologies；软件工具。目录要有纳入规则和社区贡献机制，避免声称永久穷尽所有网络资源。

## 5. 自研工作流的核心模块

1. **ID resolver**：识别输入 ID 类型，解析 NCBI/ENA/DDBJ 的 BioProject、BioSample、Experiment、Run 关系；保留原始输入和 secondary accession。
2. **publication linker**：综合 BioProject declared publications、ENA cross-references、Europe PMC accession mentions 和 study/title/author 信息；区分 own-data、reanalysis/reuse、仅提及 accession 等关系。
3. **public document discovery**：登记全文和 supplement 清单、格式、开放状态、许可和解析状态；优先使用正式 API 和公开链接。
4. **crosswalk builder**：寻找 accession、sample alias、library ID、subject/visit ID 的直接对应；精确 ID match 可自动确认，模糊匹配进入人工复核。
5. **claim extractor**：结构化表格优先确定性解析；正文/非结构化内容抽取候选值，并附原句、页码/章节/表格行、实体 scope 和来源。
6. **normalizer/QC**：raw 与 normalized 值并存；记录字段映射、单位/词表、冲突、missing/unavailable/query-failed/unresolved 状态。
7. **local exporter**：输出 BioSample master、Experiment/Run tables、accession graph、metadata claims、conflicts/unmatched rows 和 retrieval manifest；宽表作为便于分析的派生视图。

数据库连接器、解析规则和领域 profile 应分开。单个 API 或期刊格式变更时，可以局部更新 adapter/parser，不推翻样本表和证据模式。

## 6. 已有平台说明的设计机会

- **MGnify** 整合 ENA 样本/Run、分析结果和 API，也显示 Europe PMC/EMERALD 的论文 text-mining 注释。官方文档明确说，自动且有把握地确定某条出版物注释对应哪些样本并不可靠。这是本项目需要处理的 linkage/crosswalk 问题，不是再做一次普通关键词搜索。
- **Qiita** 是 multi-omics study、sample metadata、preparation metadata 和分析平台；适合作为资源目录条目，并在 ID 命中其 study 时作为补充来源。API 的开放状态、认证和权限要作为 catalog 字段记录。
- **SRA Toolkit / enaBrowserTools** 主要用于获取/下载 accession 对应的 sequence data/XML/文件，应与宿主 metadata enrichment 工具分栏。
- curated databases 可作为外部查询和核验 route；需要标注 sample unit、scope、数据版本和 license。

参考：[MGnify portal and publication metadata documentation](https://docs.mgnify.org/src/docs/portal.html)、[Qiita documentation](https://qiita.microbio.me/static/doc/html/index.html)、[SRA object model](https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/)、[ENA browser tools](https://github.com/enasequence/enaBrowserTools)。

## 7. 建议的阶段安排

**Phase 0 — 边界和 catalog schema。** 明确资源纳入规则、每条记录最小字段、许可证记录规则和维护责任。

**Phase 1 — ID 关系。** 以少量测试 accession 验证 archive resolver，建立 BioSample–Experiment–Run–Study graph 并本地导出。

**Phase 2 — 论文和补充材料。** 完成来源发现、文件清单和 sample alias crosswalk；统计论文存在但无法映射、文件不可访问和未匹配行。

**Phase 3 — 证据抽取。** 优先实现可验证结构化表格解析，再增加受限正文抽取；每条 claim 都要有 locator、quote 和 entity scope。

**Phase 4 — 资源发布。** 加入贡献模板、来源审核、变更记录和 link-check；工作流发布版本和 reproducibility report。若未来建设共享 curated database，再单独完成治理/许可证设计。

## 8. 价值与风险

**预期价值：** 使用者可快速找到适用数据库和软件；开发者能复用 API/CLI 示例；只有 accession 的用户可以获得 accession→文献/supplement→样本 crosswalk 的证据化结果；误把 cohort 信息赋给个体的风险更低。

**主要风险：** 资源范围过宽导致目录过时；外部 release 变化；第三方 license 限制；二次分析论文被误当成原始论文；文本抽取把 cohort-level 断言错误下推到单样本。用纳入标准、版本号、link relation、证据 scope 和人工审核门来管理。

## 9. 待继续讨论

首版采用“资源目录 + 本地结果”，暂不复制外部数据或维护中央样本库。后续继续确认 catalog/tool entries 的纳入边界、首批 connector、用户输入和输出格式、首个 profile。测试 accession 仍由用户稍后提供。
