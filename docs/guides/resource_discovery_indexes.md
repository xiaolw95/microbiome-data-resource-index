# 微生物组资源的二级发现入口

**用途：** 从研究主题发现数据库、数据仓库、软件和标准。这里列出的“索引”帮助定位资源或研究记录，本身通常不保存目标测序数据；命中后仍需回到资源官网核对样本范围、accession、字段、访问条件和发布日期。  
**核查日期：** 2026-11-11

## 按目标选择入口

| 你想找什么 | 优先入口 | 它实际索引什么 | 不要把它误认为 |
|---|---|---|---|
| 微生物组相关数据库、数据标准和数据政策 | [FAIRsharing](https://fairsharing.org/) | 人工策展、相互关联的 databases/repositories、standards 和 policies；记录含资源描述、领域标签和互链 | 原始数据仓库或逐样本 metadata 数据库 |
| 可接收研究数据的仓库 | [re3data](https://www.re3data.org/) | repository 层面的学科、内容类型、认证、persistent identifier、访问模式、许可和 API 信息；支持网页筛选、REST API 和每日 XML 导出 | 具体论文/项目/样本的索引，或仓库内 dataset 下载入口 |
| accession 查询、数据处理、元数据整理等软件 | [bio.tools](https://bio.tools/) | 生物信息学软件、web service、数据库及其功能、输入/输出、版本、许可和文档；公开 REST API 支持分页与过滤 | 软件执行环境、原始测序数据或资源质量保证 |
| 有数据库论文的生物学资源 | [NAR Molecular Biology Database Collection / Database Issue](https://academic.oup.com/nar/pages/special-collections) | 年度数据库论文及数据库集合的简要说明和近年更新；覆盖生物学多个领域 | 仅微生物组的完整清单；“发表过”也不保证当前网站/下载/API 仍可用 |
| 感染性/免疫介导疾病的跨仓库数据与资源 | [NIAID Data Ecosystem Discovery Portal](https://data.niaid.nih.gov/) | 参与来源中的 dataset、resource catalog、tool 和 sample metadata，可用门户/API 查询 | 序列或临床数据主仓库；全体公开微生物组资源的穷尽目录 |
| 德国健康、临床和流行病学研究/变量 | [NFDI4Health Health Study Hub](https://health-study-hub.de/) | study、substudy、变量、文档、研究设计和访问路径；有公开 REST API | 微生物组专库或个体数据自动下载服务 |

## 推荐的检索顺序

1. **先按目标拆词。** 加入 host/population、disease/condition、body site/environment、assay/omics、study design、地理和时期的同义词；同时尝试常见缩写。
2. **按资源类型分别检索。** FAIRsharing 找数据库/标准关系，re3data 找仓库，bio.tools 找软件，NAR 找数据库论文；疾病/临床主题可补查 NIAID，营养/队列研究可补查 NFDI4Health 和 Mica。
3. **检查记录对象。** 资源目录、repository、study、dataset、BioProject、BioSample、Run、software 和 ontology 是不同实体。不要因搜索结果都出现 “microbiome” 就认为它们可以互换。
4. **跟到官方来源。** 核对当前官网、API/下载文档、accession 格式、是否能检索样本级字段、发布时间/版本、许可和认证要求。目录记录应指向当前官方入口，并另存论文或版本证据。
5. **按本项目范围筛选。** 是否与测序数据有关？是否有人/动物/环境 metadata？是否能找到 study/sample/run ID？是否只是 taxa/genes/pathways/association？若只提供最后一类，放知识库/背景类别，不称为样本 metadata 数据源。
6. **把已知和未知分开记录。** 主页可访问、文献报告能力、实际查询/下载和逐 accession crosswalk 是不同核查层级。没有实际操作过的接口应标“文档已核对，未调用”。

## 可复用查询词

在不同入口中替换主题词，例如：

- `microbiome AND (sample metadata OR biosample OR phenotype)`
- `metagenome AND (database OR repository OR portal)`
- `human microbiome AND (diet OR nutrition OR lifestyle OR cohort)`
- `maternal infant microbiome AND (multiple body sites OR longitudinal)`
- `colorectal cancer microbiome AND (stool OR tissue OR shotgun)`
- `environmental microbiome AND (soil OR marine OR freshwater OR host)`
- `microbiome AND (accession resolver OR metadata harmonization OR sample mapping)`

把结果按“原始归档 / curated 数据库 / 数据发现门户 / 软件 / 标准或 ontology / 文献与补充材料”分开记载，再按官方证据筛选，而不要把搜索引擎命中数量当资源总数。

## 各入口使用注意

### FAIRsharing

用于了解某领域已有数据库、repository、标准和政策，并查看这些记录之间的链接。官方文档描述人工策展、record history、JSON API；GraphQL schema 可公开浏览。本项目本轮没有执行认证/全量 API 查询；如以后程序化批量使用，先按 [官方 API 文档](https://fairsharing.org/API_doc) 确认认证、速率及复用条款。

### re3data

用于找“数据应该存在哪个仓库”。API v4.0 有 repository index 和 repository detail；官网每天提供当前在线仓库的 XML export，元数据标为 CC0。找到 repository 后，还要去仓库内继续搜索 microbiome 项目、study/accession 和具体数据集。

### bio.tools

用于找可复用的软件、服务或数据库客户端。公开读取 API 默认 50 项一页，提供 `q` 全文搜索、按属性筛选、排序和单条详情；提交或修改工具记录才需要登录。搜索出的工具要再核对源代码、版本、文档、license 与维护情况。

### NAR Database Collection

适合按数据库论文追踪新资源或年度更新。2026 年 NAR 总览报告 online Molecular Biology Database Collection 共 2,173 条，并在该年度回顾中移除 319 个已停用 URL。年度数字是该篇综述所述的 collection 快照；资源是否仍可查询，必须再开官网/API。

## 结果进入本地目录的规则

- 新的真实微生物组 archive/platform/curated database 进入 `catalog/resources.csv` 并按类别写详情卡。
- 可复用的独立 CLI/API/client 进入 `catalog/tools.csv`；注册目录作为发现入口时，写清其索引对象和不托管数据的边界。
- 术语表、报告规范、字段标准进入 `catalog/standards.csv`。
- 某个论文/项目/公开 dataset 进入 `catalog/datasets.csv`；注明论文、accession、样本单位、数据和访问条件。
- 本轮查询式、时间、引用、变更和未解决状态追加到 [检索更新日志](../research_update_log.md)。

## 主要官方文档

- [FAIRsharing Getting Started](https://fairsharing.gitbook.io/fairsharing)
- [FAIRsharing GraphQL schema](https://api.fairsharing.org/schema/)
- [re3data API](https://www.re3data.org/api/doc) · [数据许可与导出](https://www.re3data.org/data)
- [bio.tools API Quickstart](https://biotools.readthedocs.io/en/latest/api_quickstart.html) · [API Reference](https://biotools.readthedocs.io/en/latest/api_reference.html)
- [NAR Database Issue 总览](https://doi.org/10.1093/nar/gkaf1427) · [NAR 特刊目录](https://academic.oup.com/nar/pages/special-collections)
- [NIAID Data Ecosystem Discovery Portal](https://data.niaid.nih.gov/)
- [NFDI4Health Health Study Hub](https://health-study-hub.de/)
