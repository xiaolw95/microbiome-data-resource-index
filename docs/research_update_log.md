# 检索与资源更新记录

本日志按追加方式记录每轮外部检索与目录维护。所有时间使用中国标准时间（Asia/Shanghai，UTC+08:00）；资源本身的核查日期仍写在相应 CSV 行和资源卡中。此日志记录**何时查了什么、依据哪些来源、改了哪些文件、还留下什么不确定性**，便于后续滚动更新和追溯。

## 更新规则

- 每轮开始和结束各写一条精确时间戳；若检索跨越多次会话，按日期拆分。
- 保存代表性查询式、官方/原始来源链接、候选新增/状态变化、文件清单和未解决事项。
- 资源主页可访问、文献声称有 API、以及逐 accession 端到端验证是不同证据等级；日志中明确写出做到哪一步。
- 不覆盖历史条目。若更正旧结论，追加更正记录并链接到原记录。
- `catalog/resources.csv`、`catalog/tools.csv`、`catalog/standards.csv`、`catalog/datasets.csv` 与本日志互相补充；本日志不替代机器可筛选目录。
- 没有实际调用某个 API、下载文件或逐 ID 映射时，不能写成已测试。

## 2026-11-11 — 第九轮：注册目录与当前资源版本复核

**检索开始：** 2026-11-11 09:29:39 +08:00  
**检索结束：** 2026-11-11 09:32:15 +08:00（本条整理于同一检索窗口）  
**时间戳更正：** 上述两次时钟读取发生在本轮搜索已经开始之后，不能作为精确检索起止时间；本轮实际开始时刻未记录。后续条目按“可确认时间”记录，避免把过程中的时钟读取误标为边界时间。
**范围：** 资源发现注册库、Microbiome Repo 最新 release、MiCoDa v2、MICROBE Data Portal、MGnify API 版本，以及将资源门户与真实数据仓库区分的导航方式。

### 代表性检索式

- `microbiome databases resource database index 2026 microbiome resources catalog NAR database issue metagenome metadata`
- `FAIRsharing API microbiome database records API documentation GraphQL`
- `re3data API search microbiome data repository REST API documentation`
- `bio.tools API search microbiome metagenomics metadata resources API documentation`
- `site:microbiomerepo.com API documentation samples metadata public microbiome repo 2026`
- `MiCoDa Microbial Community Database official database samples metadata sequencing studies API v2 2024`
- `MICROBE Data Portal API documentation 4353 samples ENA Biosamples MGnify`
- `NAR online molecular biology database collection current website browse database collection`

### 查阅的第一方/原始来源与发现

- [Microbiome Repo 样本浏览器](https://microbiomerepo.com/samples/index.html)、[数据包说明](https://microbiomerepo.com/docs/README.html)、[API 入口](https://microbiomerepo.com/llms/index.html)：官方发布 R2026.36 / data package 1.30.0（2026-11-06），页面报告 5,052 个 curated projects、806,054 个样本记录。其逐字段记录带 archive / supplement / full text / abstract 来源路线与 confidence，并提供证据表；这些是样本记录和证据声明，不是独立参与者数。官方给出静态 JSON/CSV/Parquet 下载入口；本轮只查阅文档，没有下载完整数据包或对 accession 做逐项映射。
- [MiCoDa v2](https://micoda.idiv.de/v2) 与 [About 页面](https://micoda.idiv.de/v2/aboutUs)：全球环境等多生态系统的整理型 16S 数据库，序列区域为 16S V4（约 515–806），样本带 INSDC accession，部分技术 metadata 由研究文献补充。页面版本/collection 计数会变化；本目录不据单个动态数字横向比较资源规模。它不能替代 shotgun archive，也不专门提供人体临床表型。
- [MICROBE Data Portal](https://data.microbeproject.eu/)：当前官方页面可见 4,353 个项目样本、API/文档入口，并链接 ENA、BioSamples、MetaboLights 和 MGnify。该门户专用于 MICROBE 项目；本轮确认官网索引可见，但没有实际调用 API 或审核完整 sample crosswalk，因此维持 `active_partial`。
- [MGnify API 文档](https://docs.mgnify.org/src/docs/api.html)：当前主版本为 API v2，覆盖 studies、samples、runs、biomes、analyses 等；文档说明 v1 已于 2026-06 弃用，关闭时间“不早于”2026-09-01，且 v1 冻结、不含 V6 analyses。目录和工具卡同步记录 API v2，使用旧版脚本时应先迁移并查看实时文档。
- [re3data API 文档](https://www.re3data.org/api/doc)、[关于页](https://www.re3data.org/about)、[数据下载页](https://www.re3data.org/data)：当前 REST API v4.0 提供 repository index/detail，另有在线仓库每日 XML 导出；其记录描述的是**数据仓库本身**（学科、访问方式、标准、认证等），不是仓库里的每个数据集。官方说明元数据 CC0。
- [bio.tools API Quickstart](https://biotools.readthedocs.io/en/latest/api_quickstart.html) 与 [API Reference](https://biotools.readthedocs.io/en/latest/api_reference.html)：公开读取 API 可分页列出工具、全文查询、按属性过滤和读取单条记录；默认每页 50，写入/修改才需要认证。它索引软件、服务和数据库描述，不运行这些工具也不托管它们的测序数据。
- [FAIRsharing 官方文档](https://fairsharing.gitbook.io/fairsharing)、[GraphQL schema](https://api.fairsharing.org/schema/) 与 [FAIRsharing API 文档入口](https://fairsharing.org/API_doc)：其核心是人工策展且互相关联的数据库/仓库、标准和政策登记；内容不等于数据集仓库。站点说明 JSON API 和记录关联/历史，GraphQL schema 可查看；API_doc 本轮对非交互抓取仅显示 JavaScript 壳，未完成可复现的公开批量查询，因此不声称 API 可匿名全量扫描。官网说明内容采用 CC BY-SA 4.0；具体 API 权限仍按官方当前条款确认。
- [NAR Database Issue 总览](https://doi.org/10.1093/nar/gkaf1427) 与 [NAR 专刊目录](https://academic.oup.com/nar/pages/special-collections)：NAR 年度专刊与 Molecular Biology Database Collection 是高价值数据库论文发现渠道。2026 总览报告 Collection 2,173 个数据库条目，并在过去一年复核 899 条、增加 96 项、移除 319 个已停用 URL；这一入口跨生物学领域，不是 microbiome-only 目录，且不能将论文入选等同于资源当前端到端可用。

### 本轮目录/文档改动

- 新建 [资源发现注册库指南](guides/resource_discovery_indexes.md)，解释 FAIRsharing、re3data、bio.tools、NAR Collection、NIAID 和 NFDI4Health 各自索引什么对象、如何查询、何时应跳回原始数据库。
- 新建本时间日志，并在 README、资源导航和维护规范中加入入口。
- 更新 Microbiome Repo、MiCoDa、MICROBE Data Portal、MGnify 的官方版本说明和核查日期；为 Microbiome Repo 与 MGnify 增加工具/接口目录行。
- 将 FAIRsharing、re3data、bio.tools、NAR Collection 作为“二级发现索引”加入资源目录，避免其与原始 reads archive 或 curated sample dataset 混淆。

### 未完成和边界

- FAIRsharing 的 API 查询/分页和数据库学科筛选没有在本轮执行；因此不把搜索注册库的候选数记为完整扫描。
- bio.tools 此轮复核官方 REST 文档；此前日志中的定向分页结果（`q=microbiome` 等）仍是关键词检索结果，不能视作整个站点的穷尽分类。
- re3data 的 API 与 XML export 已从文档核实，但没有批量下载/筛选全部 repository record。
- 本轮没有下载 FASTQ、完整外部 metadata 快照或测试样本，也没有启动第二阶段的 accession-to-metadata 实现。

## 2026-11-11 — 第十轮：重点 partial 资源复核与第一阶段首版验收

**检索窗口：** 2026-11-11（承接此前本日已开始的资源核查；精确起始时刻未采集）  
**过程中可确认的时钟读取（非检索起点）：** 2026-11-11 09:55:36 +08:00  
**记录完成时间：** 2026-11-11 10:03:13 +08:00  
**范围：** 复核 PLaBAse、OMDB、Microbiota Vault、VirJenDB、AMRnet 的官方入口/文档；复看 Celeri 和 The Microbe Directory 的在线表现；更新第一阶段首版状态与维护清单。

### 代表性检索式/核查入口

- `site:virjendb.org VirJenDB v1.1.3 sample metadata REST API`
- PLaBAse 官方查询页与下载页；OMDB 当前 About、repository 和 supplement 信息页。
- Microbiota Vault Deposits and Resources、FAQ；AMRnet Data Access 官方文档和 API docs。
- Celeri Studies Explorer 页面、The Microbe Directory 官方站点直接访问。

### 查阅来源与发现

- [PLaBAse 查询页](https://plabase.cs.uni-tuebingen.de/pb/plaba_db.php)：页面列出 5,565 个菌株并说明 taxonomy、plant-sphere 和 host-phenotype 筛选。核实搜索入口；没有批量下载或提交具体查询。
- [OMDB 当前介绍页](https://omdb.microbiomics.io/about?repo_id=ocean)：报告 12,347 个带地理坐标样本、274,282 个基因组和 31,058 个 prokaryotic species-level units，并描述序列/BGC 检索、交互地图及下载；许可标为 CC BY 4.0。没有下载数据或 accession join。
- [Microbiota Vault 目录](https://www.microbiotavault.org/deposits-and-resources/)：显示 9 个本地 collection、1,400+ 样本、部分 ENA/BioSample 链接、人类/食品 metadata templates 和 SOP；sequence release 仍受 depositor 控制。
- [VirJenDB 当前官网索引](https://virjendb.org/)显示 release v1.1.3；[官方 metadata 字段页](https://doc.virjendb.org/pages/metadata.html)列有 BioSample/BioProject/SRA、采样地点/日期和宿主等来源字段及映射文件。Swagger 页面无法被本轮浏览工具解析，没有调用 API。
- [AMRnet 数据访问文档](https://amrnet.readthedocs.io/en/latest/data.html)确认 organism TSV 无须注册，公开 S3 有周更 CSV，REST API 迁至 `api.amrnet.org` 且需免费 API key。本轮没有下载快照或提交请求。
- [Celeri Explorer](https://www.celerilab.com/data)显示 “No update available” 和 “Loading table...”；The Microbe Directory 的[官网](https://microbe.directory/)仍无法由当前检索工具打开。两者继续标 `active_partial`；Celeri 的同步间隔和抓取限制见资源卡。

### 本轮目录/文档改动

- 将 PLaBAse、OMDB、Microbiota Vault、VirJenDB 和 AMRnet 的资源状态调整为 `active_verified`，限定含义为官方可见的核心入口/文档能力有依据；没有写成 API 或单 accession 实测。
- AMRnet 更新官方 API base、数据下载文档、公开 S3 snapshot 路线与认证说明；VirJenDB 和 AMRnet API 工具行仍保留部分验证边界。
- 更新 Celeri、The Microbe Directory 最后核查日期和可观察限制；同步更新资源卡、CSV、README、开发计划、第一阶段复盘及资源发现日志。
- 首版快照：116 项资源（97 `active_verified`、11 `active_partial`、8 `legacy`）、89 张资源卡、37 项工具、8 项标准、13 项主题数据候选。
- 更正第九轮旧记录时间戳：该轮的 09:29:39 与 09:32:15 是搜索开始后的时钟读取，并非准确起止时间；其精确起点未采集。

### 未完成和边界

- 本轮依赖官方说明、当前门户和文档索引；未对 PLaBAse/OMDB/VirJenDB 发起交互查询，未调用 VirJenDB/AMRnet API，也未下载 AMRnet/OMDB/PLaBAse 数据。
- `active_verified` 是资源入口层级的状态，不代表字段齐全、样本 ID crosswalk、API 运行或字段逐条质量已经验证。
- FAIRsharing 需要合规认证的 API 扫描、更宽注册库/关键词搜索、11 项 `active_partial` 的后续复核、8 项 `legacy` 的具体历史文件/替代入口仍属日常维护清单。
- 第一阶段首版验收完成；没有读取或使用测试样本表，也没有开始第二阶段 ID-to-metadata 工具实施。

## 2026-11-11 — 第十一轮：GitHub 首版发布路径与部署准备

**记录时间：** 2026-11-11 10:10:52 +08:00  
**外部检索：** 本轮未新增文献/资源检索；整理此前研究结果并记录用户确认的发布方向。资源检索与状态变化见第九、十轮及 [`resource_discovery_log.md`](resource_discovery_log.md)。

### 本轮讨论结论

- 第一阶段可以作为一个独立可用的静态 GitHub 首版发布，建议标记 `v0.1.0`；后续第二阶段在同一仓库新增 ID-to-metadata 工具、schema、示例输入输出和使用说明，再以版本迭代发布。第一阶段的资源索引仍按时间戳日志维护。
- 当前项目由 Markdown/CSV/TSV 目录组成，首版不需要编译型 build，也不依赖 GitHub Pages；GitHub 仓库本身可以作为首版发布。若希望提供网页式筛选，再单独决定 Pages 或其他静态站点部署。
- 当前工作目录尚未初始化为 Git 仓库（不存在 `.git`），GitHub CLI 未安装；尚未配置 remote，也没有推送或创建 GitHub 仓库。
- 对外发布前尚需确定 repository owner/name、公开或私有、项目许可证和 citation/maintainer 信息，并建立经过授权的 GitHub 写入连接。不要在对话中发送密码、Personal Access Token 或其他凭据；通过应用连接或本机凭据管理进行授权。

### 需要用户提供/确认的信息

1. GitHub owner/用户名和仓库名，或已创建仓库的 URL（建议名：`microbiome-data-resource-index`）。
2. 仓库可见范围；结合“供其他开发者使用”的目标，建议 public。
3. 许可证选择；建议项目文档与整理目录采用 CC BY 4.0，未来源代码采用 MIT，并保留外部资源自己的许可/条款。可选择其他方案。
4. Citation/maintainer 中显示的姓名或 GitHub handle；ORCID、机构和公开邮箱均可选，不需要提供私人信息。
5. 是否同时部署 GitHub Pages（可选；首版默认只推送仓库，不启用 Pages）。
6. 将 GitHub 账号连接到当前工作环境，或提供有写入权限的目标仓库并确保现有连接可访问；不需要向助手粘贴任何密钥。

### 当前边界

- 本轮没有初始化 Git、创建远端仓库、写入 license 或公开推送；项目可见范围和许可影响公开发布，等待必要信息明确后再完成。
- 第一阶段首版数据快照仍为 116 项资源（97 verified、11 partial、8 legacy）、89 张资源卡、37 项工具、8 项标准、13 项主题候选。第二阶段尚未启动，也没有样本 accession 输入。

**连接状态补记（2026-11-11 10:13:17 +08:00）：** 随后确认当前 GitHub 连接可读取已授权账户 profile；因此用户无需在对话中提供账号密码或 token。尚未确认目标仓库写入权限；当前 GitHub 工具集未提供创建新仓库的操作，目标仓库仍需先存在，或另行使用账户中可用的创建入口。项目本地仍无 `.git`，也未执行任何远端写入。

## 2026-11-11 — 第十二轮：GitHub 发布预检与首版许可材料

**记录时间：** 2026-11-11 10:27:42 +08:00  
**外部资源检索：** 本轮未新增微生物组数据库/文献检索；核查了公开许可官方说明和当前 GitHub 仓库接口能力。

### 核查结果

- GitHub 连接可读取已授权账户信息；建议目标 `microbiome-data-resource-index` 在该账户下返回 404（尚不存在）。当前连接器可以操作已有仓库，但工具集中没有创建新仓库的接口；项目目录没有 `.git`，`gh` CLI 未安装，Git Credential Manager 未配置。因此还不能在此工作区建立 authenticated remote 或推送。
- 发布预检发现 `DISCUSSION_LOG.md`、`PROJECT_BRIEF.md`、`SOURCE_WORKFLOW_REVIEW.md` 含本机路径/旧项目内部目录信息。三份记录继续留在本地项目中，已加入 `.gitignore` 排除规则；目录、资源卡和检索日志保留用于候选公开首版。
- 本轮路径/凭据关键词检查未发现 API key、密码或 token 值。先前文件盘点为 117 个文件、约 2.21 MB，主要大文件为 workflow diagram（约 1.6 MB）；新增的许可与引用文件不含测序原始数据或大型矩阵。
- 许可方案依据 [Creative Commons CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)、[CC 对软件和数据库许可的 FAQ](https://creativecommons.org/faq/#can-i-apply-a-creative-commons-license-to-software) 和 [OSI MIT License](https://opensource.org/license/mit)：CC BY 4.0 可用于文档/数据库材料，需署名、链接许可并说明修改；CC 建议软件使用软件专用许可。因此暂为原创文档/整理目录拟定 CC BY 4.0，未来代码拟定 MIT。上游数据库/论文/资源条款不由本仓库 license 覆盖。

### 本轮本地改动

- 新增 `.gitignore`，明确排除三份包含本机路径的本地记录，并加入常见环境/缓存忽略规则。
- 新增 `LICENSE`（CC BY 4.0 范围说明与官方法律文本链接）、`LICENSES/MIT.txt`、`CITATION.cff`；引用署名暂用已连接 GitHub handle，版本拟为 `0.1.0`。
- 更新 README、CONTRIBUTING 和第一阶段复盘，说明许可覆盖范围、第三方内容边界和引用入口。
- 这些许可和署名文件目前是本地首版候选，尚未推送到远端；Public/Private、Pages 和仓库创建仍以用户最后确认/目标仓库为准。

### 继续所需条件

- 最直接的下一步是由用户在已连接账号下建立一个空仓库（建议 public，名 `microbiome-data-resource-index`，创建时先不勾选初始化 README/license/gitignore），然后提供该仓库 URL；之后用 GitHub 连接器写入首版目录并创建版本 tag。
- 如果选择组织仓库，请提供组织名/仓库 URL。GitHub Pages 为可选项，首版按静态仓库发布、不启用 Pages。
- 用户若同意当前许可、Citation handle 与公开设置，无需再提供用户名、邮箱、ORCID 或凭据；如需不同署名/许可，在推送前调整本地候选即可。
- 第二阶段仍未开始；无 accession/sample 表输入。本轮完成的是发布预检和本地准备，不是远端部署。

## 后续记录模板

复制以下结构追加新轮次：

```markdown
## YYYY-MM-DD — 第 N 轮：主题

**检索开始：** YYYY-MM-DD HH:MM:SS +08:00  
**检索结束：** YYYY-MM-DD HH:MM:SS +08:00  
**范围：** ...

### 代表性检索式
- `...`

### 查阅来源与发现
- [官方页面](https://...): 核实到什么；哪些还没做。

### 本轮目录/文档改动
- ...

### 未完成和边界
- ...
```

## 2026-11-11 — 发布准备记录：本地首版已提交，远端待建

**记录时间：** 2026-11-11 10:43:19 +08:00  
**目标仓库：** xiaolw95/microbiome-data-resource-index（用户已确认 public、CC BY 4.0 文档/目录、MIT 后续代码、署名 xiaolw95、不启用 Pages）。

### 本轮进展

- 已在项目目录初始化 Git 仓库，默认分支 main；首版 118 个公开文件已提交，提交短 SHA 为 $(git rev-parse --short HEAD)。
- 已配置 origin 为 https://github.com/xiaolw95/microbiome-data-resource-index.git。
- DISCUSSION_LOG.md、PROJECT_BRIEF.md、SOURCE_WORKFLOW_REVIEW.md 已被 .gitignore 排除，仍留在本机工作目录；公开提交不包含这三份内部记录。
- GitHub API 核查目标仓库仍返回 404。当前 GitHub 连接器没有创建仓库接口；浏览器自动化在访问已有窗口时因无法可靠确认 Windows 浏览器当前地址而被系统停止。因此还未创建远端，也未上传首版。

### 下一步

需要先在 xiaolw95 账户下创建空的 public 仓库 microbiome-data-resource-index（不初始化 README、license 或 gitignore）。创建完成后，当前 origin 与首版本地提交即可用于推送；之后核对远端文件和引用/许可，并补上 0.1.0 release/tag。第二阶段仍未开始。

## 2026-11-11 — 远端建仓与写权限核查

**记录时间：** 2026-11-11 11:07:10 +08:00  
**目标：** https://github.com/xiaolw95/microbiome-data-resource-index。

### 核查结果

- 远端 public 仓库已创建，默认分支为 main，目前只有 GitHub 初始化的 README。
- GitHub 连接器能读取仓库，但创建 Git blob 和通过 Contents API 新建文件均返回 HTTP 403（Resource not accessible by integration）；所以本轮没有文件被上传或公开。
- 本机 Git 的远端地址已设为 origin，但 git fetch origin 因本机无 GitHub 凭据而失败。连接器需要获准访问此个人仓库，或需在本机完成 GitHub Git 凭据认证后才能继续推送。

### 本地状态

- 首版公开文件已在本地 main 分支提交；3 份本机内部记录仍由 .gitignore 排除。
- 未创建远端 release/tag；未启用 Pages；第二阶段尚未开始。

## 2026-11-11 — 本地 Git 推送认证排查

**记录时间：** 2026-11-11 12:39:36 +08:00  
**目标：** xiaolw95/microbiome-data-resource-index。

### 本轮进展

- 使用 OpenSSL TLS 后端成功 fetch 远端 main，将 GitHub 自动生成的初始提交合并到本地发布分支；保留远端提交并以项目 README 解决同名文件冲突。
- git push 已实际尝试，但本机 GCM 没有向 Git 提供可用凭据，GitHub 返回 No anonymous write access。设备码登录遇到 TLS/网络错误；浏览器登录提示“此平台上不支持操作”。
- 因此，远端 main 仍只有初始化 README；本地 main 包含完整 118 文件首版和远端初始化历史，可通过 HTTPS/OpenSSL 推送。

### 待办

- 在用户交互式 PowerShell/终端运行带 OpenSSL 后端的 git push -u origin main，由本机 Git Credential Manager 完成登录提示；成功后核验远端文件，再创建版本标签。
