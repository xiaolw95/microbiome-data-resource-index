# 资源发现日志

**本轮检索日期：** 2026-11-10  
**阶段：** 第一阶段 1B 首轮候选资源发现  
**目录：** `catalog/resources.csv`  
**重要说明：** 当前清单是可追溯的候选种子表，不是“已穷尽所有微生物组数据库”的声明。`unverified` 状态表示只发现候选名称或次级记录、尚缺官方页面/原始论文核实；曾发表但当前服务不明的资源按 `legacy` 记录，已有范围证据但入口或能力仍有缺口的资源按 `active_partial` 记录。

## 检索方法

使用了资源注册库描述、综述资源表、数据库论文和官方资源页进行交叉发现。检索器返回结果用于发现候选；目录中的状态只有在打开官方页面/文档或原始论文后才能升级。

本轮使用的主要检索表达包括：

- `microbiome database sample metadata database human gut microbiome database resource 2024 2025 NAR database issue`
- `microbiome databases registry sample metadata microbiome repository database list`
- `site:fairsharing.org microbiome database repository resource microbiome`
- `site:biotools.org microbiome database tool metagenome microbiome resources`
- 另外检查已讨论资源的官方主页、API 文档、发布页，以及综述和数据库论文的资源比较表。

## 发现渠道

| 渠道 | 用途 | 本轮记录 |
|---|---|---|
| [FAIRsharing](https://fairsharing.org/) | 发现数据库、标准和数据政策之间的关联 | 用于确定发现入口；当前没有导出完整 microbiome 条目集，不将其结果计作穷尽式检索 |
| [re3data](https://www.re3data.org/about) | 发现研究数据仓库及其开放性、许可和元数据属性 | 作为归档/仓库类资源发现入口；首轮关键词检索后仍需逐项回查 |
| [bio.tools](https://bio.tools/) | 发现软件、数据库、工作流和服务 | 作为后续 `tools.csv` 的候选来源；本轮未声称已逐条遍历 |
| [NAR Database Issue](https://academic.oup.com/nar/pages/ms_prep_database) | 发现发表过数据库论文的资源 | 与综述和项目网站交叉使用；该入口本身不是穷尽清单 |
| [Metalog 资源比较表](https://academic.oup.com/nar/article/54/D1/D826/8307355) | 从一份近期的 non-exhaustive metadata database overview 扩展候选 | 提供 Murine/Animal Microbiome Database、Human Microbiome Compendium、mBodyMap、GMrepo、MicrobeAtlas、AncientMetagenomeDir、Marine/TerrestrialMetagenomeDB、Meta2DB、curatedMetagenomicData、HumanMetagenomeDB 等候选 |
| [H3ABioNet microbiome resource list](https://microbiome.h3abionet.org/microbiome/resource/) | 扩展区域/疾病/门户/分类数据库候选 | 提供 African Human Microbiome Portal、Human OncoBiome、MicrobiomeDB、HMP Portal、eHOMD、Disbiome、Microbiome Database 等候选 |
| [2023 数据库与资源综述](https://pmc.ncbi.nlm.nih.gov/articles/PMC10073628/) | 扩展环境、宿主、分析平台和较早数据库 | 作为候选发现来源，需逐项核验资源当前状态 |
| [2026 人类肠道微生物组资源综述](https://pmc.ncbi.nlm.nih.gov/articles/PMC12950768/) | 扩展疾病、营养和肠道资源候选 | 提供 GIMICA、DISBIOME、gcMeta、gutMDisorder、NIBN JMD 等候选；不把综述表述直接转作已核实能力 |
| 重点资源官方页/原始论文 | 核实资源具体范围和当前维护线索 | 已对部分核心候选完成核查，详见 `catalog/resources.csv` 的 `status`、`evidence_basis` 和日期 |

## 首轮候选结果（1B 初始快照）

首轮 1B 快照中的 `catalog/resources.csv` 有 **44 条不同名称的资源候选**。当时状态分布为：

| 状态 | 数量 | 解释 |
|---|---:|---|
| `active_verified` | 11 | 当前已核对官方说明或页面，至少一项核心能力有官方依据 |
| `active_partial` | 7 | 有官方页面/原始论文支持部分信息，访问/API/版本或某些范围仍需进一步核查 |
| `unverified` | 26 | 候选条目已发现，但尚未完成官方核实 |

候选资源覆盖公共归档、文献/补充材料、微生物组平台、整理型数据库和微生物知识库。以上是 44 条初始候选入库时的状态快照；工具与标准目录后来已在第一阶段独立建立，见 `catalog/tools.csv` 和 `catalog/standards.csv`。

## 去重和状态注意事项

- 资源名称相同或相近时，以稳定 `resource_id` 管理；别名写在 `aliases`。本轮发现同名 `MicrobeAtlas` 候选重复，已合并成一个候选行；官方项目身份及 Sample Groups 浏览/下载入口已核，完整下载 schema 和逐 accession 查询未实测。
- 综述中“有 N 个样本”可能指 Run、BioSample、specimen 或 participant；在官方原文核验前，不能把这些计数当作可比较的 biological sample 数。
- 论文发表日期不等于资源仍在维护。对候选状态要分别记录“核心能力有无证据”和“当前服务是否仍可用”：只由次级提及支持的候选保持 `unverified`；已发表但服务不可定位/超时的历史资源可标为 `legacy`；有官方范围证据但主交互入口未成功核验时可标为 `active_partial`。
- `active_verified` 仅表示完成了有限范围的文档/页面核对，不代表已测试全部 API、下载接口或每种 ID。
- 以上 44 条是首轮入库快照；后续新增和状态变化见本日志后续段落。资源发现仍应继续参考文献追踪、注册库记录、原始数据库论文和资源互链，并将候选按同一标准记录。

## 阶段 1C/1D 补充核查与专题数据集首轮（2026-11-10）

首轮在 44 条基础上新增 MAMI 和 EGA。目录后来根据近期论文更新 GutBiomeDB、Metalog、Meta2DB 并新增 gutDBase；随后补查 mBodyMap、MarineMetagenomeDB、TerrestrialMetagenomeDB、动物/环境资源及人群和疾病关联资源。该轮结束时的目录快照是 49 条；其后增补与状态变化见本日志后续段落。历史阶段中的 `unverified` 表示当时尚缺官方服务核实，不表示资源无效或不可访问。母婴与 CRC 专题索引共 12 条：10 `verified`、1 `unresolved`、1 `candidate`。

### 主题数据集检索路径

- 母婴：MAMI 官方 accession/abundance 下载页；Microbiome Repo mother-infant filter；NCBI SRA/BioProject、ENA；Europe PMC/PMC 原始论文和补充材料；EGA Lifelines NEXT study 页面。
- CRC：NCBI SRA/BioProject、ENA；Europe PMC/PMC 与专题论文；Research Data Gouv 的 CRC stool shotgun compendium；AC-ICAM、Colobiome 和新近 FFPE/tissue 研究的数据可用性页面。
- 首轮检索词围绕 maternal/infant/newborn、mother-infant transmission、multiple body sites、longitudinal、CRC/adenoma、stool/feces、tumour/adjacent normal、16S、shotgun 和 metatranscriptomics 组合。
- 数据集目录记录 12 条项目/整理集合：10 条 `verified`、1 条 `unresolved`、1 条 `candidate`。这是一组用于验证信息结构的代表性首轮候选，不宣称穷尽所有已发表数据。

### 本轮识别到的计数/映射问题

- PRJNA322188：论文采集 specimens、QC 后分析 specimens、NCBI BioSamples 和 SRA Experiments 是不同数字；目录分别保留来源口径。
- PRJNA352475：论文的 25 dyads/216 高质量 metagenomes 与 NCBI 的 230 BioSamples/Experiments 不是同一计数单位。
- PRJNA833324：论文报告 2,453 samples，BioProject narrative 报告 2,319，而当前 NCBI 项目页面列出 1,842 BioSamples 和 1,842 SRA Experiments；页面还提示部分数据曾在其他 BioProjects 发布。保持 `unresolved`，后续应按 BioSample ID 去重核查。
- Lifelines NEXT：论文报告 4,526 longitudinal fecal specimens，EGA 页面列 4,577 records；同时存在 public SRA reads 与需申请的 EGA metadata/reads。
- CRC pooled analysis：3,741 stool metagenomes 来自 18 cohorts，其中 2,116 来自既有公共队列、1,625 来自六个新队列；目录明确不把汇总数归到单个 accession。
- AC-ICAM 与 PRJNA943491 等数据也需区分研究/参与者、specimen、BioSample、Experiment/Run 和不同 assay 子集。

### 本轮新核实的重点来源

- [MAMI 官方资源下载页](https://bioinfo.ioz.ac.cn/mami/resource.php) 和 [2024 NAR 论文](https://doi.org/10.1093/nar/gkad813)：母亲六类、婴幼儿四类身体位点；站点按 Mother/Infant 与 body site 提供 accession 和 abundance 表。
- [EGA Public Metadata API 文档](https://ega-archive.org/discovery/metadata/public-metadata-api/) 与 [Lifelines NEXT EGA Study](https://www.ega-archive.org/studies/EGAS50000000133)：公开 Study/Dataset/Sample/Run metadata 与授权临床数据分层。
- [MUIS 母婴多位点文章与 SRA](https://www.sciencedirect.com/science/article/pii/S1931312823000434) / [PRJNA833324 SRA record](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA833324)：论文样本数与归档描述不一致，示范了必须留存 unresolved 的情形。
- [CRC 跨队列 3,741 metagenomes 论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC12283368/) 与 [Zenodo 整理 profiles/metadata](https://doi.org/10.5281/zenodo.15069068)。
- [CRC 2,340 stool shotgun compendium](https://entrepot.recherche.data.gouv.fr/dataset.xhtml?persistentId=doi:10.57745/7IVO3E)：15 cohorts 的人类粪便 shotgun profiles 和整理 metadata，底层 raw reads 留在各归档。
- [GutBiomeDB 2026 NAR 论文](https://doi.org/10.1093/nar/gkag1125)：官网可访问，说明其整理的是 168,464 个 human-gut 16S 样本/482 个 BioProjects，提供 metadata/profile 下载和 46 个 public REST endpoints；本项目尚未独立枚举 API schema。
- [gutDBase 2026 NAR 论文](https://doi.org/10.1093/nar/gkag1136)：新增为 `active_partial` Extended 候选；官方 JavaScript portal 可解析，但下载文件和 sample crosswalk 尚未审计。
- [Metalog 2026 NAR 论文](https://doi.org/10.1093/nar/gkaf1118)：补录 EMBL 官方站点链接；站点在本轮在线检查返回 anti-bot access denial，因此保留 `active_partial`。
- [Meta2DB 2026 Bioinformatics 论文](https://doi.org/10.1093/bioinformatics/btag422)：补录官方入口和论文链接并升级为 `active_partial`；具体覆盖与下载细节待逐项核对。
- [MarineMetagenomeDB 官方站点](https://web.app.ufz.de/marmdb/) 和 [2022 论文](https://doi.org/10.1186/s40793-022-00449-7)：网页显示可筛选并导出 CSV/下载 raw sequence；其 Release 1.0（2021-06）为 11,449 条海洋 shotgun metagenome metadata。
- [TerrestrialMetagenomeDB 官方站点](https://web.app.ufz.de/tmdb/) 和 [2020 NAR 论文](https://doi.org/10.1093/nar/gkz994)：网页显示 Release 2.0（2021-01）共 20,206 条记录，支持环境字段过滤和 CSV 下载；标记当前入口可用，内容版本较旧。
- [mBodyMap 官网](https://mbodymap.microbiome.cloud/) 和 [2022 NAR 论文](https://doi.org/10.1093/nar/gkab973)：多身体位点/疾病相关资源；主页能加载，但本轮未交互验证筛选和导出，状态设为 `active_partial`。
- [AnimalMetagenome DB 论文/数据](https://doi.org/10.1038/s41597-022-01444-w) 与 [Figshare 数据记录](https://doi.org/10.6084/m9.figshare.19728619)：论文描述样本、Experiment、Project 和 PubMed 交叉链接，数据仓库可作为研究入口；数据库官网当前访问未确认。
- [AnimalAssociatedMetagenomeDB](https://web.app.ufz.de/aamdb/) 与 [Animal Microbiome Database / AMDB](https://www.amdb.online/)：本轮找到论文或官方站点线索，但站点请求超时，故未将其标成当前 verified。

### 追加候选核验（2026-11-10）

本轮补查的代表性检索式包括：`"Murine Microbiome Database" 554 samples`、`site:bio-computing.hrbmu.edu.cn/gutMDisorder "v3.0"`、`"The Human OncoBiome Database" URL`、`site:microbiome.nibn.go.jp/microbiome-database/ "4,578" "4,302" "2,273"` 和 `"MicrobeAtlas" database 2026 Cell`。按“当前官网/服务页 + 原始论文 + 访问范围”的顺序核查，状态据证据强度更新如下：

- [NIBN JMD 官方数据库页](https://microbiome.nibn.go.jp/microbiome-database/) 与 [2025 论文](https://doi.org/10.1038/s41598-025-04339-z)：官方区分整体库的 4,578 条 16S 和 4,302 条 shotgun 数据，与公开版 2,273 个样本/2,068 名参与者；公开版含年龄组、性别、地区、饮食和营养摄入。完整数据访问自 2026-02-05 起要求账户登录；一部分更详细表型仅向通过伦理审查的合作方提供。年龄经分组以保护隐私。新增 Core 资源卡；其样本 ID 与 DRA accession 的逐样本 crosswalk 仍待核。
- [gutMDisorder 官网浏览页](https://bio-computing.hrbmu.edu.cn/gutMDisorder/browse.dhtml) 和 [v2.0 数据库论文](https://doi.org/10.1093/nar/gkac871)：官网列有文献关联与 raw-data-based 关联、人/鼠宿主、gut/oral 来源及疾病/表型/干预类别，包含 diet/food/nutrition；release history 记录 2026-06-10 发布 v3.0。更新为 `active_partial`，因为本轮没有交互检查当前查询和样本级链接能力；其定位是关联知识库，不是通用样本 metadata 归集器。
- [MicrobeAtlas 官网](https://microbeatlas.org/) 与 [2026 Cell 论文](https://doi.org/10.1016/j.cell.2026.01.021)：当前项目提供全球样本、sample groups、projects、publications 和 taxa 的探索/分析入口；标为 `active_partial`，下载 schema 和单个 accession 查询尚未实际核对。其环境/群落生态数据适合作为背景与二级发现来源，不能替代宿主临床 metadata。
- [Murine Microbiome Database 论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC6920994/)：2019 年资源整理了 14 个项目的 554 个健康小鼠 16S 样本及胃肠部位、基因型、供应商等 metadata；论文给出的旧站 `http://leb.snu.ac.kr/mmdb/` 本轮请求超时。保留为 `unverified`，不据此推断服务已关闭。
- [Human OncoBiome Database 论文](https://doi.org/10.2174/1574893614666190902152727) 和 [H3ABioNet 资源目录](https://microbiome.h3abionet.org/microbiome/resource/)：前者描述人工整理的癌症微生物组数据集及 web interface，后者仍将其列为资源；当前未定位到可确认的第一方服务入口，故保持 `unverified`，只作检索线索。
- [MG-RAST REST API 文档](https://help.mg-rast.org/api.html) 和 [API 论文](https://doi.org/10.1371/journal.pcbi.1004008)：核对到按平台 ID、metadata、function 或 taxonomy 查询，以及 project/sample/metagenome metadata 对象；公开数据不需要 key，私有数据需要授权。补齐目录的 API、论文、认证方式和 platform ID 类型，仍不将其描述为任意 SRA ID 的解析器。
- [Qiita 2026.01 官方文档](https://qiita.microbio.me/static/doc/html/index.html) 与 [2018 论文](https://doi.org/10.1038/s41592-018-0141-9)：确认 biological sample information 与 preparation information 分开，公开 study 可下载样本 metadata；通用 study/sample REST 端点在文档中仍标注为内部 API、计划对普通用户开放。将当前站点、论文和访问边界同步到资源卡。
- [GMrepo v3 论文](https://doi.org/10.1093/nar/gkaf1190)：新论文说明可下载整理后的 sample metadata、taxonomic profiles 和 microbial markers。最初因官方门户无法直接读取而暂留 `active_partial`；随后核对 [官方 help/download](https://gmrepo.humangut.info/help) 与 [run/sample 使用说明](https://evolgeniusteam.github.io/gmrepodocumentation/usage/findrunandsample/)，确认文档描述了按 Run/Sample ID 搜索和项目/run 下载，故更新为 `active_verified`。本轮仍未实测下载文件或逐 accession crosswalk。
- [PRIME 官方帮助页](https://primedb.sjtu.edu.cn/help) 与 [2026 NAR 论文](https://doi.org/10.1093/nar/gkaf1057)：确认按 metadata 浏览/筛选并下载子集，论文报告支持 REST API 和 R package；更新了当前论文 DOI 与帮助链接。该资源仍只覆盖入选的人类 16S 项目，Run/sample 单位及逐项目 archive crosswalk 需保留。

这一轮在原目录上完成 NIBN JMD、gutMDisorder、MicrobeAtlas 等候选核验；当时快照为 49 条：17 `active_verified`、12 `active_partial`、20 `unverified`；资源类别为 8 archive、27 curated_dataset、2 literature_supplement、7 microbial_knowledgebase、5 microbiome_platform。该数字为阶段快照，后续 JGI/NMDC/dbGaP 补录已另行计入当前统计。

### 注册库和大型数据平台补充发现（2026-11-10）

这一轮围绕公开项目/样本 metadata 和宿主表型访问路径，又核对了 NCBI、NMDC 与 JGI 官方目录。代表性检索式包括：`site:ncbi.nlm.nih.gov/gap dbGaP controlled phenotype sample mapping`、`site:microbiomedata.org NMDC data portal API microbiome metadata`、`site:gold.jgi.doe.gov GOLD studies biosamples metadata`、`site:img.jgi.doe.gov IMG/M metagenome metadata`、`site:data.jgi.doe.gov JGI Data Portal API search metadata`。这些来源不是互相替代的数据库，而是分别负责受控人类表型、环境组学、项目登记、功能注释和数据文件检索：

- [dbGaP 官方概览](https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/about.html) 与 [提交指南](https://www.ncbi.nlm.nih.gov/gap/docs/submissionguide/)：公开层包含 study summaries、变量说明和文件文档；个体级 phenotype/genotype 受研究级 DAC 控制。提交指南明确列出 Subject Sample Mapping (SSM) 文件。新增为 Core `archive`，并建立 [详情卡](resources/dbgap.md)。
- [NMDC 官方主页](https://microbiomedata.org/)、[Portal guide](https://docs.microbiomedata.org/howto_guides/portal_guide/) 和 [Runtime API](https://api.microbiomedata.org/)：可查 studies、biosamples、data objects 和处理结果；支持环境多组学，官方 FAQ 明确当前不支持 human microbiome data。Data Portal 下载使用 ORCID 登录，数据采用 CC BY 4.0。新增为 Core 平台、API 工具和 [详情卡](resources/nmdc.md)。
- [GOLD 当前官网](https://gold.jgi.doe.gov/) 与 [v10 论文](https://doi.org/10.1093/nar/gkae1000)：当前 release v10 具有 Study、Biosample、Sequencing Project 和 Analysis Project 浏览/metadata search；IMG/M 以 GOLD metadata 为来源。新增 GOLD 为 Extended curated resource。
- [IMG/M 官网](https://img.jgi.doe.gov/) 和 [JGI portals 目录](https://jgi.doe.gov/analyze-data/jgi-portals)：IMG/M 聚焦公开微生物基因组/宏基因组的比较分析和功能注释；sample metadata 来自 GOLD。作为 Extended 分析平台列入，当前交互查询尚未实测。
- [JGI Data Portal](https://data.jgi.doe.gov/) 与 [API 文档](https://files.jgi.doe.gov/apidoc/)：新版门户于 2026 年取代 sunset 的 JGI Genome Portal；可搜索公共文件 metadata 并通过 API、CLI、Globus 或网页下载。API 文档要求登录；archive 中的文件可能要排队恢复。新增为 Extended 平台和 API 工具。

### 全球环境、宿主相关参考目录与样本查询平台补充发现（2026-11-10）

本轮为资源目录补查环境标签、海洋多组学、专题宿主参考目录及按样本 metadata 查询的数据库。代表性检索式包括：`SPIRE sample metadata microntology ENA publication`、`Ocean-M multiomics sample search environmental metadata`、`MRGM mouse gut microbial genome catalog`、`MOMD mouse oral taxa database`、`HRGM2 41 countries metagenome genomes`、`MicrobiomeDB sample metadata MIxS release 37`。

- [SPIRE FAQ](https://spire.embl.de/faqs)、[下载页](https://spire.embl.de/downloads) 和 [论文](https://doi.org/10.1093/nar/gkad943)：首版研究报告 99,146 个 shotgun samples/739 studies；样本上下文综合 ENA、可用的 IMG/M metadata 和匹配论文，并以 92 项 microntology 人工标注。适合样本来源/环境检索和基因组目录，不保证逐样本 host phenotype。
- [Ocean-M 官网](https://om.biocloud.net/) 与 [论文](https://doi.org/10.1093/nar/gkaf1098)：提供 Sample Search 入口、海洋环境 metadata、多组学数据和 MAG/功能/互作模块。论文给出 54,083 个高质量 MAG，官网当前列出约 57,288 个 dataset。定位为海洋环境数据发现，不用于人体临床信息。
- [MRGM 官网](https://www.decodebiome.org/MRGM/) 与 [论文](https://doi.org/10.1080/19490976.2024.2393791)：42,245 个小鼠肠道非冗余微生物基因组、1,524 个物种，并提供 Kraken2/MetaPhlAn 库；它是小鼠菌群参考，不是动物实验 phenotype archive。
- [MOMD 官网](https://www.momd.org/) 与 [论文](https://doi.org/10.1128/mSystems.01222-20)：205 个 Mouse Oral Taxa、16S 参考、draft genomes、注释和 BLAST 工具；用于小鼠口腔菌群分类/参考序列，不提供一般性的受试动物 sample crosswalk。
- [HRGM2 官网](https://www.decodebiome.org/HRGM/) 与 [论文](https://doi.org/10.1038/s41564-025-02206-1)：基于 41 个国家、18,111 个 WMS 样本建立 155,211 个近完整基因组和 4,824 个物种；官网提供下载并标示 CC BY 4.0。国家覆盖是目录构建来源信息，不等于完整的参与者人口学 metadata。
- [MicrobiomeDB About](https://microbiomedb.org/mbio/app/about)、[release 37 公告](https://microbiomedb.org/mbio/app/static-content/MicrobiomeDB/news.html)、[论文](https://doi.org/10.1093/nar/gkx1027)：样本描述映射 MIxS/custom ontology 并支持 metadata query；2024 年 release 公告称增加 93 项 shotgun studies（>22,000 samples）。当前 app 研究表初始化失败，更新为 `active_partial` 并保留 UI/API 待核状态。

以上 5 个新资源和 MicrobiomeDB 补核后，目录状态由上一快照 54 条更新至 59 条；分类及详情卡统计见下方当前快照。

### 2026 NAR Database Issue 专题筛查（2026-11-10）

查看了 [NAR 2026 Database Issue 总览](https://doi.org/10.1093/nar/gkaf1427) 和当年 advance articles。issue 总览报告共 182 篇数据库论文（84 个新库、86 个既有库更新、12 篇近期在其他位置发表的数据库）；代表性检索词包括 `microbiome`、`metagenome`、`microbial`、`host phenotype`、`sample metadata`、`virome`、`pangenome`。按本项目范围，筛出四项值得入目录的专题资源：

- [ResMicroDb](https://resmicrodb.cncb.ac.cn/)：直接提供人体呼吸道样本/run、项目、10 个采样位点、146 个 phenotype 和 32 个手工整理 metadata factors；文档还列出年龄、sex、BMI、抗生素和 time point 等字段及 metadata/profile 下载。[NAR 论文](https://doi.org/10.1093/nar/gkaf1194)。作为 Core curated dataset 入库，交互式单 accession lookup 仍待实测。
- [gutMSNP](https://bio-computing.hrbmu.edu.cn/gutMSNP/)：按 21 种 human gut host phenotypes 组织菌群 SNP 和参考基因组，study context 包括 project accession、PMID、sample source、DO term、platform 和 count；疾病分层属于队列/组别信息，不等同每个 accession 的个体临床标签。[NAR 论文](https://doi.org/10.1093/nar/gkaf1205)。
- [VIRE](https://vire.embl.de/)：从 >100,000 个公开 metagenome 构建 >1.7M viral genomes，并与 SPIRE、MetaLog 链接同来源样本的 MAG 和环境/临床上下文；数据为 CC BY-SA 4.0。[NAR 论文](https://doi.org/10.1093/nar/gkaf1225)。
- [PanGBank](https://pangbank.genoscope.cns.fr/)：面向 >4,600 个原核生物物种、>393,000 个 genome 的预计算 pangenome 数据库，并提供 REST API/CLI；作为比较基因组参考纳入，但 relevance 标为 indirect，因为不含个体宿主样本表。[NAR 论文](https://doi.org/10.1093/nar/gkag948)。

同一筛查中出现的 GutBiomeDB、GMrepo、gutMDisorder、Metalog、gcMeta 等已有资源与既有条目比对后未重复登记；一般基因组/疾病库若缺少微生物组数据或样本/环境关联，则不因出现在 NAR issue 就自动纳入。

### 注册库和工具目录交叉检索（2026-11-10）

- **re3data：** 按 `microbiome`、`metagenome`、`microbial strain` 等词检索官方 repository entries；找到并交叉确认 MGnify、MG-RAST、NMDC、OAGR、BacDive、StrainInfo、RDP 和 Ensembl Bacteria 等记录。已有资源只补充发现来源，不重复建行。OAGR 初检时仅确认了历史范围；随后 Research Data Australia/Adelaide University 目录确认了其古代人类 genome/microbiome 数据和 provenance。进一步回查发现 [re3data 记录](https://www.re3data.org/repository/r3d100011632)明确标注 OAGR 自 2022 年离线，原始 landing page 亦不可访问，因此现更新为 `legacy`；其 [Research Data Australia DOI 目录记录](https://researchdata.edu.au/online-ancient-genome-repository/1604205)保留为历史数据发现入口，不代表 repository 当前运行。RDP 条目提示服务已于 2023 年 offline，Ensembl Bacteria 条目标记 2026-06 closed；两者未列入当时 65 项微生物组目录，后续如纳入应按 Legacy 处理。re3data 提供[月度 XML 全量导出](https://www.re3data.org/data)和 [v4.0 API](https://www.re3data.org/api/doc/)，可作为后续机器化全量候选抽取入口。
- **bio.tools（本节为稍早的网页检索快照，已由后续机器查询补充）：** 官网 API 文档确认 `GET /api/tool/` 支持分页、全文 `q` 和属性过滤；初始浏览器检索没有读取 API 响应，因此当时未把搜索摘要视为完整结果。后续完成的 JSON API 查询、页数和命中数见下文“注册库 API 能力核实与剩余工作”。
- **FAIRsharing：** 对 microbiome database、metagenome repository 的站点索引检索未找到可直接核验的新资源记录；官方页面由 JavaScript 渲染，API 文档页在当前读取器中无法显示内容。该来源尚未完成实际 API/交互式检索，不能算“已穷尽”。
- **菌株/古代样本边界：** re3data 还收录了用于菌株 identity / culture deposits 的 StrainInfo，以及微生物 16S/菌株知识库。这些不含宿主人群样本表的资源不自动晋升为核心；BacDive 因 strain accession、isolation source、sequence information 可辅助微生物数据解释而纳入 Extended。OAGR 因 Adelaide University/Research Data Australia 保留 DOI 目录及 provenance 描述而列入历史入口；repository 已标记离线，不能假设旧文件仍可直接获取。

依据 [目录状态定义](../catalog/schema.md)，已将 SPIRE、Ocean-M、MRGM、MOMD、HRGM2、ResMicroDb、gutMSNP、VIRE、PanGBank、BacDive 十项从 `active_partial` 提升为 `active_verified`：它们的官方页面/文档确认至少一项 browse/search/download/API 能力。该状态确认的是资源核心入口，不表示已对每个 accession 做端到端映射；相关限制仍保留在资源卡和 CSV notes。MicrobiomeDB 的当前研究表初始化失败，继续留在 `active_partial`。
Qiita 的 2026.01 官方指南确认公开 study 可下载 sample information 文件，PRIME 官方下载页列出 metadata 和 abundance CSV，gutMDisorder 官方浏览页和 release log 确认 v3.0 入口仍在运行；这三项也据此从 `active_partial` 调整为 `active_verified`。Qiita 通用 study/sample REST API 仍标注为 internal/planned；gutMDisorder 仍是关联知识库而非 BioSample crosswalk。

### 官方下载和平台查询能力补核（2026-11-10）

- **Human Microbiome Compendium：** 论文确认其原始完整集合为 168,464 个样本、482 个 BioProjects，并区分用于大部分分析的过滤子集；当前 [Zenodo 记录](https://zenodo.org/records/15122187)明确列出 `sample_metadata.tsv`、project/taxonomy 等可下载文件。资源状态更新为 `active_verified`，含义是可确认数据下载记录，不是实时 accession 查询器。
- **GIMICA：** 官方 [Full Data Download](https://gimica.idrblab.net/ttd/full-data-download)列出宿主遗传/免疫因子影响的 microbiota 数据，以及 microbe、host genetic factor、immune factor、disease 数据文件。页面显示最后更新为 2020-11-20 且 All rights reserved。状态更新为 `active_verified`（下载入口确认），同时明确其内容陈旧、许可受限、属于关联知识库而非样本级 metadata archive。
- **GMrepo v3：** 官方文档描述 Run/Sample ID 搜索、项目/run 查询与下载；v3 论文报告 curated sample metadata、taxonomy profiles 和 microbial marker 下载。状态更新为 `active_verified`，但主站交互与逐 ID 映射仍未直接测试。
- **Metalog：** 2026 NAR 论文详细说明按 metadata 字段浏览/过滤、交互式地图、疾病/药物/生态分类树，以及全库或单 study 下载，并记录与 publications/sequence records 的链接。当前网页触发 anti-bot 拒绝，但论文足以确认核心浏览/下载能力；状态更新为 `active_verified`，实时页面与具体 ID crosswalk 未实测。
- **Meta2DB：** [Zenodo v1 记录](https://zenodo.org/records/17315984)明确列出 metadata CSV、字段说明、taxonomy profiles 与 feature data，报告 13,897 samples/84 studies/23 disease states/34 geographical locations。状态更新为 `active_verified`；该整理库的许可字段未能从记录页面确认，已保持未知。
- **gutDBase：** 2026 NAR 原始论文确认按疾病/数据类型浏览、跨研究差异表达/差异微生物查询及 processed profile/结果下载。状态更新为 `active_verified`；样本 ID crosswalk 与许可仍待单独检查，且其范围为聚焦肠道疾病的多组学数据。
- **gutMGene v2.0：** NAR 2025 论文说明用户可浏览、搜索并检索微生物—代谢物—宿主基因关联及证据详情。状态更新为 `active_verified`；它属于关联知识库而非测序样本 metadata 库，且页面声明 All rights reserved。
- **MicrobeAtlas：** 官方 Sample Groups 页面显示探索与下载入口；结合 2026 Cell 论文确认样本、项目、publication 和 taxonomy context。状态更新为 `active_verified`；完整下载 schema 和逐 accession 查询未实测。
- **IMG/M：** 官方 help 页面列出 genome/metagenome search，并链接 sequence/annotation 和 bulk dataset download；同时说明 metadata 来源 GOLD。状态更新为 `active_verified`；数据使用条款和具体记录访问条件需按数据集检查。
- **mBodyMap：** 2022 NAR 论文确认 22 个身体位点、56 种疾病、136 个项目，并详细说明可按身体位点/疾病浏览以及下载手工整理的 project 与 sample/run metadata；字段涵盖年龄、性别、国家、BMI 和疾病。状态更新为 `active_verified`；论文中的 63,148 runs 是历史快照，现行数量及 accession crosswalk 未重测。
- **NIBN JMD：** 官方公开版入口展示可选样本 ID、年龄、性别、采样月份及测序类型；官方数据库说明给出 2,273 个公开样本/2,068 名参与者，并说明饮食/营养数据可见范围及需账户登录（2026-02-05 起）。状态更新为 `active_verified`；全量样本需注册，详细 phenotype 部分为合作/伦理审批访问，NIBN ID 与 INSDC ID 仍需 crosswalk。

### 公共 API 端点抽样核验（2026-11-10）

- **MG-RAST：** 对已公开的 [metagenome API 记录](https://api.mg-rast.org/1/metagenome/mgm4440026.3?verbosity=full)发出只读 GET 请求，HTTP 200 返回包含 metagenome、关联 sample 与 metadata 的 JSON。另一个公开搜索条件返回 HTTP 200 但 `total_count=0`，说明可确认记录查询端点工作，但尚不能据此保证搜索召回或任意外部 accession 的映射。资源状态调整为 `active_verified`，卡片和 CSV 保留这一限定。
- **Disbiome：** 按[官方导出说明](https://disbiome.ugent.be/export)访问公开 `/experiment` 与 `/disease` JSON endpoints，均返回 HTTP 200 和记录内容。该结果验证 disease/experiment 关联浏览能力，不是 biological sample 或任意 accession 的解析能力，因此不为样本级 crosswalk 做能力背书。
- 本节仅记录公开、只读的端点抽样，不抓取/复制数据库全集，也不等同于稳定性 SLA 或完整 API 测试。

**上一轮目录快照（2026-11-10，扩展前）：** `resources.csv` 共 69 条：62 `active_verified`、1 `active_partial`、6 `legacy`、0 `unverified`；资源类别为 11 archive、32 curated_dataset、2 literature_supplement、14 microbial_knowledgebase、10 microbiome_platform；详情卡 42 张；`tools.csv` 19 项；专题项目索引 12 条（10 verified、1 unresolved、1 candidate）。

### 当前状态复核与新增的主题发现入口

- 当前 `active_partial` 仅有 MicrobiomeDB：官网说明其样本 metadata 可映射 MIxS/custom ontology，新闻页记录曾有持续 release；但本轮 app 的研究表未成功初始化，需后续复核其当前 query/download 操作。
- 当前 `legacy` 为 Animal Microbiome Database、Murine Microbiome Database、MicrobiomeHD、Human OncoBiome Database、iMicrobe 和 OAGR。前几项分别存在旧门户超时、固定数据集/归档代码、未找到当前第一方服务或访问异常；OAGR 的 re3data 记录标注自 2022 年离线，Adelaide/Research Data Australia 的 DOI 目录记录继续作为历史发现线索。
- **历史资源替代入口复核：** MicrobiomeHD 的 [Zenodo 固定数据记录](https://zenodo.org/records/840333)仍列出 metadata 与 processed outputs，可作为历史 curated dataset 使用；Animal Microbiome Database 和 Murine Microbiome Database 的原始论文说明样本来自 NCBI SRA，但原门户不可用时应从论文中的 accession/补充材料回查原始项目；Human OncoBiome 本轮仍未找到可确认的现行一方下载服务。iMicrobe 旧文档记录 CyVerse Data Commons shared directory 和 FTP 路径，但本轮 Data Commons 只确认应用外壳可访问，未核实目录/文件；不把该路径写成可用镜像。OAGR 保留 Research Data Australia DOI 目录，主仓库按 re3data 记录标为离线。
- 近期补核并纳入分类导航的其他入口包括：NCBI GEO 与 EMBL-EBI BioStudies（研究/样本/metadata 和附件检索）；HumanMetagenomeDB（可访问的 2020 固定版）；AncientMetagenomeDir（古代样本/文库与文章 accession 索引）；动物 metagenome 数据库；HMP DACC；MetaSRA；eHOMD、BugSigDB；African Human Microbiome Portal；MetaHQ 和 MiMeDB 2.0。各自能力和非目标用途已在 CSV notes 与[分类导航](resource-categories.md)中说明。
- 近期工具目录从 8 项扩充到 19 项：新增 `ffq`、`nf-core/fetchngs`、`fastq-dl`、ENA Browser Tools、SRA Explorer、Kingfisher、iSeq、`metatools_ncbi`、`grabseqs`、GEOfastq 和 NCBI SRA Run Selector。新补工具覆盖 GSA/SRA/ENA/DDBJ accession、RunInfo 与批量 metadata 导出、GEO 到 ENA FASTQ、MG-RAST metadata 和 reads 获取。它们读取或整理已有归档/平台记录；不会自动恢复论文或 supplement 中未归档的饮食、生活方式、临床信息或 subject crosswalk。
- `active_verified` 仍是有限证据等级：例如固定快照、近期有更新但许可未清楚、或尚未测试 accession crosswalk 的条目会在备注中标明；不能仅凭状态推断元数据完整度或自动映射能力。

### 注册库 API 能力核实与剩余工作

- **bio.tools：** 官方 API 文档确认 GET `/api/tool/` 支持 `q` 全字段搜索、`page`/`per_page` 分页、属性过滤，并返回 `count`、`next` 和结果列表；可用 `topic`、`operation`、`input/output`、tool type、license 等条件缩小发现范围。[API Reference](https://biotools.readthedocs.io/en/latest/api_reference.html)。本轮通过官方 JSON API 完成 `q=microbiome` 全部分页（268 条、3 页、268 个唯一 ID），并完成 `q=sample metadata`（85 条）及 `q=SRA ENA`（4 条）定向扫描。`q=accession` 返回 1,359 条，但只读取首 100 条，属于候选发现而非完整扫描。检索结果人工筛选后新增 Kingfisher、iSeq、`metatools_ncbi`、`grabseqs` 和 GEOfastq 等工具；总搜索命中数不是可直接纳入目录的工具数。
- **FAIRsharing：** 官方 GraphQL schema 暴露 `allFairsharingRecords`、`searchFairsharingRecords`、`multiTagFilter` 和 `advancedSearch`，可按 query、registry/type/status、subjects/domains/object types、license、access mode 等搜索；查询结果支持 `page`/`perPage`。[Query schema](https://api.fairsharing.org/schema/query.doc.html)、[advanced-search fields](https://api.fairsharing.org/schema/advancedsearchfields.doc.html)。API 使用说明所在的[官方 API 页面](https://fairsharing.org/API_doc)在读取器中只显示 JavaScript 壳；FAIRsharing 的[官方集成说明](https://blog.fairsharing.org/?p=657)称 API 受认证/保护。本轮没有可用 token，故尚未执行完整 GraphQL 查询或分页导出。
- **判定：** bio.tools 已完成代表性关键词查询及 microbiome 查询全分页，但尚未遍历全部工具条目，也未穷尽所有 EDAM 过滤组合。FAIRsharing 仍需获得合规 API 访问后，按 domains/subjects 和关键词跑分页查询并保存结果与去重日志。发现入口与代表性扫描已完成，不等于所有注册条目已穷尽。

细节和可筛选记录见 `catalog/datasets.csv`、`docs/guides/maternal_infant_multisite.md`、`docs/guides/crc_microbiome.md`、`docs/resources/mami.md` 与 `docs/resources/ega.md`。

### 资源扩展检索：专题库、跨生态资源与版本更新（2026-11-10）

本轮按食品/发酵、植物/农业、动物、人体多身体位点、环境/海洋、样本 ID 查询、参考序列/知识库等方向扩展；由 NAR database issue、综述和专题页面互链发现候选，再用官方页面、手册、下载记录和原始论文核对。代表性搜索主题包括 food microbiome databases、crop/rhizosphere metagenome databases、animal microbiome multi-omics、metagenome BioProject environment/host metadata API、vaginal 16S reference database、ocean genome-resolved microbiome repository 和 microbiome sample ID/phenotype search。

- **食品资源：** FoodMicrobionet v5.1.2（[官方维护页](https://web.unibas.it/parente/?page_id=761)）整理食品 bacterial/fungal amplicon，并保留 BioProject/BioSample/Run 和文献关系；FoodMicroDB（[论文](https://doi.org/10.1002/imo2.40)）收录食品 amplicon 项目及 food–organism 关系，强调组成/时间序列；cFMD（[数据仓库](https://github.com/SegataLab/cFMD)）专注 shotgun food metagenomes、functional/taxonomic profiles 和 MAG，官方列最新 v1.3.2（2026-06）。三者不等于人体饮食暴露或 lifestyle metadata。
- **农业与植物：** MicroAgroBiome（[NAR 2026](https://doi.org/10.1093/nar/gkaf1083)）提供 554 个 crop-associated metagenomes、28 种作物及标准化 profiles/MAG/BGC 和 NCBI accession 线索；PLaBAse（[官网](https://plabase.cs.uni-tuebingen.de/pb/plabase.php)）是植物相关菌株、plant sphere、interaction phenotype 和促生性状参考库，不是样本 archive。
- **动物多组学：** AnimalMetaOmics（[NAR 2024](https://doi.org/10.1093/nar/gkad931)）的论文报告动物微生物基因组、metagenome、transcriptome、proteome 和 pangenome 模块；当前门户未能打开，记 active_partial。它与 AnimalMetagenome DB（动物 metagenome 项目/样本元数据）不同。
- **环境项目查询：** Microbiome Datahub（[官方手册](https://mdatahub.org/document/)）支持按环境、host taxon 和关键词筛选 INSD shotgun BioProject，提供 metadata TSV/API 和 genome/MAG 搜索。项目和 genome 记录数不等于 BioSample/参与者数；项目级 context 不下推到单样本。
- **人体平台：** Majorbio HMD/iHMD（[样本浏览](https://microbiome.majorbio.com/hmd/sample)）列出身体位点、country、年龄、性别、health-condition、技术和平台过滤；diet、API 和许可尚未确认。它作为候选发现入口，不替代论文和 archive crosswalk。
- **CNGBdb MDB：** 官方[帮助页](https://db.cngb.org/microbiome/help/)说明按 sample/project ID 或 microorganism 查询、浏览 Project/Sample/Experiment/Run/Assembly，并按 170 多个 phenotype 筛选；官网本轮超时，先记 active_partial。此 MDB 与美国 MicrobiomeDB 不同，名称应带机构区分。
- **海洋资源：** Ocean-M 是多组学海洋平台；Ocean Microbiomics Database (OMDB 2.0) 提供地理样本、MAG、BGC、地图和下载，但官网标记功能开发中，记 active_partial；Marine Metagenomics Portal 聚合 MarRef/MarDB/MarFun/SalDB 等 genome/context 参考库，含环境/宿主、taxonomy、phenotype、pathogenicity、assembly 等信息。三者定位不同。
- **知识库和历史资源：** VagDB（[Zenodo](https://zenodo.org/records/17452627)）是基于 582 种已发表 vaginal bacteria 的 DADA2 16S reference，不含样本表型；ODFM（[论文](https://doi.org/10.1038/s41597-021-00895-x)）和 MicroPhenoDB（[论文](https://doi.org/10.1016/j.gpb.2020.11.001)）的历史服务地址无法访问，按 legacy 保留文献和资源线索。
- **版本更新：** Human Microbiome Compendium 当前 Zenodo 记录为 v1.1.2（2026-08-20），包含 sample metadata、projects 与 profiles；Microbiome Repo 官网报告 R2026.36 / package 1.30.0（2026-11-06），区分 7,385 项 study registry 与 curated catalog 的 5,052 studies/806,054 samples。样本记录数不代表参与者人数。

上一批新增 14 条资源后，目录达到 83 条、56 张详情卡。该数字是前一轮快照；本轮已再新增 8 条，当前统计见下方第二轮记录。

### 第二轮扩展：样本门户、全球项目、biobank 与专项资源（2026-11-10）

本轮按 sample metadata download/API、human gut shotgun atlas、global microbial collection/biobank、animal feed intervention metadata、crop/rhizosphere samples、sample ontology、taxon trait database 继续检索。优先使用第一方门户、官方文档、原始论文和 dbGaP/ENA accession 验证。新增 8 个 resources、8 张资源卡；并新增 Redbiom 工具记录和 EMPO 标准记录。

- **HGMA：** [官方下载页](https://www.microbiomeatlas.org/downloads.php)列 sampleID.csv、abundance、bioproj.csv 和模型文件，Version 2 于 2022-10-25 发布；[论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC11293553/)报告 6,014 个 public human-gut shotgun samples、19 countries、23 diseases，并指出 sample metadata 有 age、gender、BMI、geography。记录为固定版 curated dataset，不混同 MicrobeAtlas/Human Microbiome Compendium。
- **EMP/Redbiom/EMPO：** [EMP data page](https://earthmicrobiome.ucsd.edu/data-and-code/)明确 metadata、observation tables、mapping files 可经 Zenodo、FTP、Qiita 获取，Redbiom 可按 sample metadata/features 搜索；[EMPO 页面](https://earthmicrobiome.ucsd.edu/protocols-and-standards/empo/)定义 empo_0–3 habitat hierarchy。EMP 进资源目录，Redbiom 进工具目录，EMPO 进 standards.csv。
- **GMC：** [项目页面](https://microbiomeconservancy.org/our-work/our-biobanks/)说明 metadata 向 GMC 联系，sequencing data 通过 dbGaP 正式申请；[dbGaP phs002235.v1.p1](https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs002235.v1.p1)确认受控研究入口。官网 overview 与 biobank 子页公开的 collection counts 不一致（2,000+ 与 1,500+），因此未用单个样本数作为可比统计。
- **Microbiota Vault：** [collection page](https://www.microbiotavault.org/deposits-and-resources/)列 1,400+ samples、9 local collections、human/food metadata templates 和部分 ENA/BioSample links；[FAQ](https://www.microbiotavault.org/faq/)确认 depositor 控制和条件性开放。2026 launch-phase paper 对 767 stool、157 fermented-food samples 提供标准化 metadata 和 16S data，记录在资源卡中。
- **HoloFood：** [API 文档](https://docs.holofooddata.org/api.html)明确 samples/animals endpoints 与 archive canonical links；[网站说明](https://docs.holofooddata.org/website.html)说明 treatment search 命中动物 BioSample 中 sampling time/name/description/code/concentration。适合 feed-treatment、animal、derived sample 与 multi-omics 关系发现。
- **AgMicrobiomeBase：** [项目数据页](https://agmicrobiomebase.org/data/)与[2023 年 Cryobank 论文](https://doi.org/10.1186/s43170-023-00190-2)将项目目录与 ENA、BioSamples/MGnify 及 UK crop rhizosphere/bulk-soil samples 相连。由于 dashboard 未渲染、字段筛选/导出能力未核实，保持 active_partial；使用前需核对门户与底层 archive 当前条款。
- **MICROBE Data Portal：** 搜索索引的[官方首页](https://data.microbeproject.eu/)显示 4,353 samples 并给出 API/docs 入口；[官方 GitHub](https://github.com/EBI-Metagenomics/microbe-data-portal)说明 Django API 缓存 ENA、BioSamples、MGnify metadata。当前读取超时，因此只记录项目级入口和待复核状态，不假设 endpoint schema 已验证。
- **The Microbe Directory：** [2025 年论文](https://doi.org/10.1093/database/baaf060)说明其为 cross-domain taxa feature/ecology knowledgebase，近 18,000 species、42 traits；网站当前不可访问，故记 active_partial，并注明不是 sample/host phenotype database。

本批新增资源中 HGMA、EMP、GMC、HoloFood 的官方数据/检索路线已由下载页、研究论文或 controlled-access record 支持，记 active_verified；MVI、MICROBE portal、AgMicrobiomeBase、The Microbe Directory 因访问许可/页面/字段级能力尚需核实，记 active_partial。

## 后续扩展检索记录

### 第三轮交叉检索：样本 metadata manifest、ID indirection 和 paired multi-omics（2026-11-10）

- **HMBR：** 官方 browse guide 证实 sample facets/advanced search，可按 study、assay preparation、race、smoking history、gender、age category 检索，并查看 file facets。其 file manifest 样例提供 file ID、MD5、size、URL、sample ID；sample metadata manifest 示例含 subject/sample accession、PMID、gender、disease、race、BMI、age category、body site、sample type、timepoint、smoking、alcohol、medication 等变量。明确区分 file 与 sample，并说明一个 sample 可关联多个 file。[browse guide](https://microbiome-bioactives.org/browse-portal/index.html) · [manifest documentation](https://microbiome-bioactives.org/download-file-manifest/index.html)。状态 `active_verified`，但只代表可核实到 portal/manifest 能力，实际每个字段的完整度、archive crosswalk 和 access type 需逐 study 查看。
- **HMBR Portal Client：** 官方使用页描述 manifest 输入、HTTP/FTP/S3 等下载端点和 checksum 验证；代码位于 IGS GitHub。[文档](https://microbiome-bioactives.org/download-portal-client/index.html) · [代码](https://github.com/IGS/portal_client)。列为下载工具，不是 metadata 搜索 API。
- **MetaSUB-metadata / `map_collate`：** 官方公开仓库列出源 spreadsheets、cleaning script 和 mapping 表。README 报告 1,301 个 sample/FASTQ 的生成 metadata，并明确承认字段不完整；还提供丢失 barcode leading zero、错列、非标准缺失值等清理案例。`map_collate` 旨在按多层来源 ID 关系尽力连接记录，因此适合作为 crosswalk/provenance 设计案例，不是通用 accession 工具。[repository README](https://github.com/MetaSUB/MetaSUB-metadata) · [ID/storage conventions](https://metasub-bioinformatics.readthedocs.io/en/latest/data_storage.html) · [2021 paper](https://doi.org/10.1016/j.cell.2021.05.002)。因字段不全、数据包访问不同，资源标为 `active_partial`。
- **HuMMANet：** 公开 Zenodo 数据记录、Bioconductor/GitHub R 包和 2026 bioRxiv preprint 报告 46 paired gut microbiome–metabolome studies、59 study-units、14,405 samples，并提供 matched metadata 与研究级多组学 modalities；原始资源不一定由该项目统一重新分发。作为专题数据集记录为 `active_verified`，同时保留 preprint 状态与逐 study 权限限制。[Zenodo](https://doi.org/10.5281/zenodo.22053943) · [Bioconductor](https://bioconductor.org/packages/HuMMANet) · [GitHub](https://github.com/ShivangiV-IIITD/HuMMANet) · [preprint](https://doi.org/10.64898/2026.08.24.746727)。
- **第三轮结束时快照：** `resources.csv` 94 条：76 `active_verified`、10 `active_partial`、8 `legacy`；资源类型分别 11 archive、45 curated_dataset、2 literature_supplement、20 microbial_knowledgebase、16 microbiome_platform。重点资源卡 67 张、tools.csv 23 项、standards.csv 6 项。新增 3 个资源与 3 个工具索引项，没有复制外部大体量数据。

### 第四轮扩展：跨仓库疾病数据发现门户（2026-11-10）

- **NIAID Data Ecosystem Discovery Portal：** 官方站点与 FAQ 说明它跨多个感染性/免疫介导疾病及 generalist repositories 索引 datasets、resource catalogs、tools 和 sample records，收录源中包括 MicrobiomeDB。可用关键词/字段检索，下载 CSV/JSON metadata，或调用公开 API；找到候选后需跳转到来源库获取数据。门户声明它不是数据仓库，来源范围有限，metadata 缺失会在门户中继续缺失，搜索也可能命中与 IID/microbiome 无关的记录。[官方首页](https://data.niaid.nih.gov/) · [API 指南](https://data.niaid.nih.gov/knowledge-center/accessing-the-metadata-api) · [FAQ](https://data.niaid.nih.gov/knowledge-center/frequently-asked-questions) · [2026 mSystems resource report](https://doi.org/10.1128/msystems.01270-25)。作为跨仓库发现门户单独建立 `resource_discovery_portal` 类型，不把它误归为 microbiome 专属数据库或 archive。
- **NIAID API：** 官方文档说明可程序化检索 portal 索引的 dataset/resource/tool metadata 并批量导出。作为 API 工具入 `tools.csv`；它不提供底层文件下载，也不绕过 source repository 的 access rules。
- **第四轮结束时快照：** `resources.csv` 95 条：77 `active_verified`、10 `active_partial`、8 `legacy`；资源类型分别 11 archive、45 curated_dataset、2 literature_supplement、20 microbial_knowledgebase、16 microbiome_platform、1 resource_discovery_portal。重点资源卡 68 张、tools.csv 24 项、standards.csv 6 项。新增 1 个资源门户和 1 个 API 目录项，没有复制外部大体量数据。

### 第五轮扩展：2026 NAR 数据库专刊与微生物功能/病毒/病原资源（2026-11-10）

本轮使用 [2026 NAR Database Issue review](https://doi.org/10.1093/nar/gkaf1427) 的新数据库表作为候选索引，再逐项查看资源官网、documentation、原始数据库论文与可用下载页。该综述报告本届专刊含 182 篇数据库论文、NAR 在线目录累计 2,173 个条目；专刊表是跨领域 discovery map，必须筛选 microbiome、metagenome、microbial genome、viral、AMR 等范围，不能直接把所有条目当微生物组数据库。

- **HLRMDB：** 官方页面支持按样本、健康/疾病、采样情境、测序平台和 genome-bin 检索，报告 1,672 个人体长读长/hybrid metagenomes、38 项研究，并连接 taxonomy/function/ARG 与 MAG 结果。官网注明学术使用免费，商业使用需联系项目方。[官网](https://www.inbirg.com/hlrmdb/home) · [下载页](https://www.inbirg.com/hlrmdb/downloads/) · [论文](https://doi.org/10.1093/nar/gkaf1152)。
- **dbCAN-HGM：** 官方页核实 6,031 个代表性 MAG 中的 121,883 个 CAZyme gene clusters，可按 taxonomy、continent、substrate 浏览/下载，并显示不同 diet/disease group 的 read-mapping。该分组不能解释成逐受试者饮食或疾病字段。[官网](https://pro.unl.edu/dbCAN_HGM/) · [论文](https://doi.org/10.1093/nar/gkaf1185)。
- **DOO：** 官方门户/下载页与 NAR 论文报告深海 68 个物种的 multi-omics atlas，包括 metagenomes、transcriptomes、single-cell data、symbionts、genome annotation 和可下载序列/功能注释。它支持深海生态数据发现，而不是人体宿主 metadata 检索。[官网](https://deepoceanomics.org/) · [Download](https://deepoceanomics.org/download.php) · [论文](https://doi.org/10.1093/nar/gkaf1096)。
- **MetaVR：** NAR 论文将其定义为 IMG/VR successor，报告 24,435,662 个 UViGs、分类/host assignment/protein clusters 和 REST API；本轮 portal/API 返回访问错误，标 `active_partial`。[论文](https://doi.org/10.1093/nar/gkaf1283) · [portal](https://www.meta-virome.org/) · [API docs](https://meta-virome.org/api/docs)。
- **metaTraits：** EMBL 官网与论文说明它整合培养来源性状和 genome/MAG predictions，覆盖 2.2M+ genomes、140+ traits，提供 taxonomy/genome 查询、profile annotation、bulk downloads 和无认证 JSON API。官网此时提示 scheduled maintenance，因此资源和 API 均标 `active_partial`。这些 traits 是微生物性状，不是 host phenotype。[官网](https://metatraits.embl.de/) · [docs/API](https://metatraits.embl.de/documentation) · [论文](https://doi.org/10.1093/nar/gkaf1241)。
- **metagRoot：** NAR 论文报告 71,091 个植物根际微生物蛋白家族，来源于 metagenomes、metatranscriptomes 和参考基因组，带生态分类/功能/结构信息及 Zenodo data deposit；门户本轮无法访问，按 `active_partial` 处理。[论文](https://doi.org/10.1093/nar/gkaf862) · [portal](https://www.metagroot.org/) · [data deposit](https://doi.org/10.5281/zenodo.15488157)。
- **MicrobialScope：** 官方首页可用，按 microbial genome accession 搜索跨细菌、古菌、真菌和病毒的 genome/protein/ARG/virulence 等功能注释，并提供 FASTA/metadata/customized download API。[官网](https://microbial.deepomics.org/) · [论文](https://doi.org/10.1093/nar/gkaf1234)。
- **VirJenDB：** 官方 docs 和 NAR 论文说明其整合病毒序列、harmonized metadata、taxonomy，并支持检索/下载及 REST/OpenAPI；字段包括 INSDC、BioSample、BioProject、SRA accession、collection geography/date 与若干 host 变量。样本/host 字段依来源而异，本轮 portal 检查失败，所以标 `active_partial`。[portal](https://virjendb.org/) · [docs/schema](https://doc.virjendb.org/pages/metadata.html) · [API](https://api.virjendb.org/swagger) · [论文](https://doi.org/10.1093/nar/gkaf1224)。
- **AMRnet：** 论文与官方 GitHub 描述限于多种 priority bacterial pathogens 的 genome-derived surveillance：year/country、lineage、AMR markers/predictions、可下载的 isolate-level records/API/周期快照。主应用需 JavaScript，API 未实测，标 `active_partial`。它不是通用 microbiome dataset resource。[dashboard](https://www.amrnet.org/) · [GitHub/API](https://github.com/amrnet/amrnet) · [论文](https://doi.org/10.1093/nar/gkaf1101)。
- **ARKbase 与 IVCDB：** ARKbase 官方站可查看 pathogen reference genome、curated AST、AMR/virulence 等；IVCDB 官网可查 310 iridovirus isolates、地理分布、宿主范围、疫苗/检测与 genome/protein data。两者作为扩展 pathogen knowledgebase 收录，isolate AST/virus-host range 不能当作人体受试者 phenotype。[ARKbase portal](https://datascience.imtech.res.in/anshu/arkbase/) · [ARKbase paper](https://doi.org/10.1093/nar/gkaf1307) · [IVCDB portal](https://www.iridovirus.com/) · [IVCDB paper](https://doi.org/10.1093/nar/gkaf838)。
- **第五轮结束时快照：** `resources.csv` 106 条：83 `active_verified`、15 `active_partial`、8 `legacy`；资源类型分别 11 archive、47 curated_dataset、2 literature_supplement、28 microbial_knowledgebase、17 microbiome_platform、1 resource_discovery_portal。重点资源卡 79 张、tools.csv 28 项、standards.csv 6 项。新增 11 个资源和 4 个 API/数据访问工具索引项；没有复制外部大体量数据。

### 第六轮扩展：metadata 搜索平台、harmonization、基因组背景与代谢模型（2026-11-10）

本轮针对“已有样本 ID 后能否直接补充宿主信息”继续检索，同时区分数据库、检索平台、软件和字段规范。所有条目仍只保留轻量目录与外部链接，不复制外部数据。

- **Celeri Microbiome Studies Explorer：** 官方说明它从 ENA XML 提取人体肠道原始测序项目/样本的 submitter metadata，使用 AI 结构化 host age/sex、疾病、干预、采集日期/来源、host ID、临床字段及 Experiment/Run 关系；不托管 reads。它是本轮最直接相关的二级发现平台，但其官方说明并未表明会系统查文章和 supplement，因此 ENA 未提供的生活方式/饮食或 crosswalk 不能假定可恢复。平台说明称每周更新，但本次可见同步时间为 2026-05-28，且未看到已核实 API。其条款同时禁止镜像/系统性抓取，故仅列链接并标 `active_partial`，后续不可按普通开放 API 批量抓取。[Explorer](https://www.celerilab.com/data) · [字段/处理说明](https://www.celerilab.com/learn-more) · [条款](https://www.celerilab.com/data/license)。
- **curatedMetagenomicData 3 与 OmicsMLRepoR：** cMD 3 继续作为人体 shotgun curated 数据/metadata 基准；论文资源包为 22,588 样本、93 项 dataset，论文分析增加一项 122 样本研究后报告 22,710 个样本、94 个 cohort。OmicsMLRepoR 是 Bioconductor 软件，不是独立的公共样本库；它提供 cMD/cBioPortalData harmonized metadata 下载与 ontology-aware 浏览，支持同义词、大小写不敏感和 ontology descendants 搜索。它适合作为未来字段标准化与浏览参考，但范围限于已整合的数据包。[cMD 3 论文](https://doi.org/10.1038/s41467-025-66888-1) · [OmicsMLRepoR package](https://bioconductor.org/packages/release/bioc/html/OmicsMLRepoR.html) · [官方 Quickstart](https://bioconductor.org/packages/release/bioc/vignettes/OmicsMLRepoR/inst/doc/Quickstart.html) · [harmonization paper](https://doi.org/10.1093/database/baag027)。
- **Microbiome Research Data Toolkit：** 作为 `standards.csv` 的字段采集/回顾 harmonization 规范纳入，而非资源查询数据库。v1.1 提供 REDCap XML、数据字典、guideline 和 codebook，覆盖项目/样本处理、人口学、身高体重、烟酒、药物、运动和饮食；它可为本项目未来输出 schema 设计提供字段参考，但不能回填历史研究未提供的信息。文件级再分发许可未确认。[论文](https://doi.org/10.1093/database/baae062) · [GitHub 文件](https://github.com/h3abionet/h3aphenstds/tree/main/Microbiome%20Toolkit%20v1.1) · [Figshare](https://doi.org/10.25375/uct.24218999.v2)。
- **mOTUs-db 与 mOTUs profiler：** mOTUs-db 提供物种层级 mOTUs、MAG/isolate genomes、功能注释、环境/采样点和关联研究；配套 CLI 可对 reads 做分类 profiling 并按分类 ID 取 genome/annotation。数据库论文报告 124,295 个 species-level units 与约 3.75M genomes。它可给环境和微生物参考背景，但不是 participant-level phenotype 库；新增 resource 与 CLI 工具分列。[数据库](https://motus-db.org/) · [文档](https://motus-tool.org/database/index.html) · [论文](https://doi.org/10.1093/nar/gkae1004)。
- **APOLLO 与 MicroMap：** APOLLO 在 VMH 中提供 247,092 个微生物 genome-scale metabolic reconstructions 及 14,451 个 sample-specific community models；MicroMap 为超过 25 万个模型提供代谢网络可视化，并连接 VMH/COBRA。二者可按身体位点、年龄、疾病分层理解微生物代谢潜力，但不是样本表型搜索工具，模型分层字段不等于每个样本可回收的个体临床或饮食变量。[APOLLO paper](https://doi.org/10.1016/j.cels.2025.101196) · [VMH](https://www.vmh.life/) · [MicroMap paper](https://doi.org/10.1038/s41522-025-00853-0) · [Dataverse](https://dataverse.harvard.edu/dataverse/micromap)。
- **第六轮结束时快照：** `resources.csv` 110 条：86 `active_verified`、16 `active_partial`、8 `legacy`；资源类型分别 11 archive、48 curated_dataset、2 literature_supplement、30 microbial_knowledgebase、18 microbiome_platform、1 resource_discovery_portal。重点资源卡 83 张，`tools.csv` 30 项，`standards.csv` 7 项。新增 4 个资源、2 个工具、1 个字段规范入口，并补充 cMD 3 口径说明。

### 第七轮补充：营养研究发现与 phenotype-rich 16S 数据资源（2026-11-10）

- **Mica：** 新增 INTIMIC metadata portal，面向参与项目中的营养流行病学/肠道菌群观察研究，提供 studies、datasets、variables、harmonization initiatives 和 protocols 的发现入口。官网明确采用 DataSHIELD 进行多研究非披露式分析；个体数据可能保留在研究方 Opal server，并需要申请/合作。它适合从 diet/nutrition 问题发现候选队列，不是任意测序 ID 的解析器，也不表示有开放的逐样本饮食数据。[官方门户](https://mica.mdc-berlin.de/) · [研究列表](https://mica.mdc-berlin.de/individual-studies) · [harmonization protocols](https://mica.mdc-berlin.de/harmonized-datasets) · [INTIMIC paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC9100002/)。
- **PRIME：** 对已有资源条目补充当前 NAR paper/官网 Download Center 的明确范围和接口：53,449 个样本记录、111 项人类 16S 研究、93 个身体位点、101 类 phenotype，提供人工整理 sample metadata、统一 taxonomy abundance、REST API v1 和 primeDB R client；页面支持 Project accession/Run ID 定制 abundance 选择。新增 `primedb_client` 工具索引。样本不是参与者计数，README/API 的数据许可声明与特定发布文件的再分发权需分开确认。[NAR paper](https://doi.org/10.1093/nar/gkaf1057) · [Download Center](https://primedb.sjtu.edu.cn/download) · [API](https://primedb.sjtu.edu.cn/api/v1) · [primeDB](https://github.com/reckonzzz/primeDB) · [Zenodo](https://doi.org/10.5281/zenodo.15711237)。
- **GutBiomeDB：** 复核其 2026 NAR 新文，确认 168,464 个肠道 16S sample records、482 个 BioProjects、疾病/生命阶段/性别/地理 metadata、统一 taxonomy matrix、Zenodo 数据和 46 个公开 REST endpoint。文中指出样本级疾病、年龄、性别在资源内仍有缺失；平台主站为 JavaScript 应用，API endpoints 数量和源代码不是逐 endpoint live audit。这个例子进一步说明大型 curated compendium 仍不能保证完整 phenotype 覆盖。[NAR paper](https://doi.org/10.1093/nar/gkag1125) · [GutBiomeDB](https://gutbiomedb.online/) · [Zenodo](https://zenodo.org/records/22952317)。
- **Human Phenotype Project diet–microbiome：** 新增到 `datasets.csv` 和饮食检索指南。2026 Nature Medicine 论文报告 10,068 名参与者、app-based diet logs 与 shotgun metagenomics；论文数据声明指向 EGA `EGAS00001007204` 和 HPP data-access page。EGA 当前 Study 页面关联的 `EGAD00001010925` 展示 7,190 个粪便宏基因组样本。论文分析人数与 EGA 当前样本数不是相同计数，数据 freeze、子集和 sample crosswalk 尚未核对，所以条目标为 `unresolved`；不把代码归档当作数据公开，也不推断 diet log 可直接下载。[论文](https://doi.org/10.1038/s41591-026-04312-x) · [EGA study](https://www.ega-archive.org/studies/EGAS00001007204) · [HPP data access](https://humanphenotypeproject.org/data-access) · [analysis code](https://github.com/TmrSegev/diet-microbiome)。
- **第七轮补充后快照：** `resources.csv` 111 条：87 `active_verified`、16 `active_partial`、8 `legacy`；资源类型为 11 archive、48 curated_dataset、2 literature_supplement、30 microbial_knowledgebase、19 microbiome_platform、1 resource_discovery_portal。资源卡 84 张、`tools.csv` 31 项、`standards.csv` 7 项。`datasets.csv` 增至 13 条（10 verified、2 unresolved、1 candidate），新增 HPP 饮食—菌群候选。没有复制外部数据库或数据文件。

### 第八轮补充：健康研究发现入口与 dietary metadata schema（2026-11-10）

- **NFDI4Health Health Study Hub：** 新增为跨领域 `resource_discovery_portal`，不是微生物组专库。官方说明其汇总 DRKS、ClinicalTrials.gov、WHO ICTRP 等研究 metadata，并允许网页/API 查询；部分记录能探索到 variables/items 和数据访问条件。对本项目的价值是从德国营养流行病学/健康研究中找队列，再核验菌群 assay、测序 accession 和样本 crosswalk。[portal/API](https://health-study-hub.de/api/docs/) · [Hub overview](https://www.nfdi4health.de/en/service/health-study-hub.html)。
- **NFDI4Health Metadata Schema：** 新增 standards.csv；官方 schema v3.3 包含研究设计、人群、数据访问、dietary assessment instruments 和 record-linkage 等模块，可作为健康/营养字段描述规范参考，不含具体 study/sample values。[官方 schema](https://www.nfdi4health.de/en/service/metadata-schema.html) · [machine-readable schema](https://health-study-hub.de/api/MDS_latest_full.json)。
- **API 工具：** 将 Health Study Hub REST API 单独记入 tools.csv。官方 OpenAPI 文档描述 `POST /api/resources/` 搜索 published resources；本次未执行 API 请求，工具状态标 `active_partial`。API 结果是 portal metadata，不是底层数据文件或自动 BioSample crosswalk。
- **第八轮补充后快照：** `resources.csv` 112 条：88 `active_verified`、16 `active_partial`、8 `legacy`；类型为 11 archive、48 curated_dataset、2 literature_supplement、30 microbial_knowledgebase、19 microbiome_platform、2 resource_discovery_portal。资源卡 85 张，`tools.csv` 32 项，`standards.csv` 8 项；`datasets.csv` 13 条（10 verified、2 unresolved、1 candidate）。

## 第八轮后待续项（历史记录）

1. 继续尽可能广地发现数据库、专题数据集与工具：112 条是多来源支持的可追溯目录，并非穷尽；2026 NAR Database Issue 汇总表已按主题筛查并纳入可确认的微生物组/病毒/病原候选；bio.tools 已完成 microbiome 全分页及 accession/sample-metadata 定向查询但未全库遍历；FAIRsharing 的认证 GraphQL 扫描仍未完成。
2. 目前有 16 条 `active_partial` 待优先核查：MicrobiomeDB、CNGBdb MDB、AnimalMetaOmics、PLaBAse、OMDB、Microbiota Vault、MICROBE Data Portal、AgMicrobiomeBase、The Microbe Directory、MetaSUB Reproducible Metadata、MetaVR、metaTraits、metagRoot、VirJenDB、AMRnet、Celeri。8 条 `legacy` 已做首轮历史入口/替代路线复核；旧文件路径若复用仍需逐项查证。
3. 逐链接在线状态检查应在发布前或定期更新时执行；当前为内部路径检查和重点入口抽样，不代表全部 112 项资源链接持续在线。
4. 在 FAIRsharing 合规 API 查询、扩大注册库定向发现、MicrobiomeDB 与 partial 资源状态判定完成后，再评估冻结第一阶段目录；未来按 accession 自动回收论文与补充材料 metadata 属于后续自研流程，测试样本由用户后续提供。

### 第九轮续查与首版验收：部分资源状态和目录冻结（2026-11-11）

- **PLaBAse：** 官方查询页显示 5,565 个植物相关细菌菌株，支持 taxonomy、plant-sphere 和 host-phenotype 过滤。确认公开检索入口可用；批量下载仍在开发中，因此只确认其浏览/查询核心能力，不暗示全量数据可下载。[官方查询页](https://plabase.cs.uni-tuebingen.de/pb/plaba_db.php) · [下载页](https://plabase.cs.uni-tuebingen.de/pb/download.php)。
- **Ocean Microbiomics Database（OMDB）：** 当前官方介绍页报告 12,347 个带地理坐标样本、274,282 个重建基因组、31,058 个 prokaryotic species-level units，并说明可搜索序列/BGC、浏览采样地图和下载 supporting data；列明 CC BY 4.0。它与 CNGBdb 的 Ocean-M 是不同资源。本轮不下载数据、不做 accession join。[当前介绍页](https://omdb.microbiomics.io/about?repo_id=ocean) · [数据页](https://omdb.microbiomics.io/repository/ocean/)。
- **Microbiota Vault：** 官方目录列出 9 个本地 collection、1,400+ 样本，含样本类别、部分 ENA/BioSample 链接、人类/食品最小 metadata 模板和 SOP。目录/元数据参考功能可用，但实体样本、序列开放范围由 local depositor 管理，部分资料需申请。[官方目录](https://www.microbiotavault.org/deposits-and-resources/) · [FAQ](https://www.microbiotavault.org/faq/)。
- **VirJenDB：** 官网搜索索引识别当前 release v1.1.3；官方 metadata schema 页面列有 INSDC、BioSample、BioProject、SRA、采样日期/地点和部分 host fields，并提供字段映射下载。Swagger 无法由本轮浏览工具解析，未调用 API 或逐 ID 验证；host 字段因上游来源可缺失或不统一。[官网](https://virjendb.org/) · [metadata schema](https://doc.virjendb.org/pages/metadata.html) · [API Swagger](https://api.virjendb.org/swagger)。
- **AMRnet：** 官方文档确认 organism 页面可免注册下载 TSV、公开 S3 提供周更 CSV 快照；REST API 已转到 `api.amrnet.org` 并需免费申请 API key，旧 MongoDB Atlas Data API 文档已被替代。本轮没有下载快照或请求 API。[数据访问说明](https://amrnet.readthedocs.io/en/latest/data.html) · [API docs](https://api.amrnet.org/api-docs)。
- **Celeri 与 The Microbe Directory：** Celeri 官网本轮仍显示 “No update available” 和 loading table；此前页面能看到的最近同步日期为 2026-05-28，且缺少经核实的公开 API、条款限制系统抓取，维持 `active_partial`。The Microbe Directory 官网此轮仍不可访问，维持 `active_partial`，其论文与 GitHub 数据入口保留为后续替代核查路线。
- **状态修订与边界：** 上述前五项状态从 `active_partial` 调整为 `active_verified`，仅代表当前官方页面/文档确认了至少一项核心查询、目录或下载入口；不表示本项目已实际调用 API、下载文件、确认全字段覆盖或完成 accession-to-sample crosswalk。目录快照更新为 116 条（97 `active_verified`、11 `active_partial`、8 `legacy`、0 `unverified`），89 张资源卡、37 项工具、8 项标准、13 项专题候选。完整检索式、时间戳、修改清单和未完成边界见[检索与资源更新记录](research_update_log.md)。

第一阶段首版按计划验收完成。注册库认证接口、更宽关键词搜索和各站点变化属于持续维护项；第二阶段样本 ID 到论文/补充材料 metadata 的自动检索尚未启动。
