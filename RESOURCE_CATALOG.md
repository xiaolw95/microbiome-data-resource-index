# 相关资源详解：数据库、数据包、检索接口与规范方法

**检索日期：** 2026-11-10  
**范围：** 解释本项目已讨论的资源具体存放什么、能做什么、不能替代什么。重点围绕“输入可能只有 public sequencing accession，需要再发现论文及样本映射”这一边界。没有对任何用户测试 accession 查询。

## 先区分四种资源

1. **公共 archive/API**（NCBI SRA/BioSample、ENA、Europe PMC、PMC BioC）：提供可编程的原始记录和关联服务。它们有稳定入口和 ID 关系，但提交者元数据不等于完整宿主表型，也不会替每篇论文完成样本 crosswalk。
2. **已整理的数据库/数据集**（cMD、HumanMetagenomeDB、GMrepo、PRIME、GutBiomeDB、Microbiome Repo）：已对特定范围的一批 accession/研究做筛选、映射或整理，可查覆盖范围内的数据；大多不是任意输入 accession 的通用实时信息恢复服务。
3. **抽取/规范化方法**（MetaSRA、数据库各自的 curation pipeline、Microbiome Repo 的 routes）：把已取得的字段或论文证据解析成标准值，功能和适用的输入证据各不相同。
4. **字段规范/词表**（MIxS/MIMARKS 等）：定义应如何描述样本与测序上下文，本身不储存样本答案，也不负责找论文。

## 逐项说明

### 1. Microbiome Repo（数据库 + 数据包 + 可复现的整理流程）

- **它是什么：** Olm Lab 于 2026-11-06 发布的 human-associated shotgun DNA/RNA 目录。既有网页样本/项目搜索，也提供 release 固定的数据包、多个表和 SQLite 包；资料页公开检索/整理路线。当前 scope 是人类相关 shotgun，不包括任意 RNA-seq、16S、single-cell、空间组学或非人样本。
- **存什么：** 项目、BioSample/sample、Run、论文关联、字段级 determination 和冲突记录。每个字段 claim 可含 source、locator、quote、route、scope、determiner 和 confidence tier。查询界面可以按 SAMN/项目/题名等搜索已收录样本，并查看每字段证据。
- **怎么找数据：** registry 先从 ENA/SRA/DDBJ 项目识别符合人类 shotgun 条件的研究；论文通过 Europe PMC accession mentions/data availability 和 NCBI BioProject declared publications 连接。再分路线整理：R1 BioSample/archive attributes；R2 机器可读 supplement 表按 accession/alias/library name 精确 join；R3 OA 正文；R4 abstract/title/archive description。它把研究层陈述明确标为 study-wide，并留下冲突。
- **AI 用在哪里：** 官方方法说明中，R1 主要由确定性字段映射与解析器完成，模型帮助判断含糊字段名或标准化部分疾病词；R2 表连接不使用模型；R3/R4 使用模型抽取候选，同时要求引用片段能在原文中核对。其方法还说明 case–control 描述不会自动分给样本。
- **对本项目的价值：** 这是已查到的最接近“自动发现 archive、论文、supplement 并将证据连回样本”的完整实践；特别值得借鉴 registry→paper link、exact-match gate、逐字段证据、conflict table 和版本化数据包。
- **不能直接解决的部分：** 它是预先整理的特定范围 catalog。输入 ID 不在其 scope 或 release 覆盖内时，不会因此自动恢复信息。其公开字段覆盖不完整，置信数值是 engine tier，不是校准概率；文档也承认全文和 supplement 访问受 OA 范围限制，PDF-only supplement 不在当前 parser 覆盖范围。新资源适合作为现成查表来源和流程参照，不能作为完整度保证。
- **来源：** [About](https://microbiomerepo.com/about/index.html)、[Methods](https://microbiomerepo.com/about/methods.html)、[Downloads/releases](https://microbiomerepo.com/downloads/index.html)、[Samples](https://microbiomerepo.com/samples/index.html)。

### 2. GutBiomeDB（整理数据库 + 分析平台）

- **它是什么：** 2026 年 NAR 论文发布的肠道 16S 数据库和分析网站。论文列出 168,464 个样本、482 个 BioProjects，并提供统一 taxon matrix 及疾病、生命阶段、性别、地理等整理字段和分析工具。
- **怎么建：** 以已有的公共 human gut 16S compendium 为底，不重新处理原始 reads；人工整理使用 BioProject/BioSample、PubMed 论文、ENA、EBI BioSamples、ClinicalTrials.gov、Qiita 和 GMrepo。curator 阅读方法、人口学表、纳排标准和样本级 supplement；两人独立核对，第三人处理分歧。疾病标签以明确表述为准，未知值不自动填成健康对照。
- **类型判断：** 主要是可搜索和分析**已整理好的一批数据**；有人工整理实践方法，但不是输入任意 accession 就从网络抓论文和建 crosswalk 的通用检索器。
- **对本项目的价值/限制：** 可查已纳入肠道 16S 样本，并提供疾病/群体二级核验。其数据域、字段范围、入选样本有限，不覆盖一般 shotgun、非肠道宿主微生物组或所有测序 assay。
- **来源：** [NAR paper and methods](https://academic.oup.com/nar/advance-article/doi/10.1093/nar/gkag1125/9013047)。

### 3. curatedMetagenomicData 3（人工整理的 R/Bioconductor 数据包 + 软件接口）

- **它是什么：** R/Bioconductor 和 CLI 可访问的 human shotgun 数据包，包含处理好的 taxonomic/functional profiles 和 harmonized sample metadata；新版本文章报告约 22.7k 个样本、94 cohorts，涉及 100+ 参与者特征。
- **怎么建：** 团队对入选队列手动整理 metadata，再由机器规则/校验辅助；文章报告 17 位 curator 参与。它通常围绕已经选入的研究整理样本 ID、subject、年龄、性别、疾病、body site、国家、技术信息等。
- **类型判断：** 主要是“整理好的数据仓库/软件包”，提供查询和下载；它不是通用文献爬虫或 accession-to-supplement 实时抽取器。
- **对本项目的价值/限制：** 对它覆盖的 shotgun 数据，可作为已有 sample/subject crosswalk、标准字段与 gold-set 候选。它纳入的是有限研究集合；遇到未收录 accession，仍需自行找原始论文和 supplement。
- **来源：** [Nature Communications article](https://www.nature.com/articles/s41467-025-66888-1)、[Bioconductor package](https://bioconductor.org/packages/release/data/experiment/html/curatedMetagenomicData.html)。

### 4. GMrepo v3（人工整理数据库 + 微生物组分析 pipeline）

- **它是什么：** NAR 2026 Database Issue 中的人类肠道 16S/WGS 数据库和网站；论文发布时覆盖 890 个项目、118,965 个样本和 302 种表型/疾病及健康对照，并提供跨项目疾病标志物分析。
- **怎么建：** 从 NCBI BioProject 与 PubMed 的关键词检索得到约 20,000 个候选项目；LLM 仅用于初筛项目是否可能属于人类肠道研究，之后由 curator 人工确认研究范围并整理表型/metadata。纳入项目后从 SRA/ENA 取数据和 metadata，进行两轮人工 metadata curation；测序处理另有 16S/WGS pipeline。
- **类型判断：** 已整理的疾病导向数据库和分析系统；它的研究发现流程包含候选文献/项目筛查和人工整理，但不是面向任意 sample ID 的通用元数据恢复 API。
- **对本项目的价值/限制：** 可作为肠道疾病、样本组别和表型的二级查询来源；也提供有用的“LLM 只筛候选、人工确认最终纳入”范例。大量人口学字段仍缺失，范围主要是肠道数据。
- **来源：** [GMrepo v3 paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC12807640/)。

### 5. PRIME（人工/规则整理的 16S 数据库 + API/R package）

- **它是什么：** 人类 16S 数据库；论文报告 111 个研究、53,449 个 Run-level samples，统一的 phenotype/body-site/研究设计信息和 16S 处理结果，并支持 web、REST API 与 R package。
- **怎么建：** 原始 sample-level metadata 从 NCBI SRA Run Selector 获取；论文报告结合正则表达式解析与人工注释，将自由文本说明和自定义字段转成标准字段。研究层信息还人工核验。
- **类型判断：** 主要是已整理数据库并附查询接口；它确实给出 metadata parsing 和 manual curation 方法，但目标是其选定的 16S 项目集，不是通用 accession-to-paper/supplement 检索器。
- **对本项目的价值/限制：** 对 16S 和文中收录的项目有帮助。其 curated sample 单位是 Run；并入用户确认的 BioSample 主表时，必须保留 Run 与 BioSample 的关系，避免把 run 数误当 biological sample 数。
- **来源：** [PRIME 2026 NAR paper](https://doi.org/10.1093/nar/gkaf1057)、[PRIME docs](https://primedb.sjtu.edu.cn/help)。

### 6. HumanMetagenomeDB（历史性的人工整理元数据库）

- **它是什么：** 人类 WGS metagenome 的网页检索/CSV 下载数据库。原论文的 v1.0 收录 69,822 个 metagenomes，标准化 203 个属性，包含年龄、性别、BMI、诊断、国家/坐标、sample site 和测序属性。当前网站仍展示 69,822 条、Release 1.1（2020）。
- **怎么建：** 聚合 SRA 和 MG-RAST metadata；先用 PARTIE、library 字段和规则筛除非 WGS，然后用 human/non-human 关键词字典分类，人工检查保留结果；通过属性同义词表、BTO/DOID 等概念规范化 sample site 和诊断。
- **类型判断：** 已汇总并标准化的数据库，附带其构建方法；不是论文 supplement 抽取服务，也不是每次查询都会访问最新文章的 pipeline。
- **对本项目的价值/限制：** 可复用其 host/sample site/diagnosis 属性设计和同义词映射思想；版本较旧且主要从 archive metadata 生成，因此无法解决用户指出的“只给 ID，相关论文表里才有宿主信息”的主要缺口。
- **来源：** [NAR paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC7778935/)、[current database](https://web.app.ufz.de/hmgdb/)。

### 7. MetaSRA（标准化数据库 + 自动 ontology mapping pipeline）

- **它是什么：** SRA human RNA-seq sample-specific metadata 的标准化数据库，提供查询 API 和 JSON/SQLite 下载；历史版本 1.8（2020）列出 718,384 samples。原论文 scope 是 Illumina human RNA-seq，不能视为全体 SRA 当前全集。
- **怎么建：** 输入主要是 SRA/BioSample 提交的 key-value attributes；算法把 phenotype、tissue/anatomy、cell type 等映射至 Disease Ontology、Cell Ontology、Uberon、EFO、Cellosaurus 等词表，并用 Text Reasoning Graph 保留术语与上下文关系，也抽取部分年龄/数值属性。API 返回 raw metadata 与 ontology terms；官网的 sample/run endpoints 可用于已整理样本查询。
- **类型判断：** 既有可下载/可查询的**数据库**，也有可参考的**字段规范化算法**；它整理和解释当前已有 archive attributes，主要不负责从论文/补充文件发现原本未存入 archive 的新属性。
- **对本项目的价值/限制：** 可参考术语映射、上下文消歧、provenance graph 与 ontology hierarchy；需考虑其领域/assay 覆盖与版本更新节奏。
- **来源：** [original paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC5870770/)、[API](https://metasra.platformx.wisc.edu/api.html)、[downloads](https://metasra.platformx.wisc.edu/supportpages/download.html)。

### 8. MetaHQ（跨库注释聚合数据库 + CLI，不是新的原始信息抽取器）

- **它是什么：** 2026 arXiv 预印本所述的整合平台，称汇集 13 个来源近 200,000 条公共 omics 样本/研究注释，并提供 CLI 查询在线/打包数据库。
- **怎么建：** 核心是从多个既有社区整理来源收集并 harmonize 注释，重点是“已有答案跨库分散、格式与字段不统一”的索引和分发。
- **类型判断：** 聚合整理后的数据库 + 查询客户端。它不等价于一个从输入 accession 开始下载原始论文、读取每份 supplement 并建新样本关联的通用工具。
- **对本项目的价值/限制：** 将来可作为额外二级 evidence route/交叉验证来源。其预印本尚非 peer-reviewed；官方仓库说明注释库受 CC BY-NC 4.0 限制，具体数据来源的许可需要逐项确认。
- **来源：** [preprint](https://arxiv.org/abs/2602.07805)、[repository and license](https://github.com/krishnanlab/meta-hq)。

### 9. MIxS/MIMARKS（字段标准/检查清单，不是数据库）

- **它是什么：** Genomic Standards Consortium 对样本上下文和序列报告内容的 checklist/terms。HumanAssociated、HumanGut 等扩展给出适配的字段语义。
- **可做什么：** 作为新数据模型的字段字典起点和完整性参照，有助于术语和最低报告要素互操作。
- **不能做什么：** 它不保存样本值、不替用户抓取论文，也不能补回作者没有公开的饮食/病史/individual mapping。
- **来源：** [MIxS current specification](https://genomicsstandardsconsortium.github.io/mixs/)。

### 10. MGnify（微生物组分析平台 + 数据库/API + 论文文本挖掘展示）

- **它是什么：** EMBL-EBI 的免费 metagenomics/metatranscriptomics/amplicon/assembly 数据与分析平台，可按 study/sample/run 查询 ENA 关联数据和 MGnify 分析，并提供 API。
- **已有 metadata 来源：** sample metadata 从 ENA/BioSample 来；部分样本有 ELIXIR Contextual Data Clearing House 的补充或更正；publication 页面还显示由 Europe PMC/EMERALD 提供的论文 text-mined 注释。
- **最关键的限制：** 官方文档明确说，publication 上的自动注释无法被自动且有把握地判定具体对应到哪些 sample；sample 页面会提示相关论文注释存在，但不代替 sample-level join。这直接支持把样本 crosswalk/evidence adjudication 作为本项目关键增量。
- **类型判断：** 平台/API 能查询已接入研究、样本和分析；带有 publication text-mining 集成，但不是完整的 accession→supplement-row crosswalk 工具。
- **来源：** [MGnify documentation](https://docs.mgnify.org/index.html)、[portal, metadata and publication annotations](https://docs.mgnify.org/src/docs/portal.html)、[API](https://www.ebi.ac.uk/metagenomics/api/v1/?format=api)。

### 11. Qiita（多组学 study/sample metadata 仓库 + 分析平台）

- **它是什么：** 可复用多组学研究、样本信息和实验 preparation 信息的平台，支持 metadata、raw/BIOM data 下载以及与 EBI 仓库的数据提交流程。
- **metadata 结构：** study、sample information 和 preparation information 分开维护；一个样本可以对应不同实验 prep。文档列出 study/sample metadata 接口，但不同 API 的开放状态、认证和权限需要分别检查；部分 REST 文档仍标为内部/计划开放。
- **类型判断：** 主要是数据/metadata 平台与分析系统，也包含社区提交的样本数据；可作为命中某研究时的补充来源，不能假设任何 accession 都已同步到 Qiita。
- **来源：** [Qiita documentation](https://qiita.microbio.me/static/doc/html/index.html)、[REST API docs](https://qiita.microbio.me/static/doc/html/dev/rest.html)、[2018 paper](https://doi.org/10.1038/s41592-018-0141-9)。

### 12. 新增的受控人类表型与环境/JGI资源

- **dbGaP：人类受控表型归档。** 公开层可以查研究摘要、phenotype variables 和 study documents；个体级 phenotype/genotype 按 study 由 DAC 控制，通常需要 Data Use Certification。官方提交规范包含 Subject Sample Mapping 文件，所以在某些研究中它可能提供把 subject 与测序样本连起来的关键表；该映射是否公开需按项目核查。它与 EGA 都是受控人类数据入口，但数据来源和访问条款分属各自研究。
- **NMDC：环境微生物组多组学数据库/API。** 提供 studies、biosamples、data objects 和处理结果的 REST 查询及标准化样本 metadata，强调 MIxS/EnvO 和可复用工作流；公开数据采用 CC BY 4.0，文件下载需 ORCID。官方 FAQ 明确其当前不收录 human microbiome，因此适合环境微生物组和字段/标准参考，不适合补充人体饮食或临床 metadata。
- **GOLD：项目与生物样本 metadata 注册库。** JGI GOLD v10 维护 genome/metagenome sequencing projects、biosamples 和 ecosystem classification；覆盖来源广，也连接到 JGI 的 IMG/M。它更适合作为环境与微生物项目检索/交叉链接，不是人类临床表型库。
- **IMG/M：微生物组功能注释和比较分析。** 以 GOLD 的 metadata 组织公共 metagenome 和 reference genomes，长处是 taxonomic/functional annotation 与 comparative analysis；不会替代原始测序归档或文献中的 host phenotype table。
- **JGI Data Portal：JGI 生成数据的文件发现和下载。** 2026 年新版门户取代已 sunset 的 JGI Genome Portal，提供公开 genome/metagenome 文件 metadata 搜索和 API/CLI/Globus 下载。API 需要登录，部分归档文件需排队恢复；它主要覆盖 JGI 公共数据，不是全网 accession resolver。
- **来源：** [dbGaP overview](https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/about.html)、[dbGaP submission guide](https://www.ncbi.nlm.nih.gov/gap/docs/submissionguide/)、[NMDC API and portal guide](https://docs.microbiomedata.org/howto_guides/portal_guide/)、[NMDC data policy](https://microbiomedata.org/nmdc-data-use-policy/)、[GOLD v10](https://doi.org/10.1093/nar/gkae1000)、[IMG/M](https://img.jgi.doe.gov/)、[JGI Data Portal API](https://files.jgi.doe.gov/apidoc/)。

### 13. 全球/海洋样本上下文与宿主相关参考基因组资源

- **SPIRE：** shotgun 样本、研究、MAG 与功能目录的整合平台。样本 contextual data 来自 ENA、适用的 IMG/M metadata 和匹配论文，再以 habitat/lifestyle microntology 人工标注。适合全球环境和宿主相关 metagenome 的二级发现；不能假定每个记录有临床/人口学表型。[FAQ](https://spire.embl.de/faqs)、[原始论文](https://doi.org/10.1093/nar/gkad943)。
- **Ocean-M：** 海洋多组学平台，连接 sample search、环境梯度、MAG、功能基因与生态互作。适合海洋样本和多组学发现；其 host 语境是海洋生态互作，不是人体临床信息。[官网](https://om.biocloud.net/)、[原始论文](https://doi.org/10.1093/nar/gkaf1098)。
- **MicrobiomeDB：** 平台把已收录研究的 sample metadata、MIxS/custom ontology 和菌群丰度用于交互查询；2024 年 release 37 公告新增 93 项 shotgun studies。当前首页可访问但研究表初始化失败，故只标 `active_partial`，不把历史论文功能描述成已实测的现行能力。[About](https://microbiomedb.org/mbio/app/about)、[release notes](https://microbiomedb.org/mbio/app/static-content/MicrobiomeDB/news.html)、[NAR 论文](https://doi.org/10.1093/nar/gkx1027)。
- **HRGM2、MRGM、MOMD：** 分别提供人类肠道、小鼠肠道和小鼠口腔的基因组/分类/功能参考。它们适合物种鉴定和微生物参考比较，不等同于含有宿主年龄、饮食、疾病、采样时间及 accession crosswalk 的临床样本 metadata 库。[HRGM2](https://doi.org/10.1038/s41564-025-02206-1)、[MRGM](https://doi.org/10.1080/19490976.2024.2393791)、[MOMD](https://doi.org/10.1128/mSystems.01222-20)。

### 14. 2026 NAR Database Issue 中的新增专题资源

- **ResMicroDb：** 人体呼吸道 curated sample/run、phenotype、年龄、sex、BMI、采样部位和 sequencing metadata，提供项目/样本过滤与 metadata/profile 下载；是本轮新增资源中最直接匹配宿主样本 metadata 检索的专题库。[官网帮助](https://resmicrodb.cncb.ac.cn/help)、[NAR 2026](https://doi.org/10.1093/nar/gkaf1194)。
- **gutMSNP：** 将人类肠道微生物 SNP、参考 genome 与 21 种宿主 phenotype 关联，并给出 project accession、PMID 和样本数量等研究级线索；个体病例标签的 sample-level crosswalk 仍需回源。[官网](https://bio-computing.hrbmu.edu.cn/gutMSNP/)、[NAR 2026](https://doi.org/10.1093/nar/gkaf1205)。
- **VIRE：** 从公开 metagenomes 组装全球病毒基因组，并与 SPIRE、MetaLog 的生态/临床上下文连接；对 virome 环境发现有用，不是临床问卷仓库。[官网](https://vire.embl.de/)、[NAR 2026](https://doi.org/10.1093/nar/gkaf1225)。
- **PanGBank：** 以 REST API/CLI 提供大规模微生物 pangenome 图谱。它扩充微生物基因组学和功能比较资源，不直接补充 BioSample 的宿主 phenotype。[官网/API](https://pangbank.genoscope.cns.fr/)、[NAR 2026](https://doi.org/10.1093/nar/gkag948)。
- **发现依据：** [2026 NAR Database Issue 总览](https://doi.org/10.1093/nar/gkaf1427) 收录 182 篇数据库论文；本轮按“微生物组研究发现、样本/人群或环境上下文、可复用菌群/基因组数据”筛选相关条目，而不是把 issue 中所有基因数据库全部纳入。

### 15. 注册库补充的古代样本和菌株参考资源

- **OAGR：** Adelaide University/Research Data Australia 目录保留古代人类 genome 与 microbiome 原始/处理数据、provenance/production metadata、CC BY 4.0 和数据 DOI 的历史记录；但 [re3data 将仓库标注为自 2022 年离线](https://www.re3data.org/repository/r3d100011632)，原始 Figshare/OAGR landing page 也不可访问。因此目录状态改为 `legacy`，机构目录/DOI 只作为历史发现线索，不代表 OAGR 主服务或当前 inventory 可用。[Research Data Australia 记录](https://researchdata.edu.au/online-ancient-genome-repository/1604205)、[DOI](https://doi.org/10.4225/55/59ae2d4038294)。
- **BacDive：** 细菌/古菌菌株知识库，超过 1,000 个字段覆盖 taxonomy、isolation origin、physiology、cultivation 和 sequence accessions；2026 年起 API v2 可免注册访问。它支撑菌株/isolate 背景核查，不提供人群样本或宿主表型。[官网](https://bacdive.dsmz.de/)、[API v2](https://api.bacdive.dsmz.de/)、[NAR 2025](https://doi.org/10.1093/nar/gkae959)。

### 16. 2026-11 扩展检索新增的主题资源

这轮按食品、植物/农业、动物、海洋、环境项目检索、人体多位点、菌株/参考序列和疾病知识库扩大目录。新增资源说明见各自卡片和 machine-readable CSV。

#### 食品与农业资源

- [FoodMicrobionet](docs/resources/foodmicrobionet.md) 通过 FoodEx2 和样本表整理食品细菌/真菌 amplicon 数据，并保留 BioProject、BioSample、Run 与 publication 关系；其样本匹配说明了重复归档/跨细菌真菌表的处理。
- [FoodMicroDB](docs/resources/foodmicrodb.md) 以 food 与 food-sourced organism 组织食品来源 amplicon，突出组成、跨食品比较和时间序列。
- [cFMD](docs/resources/cfmd_food_metagenomes.md) 以 shotgun food metagenomes、功能和分类 profiles、MAG 为重点，提供版本化 GitHub 数据发布。
- [MicroAgroBiome](docs/resources/microagrobiome.md) 把作物/根际 shotgun 数据、taxonomy/function、MAG、BGC 等连到原始 NCBI accession；[PLaBAse](docs/resources/plabase.md) 则是植物相关菌株及促生性状知识库，不是样本归档。

这几项可帮助用户从“食品类别/作物场景”找数据，但 food-source category 不能当成受试者饮食、dietary recall 或人群生活方式信息。

#### 环境、动物和海洋资源

- [Microbiome Datahub](docs/resources/microbiome_datahub.md) 面向 INSD shotgun metagenome BioProject 和基因组/MAG；按 environment、host taxon 和关键词筛选，提供项目 metadata TSV/API。它提供的 project context 需要保留为 study/project scope，不能无依据地赋给所有 BioSample。
- [AnimalMetaOmics](docs/resources/animalmetaomics.md) 汇总动物微生物多组学和功能信息，区别于已有的动物样本 accession/metadata 清单；当前门户仍待复核。
- [Ocean-M](https://om.biocloud.net/) 是海洋多组学样本与研究平台；[Ocean Microbiomics Database (OMDB)](docs/resources/ocean_microbiomics_db.md) 强调全球海洋 MAG、BGC、坐标和地图下载；[Marine Metagenomics Portal](docs/resources/marine_metagenomics_portal.md) 提供 MarRef/MarDB 等带环境/宿主上下文的参考基因组。名称接近但对象和任务并不相同。

#### 额外样本入口、参考库和历史资源

- [CNGBdb MDB](docs/resources/cngb_mdb.md) 的官方帮助描述 sample/project ID 搜索和 phenotype filters，但本轮服务超时；它和美国 MicrobiomeDB 是两个不同数据库。
- [Majorbio HMD](docs/resources/majorbio_ihmd.md) 提供人体多身体位点的样本/项目筛选，页面列 age、gender、country、body site 和 health condition；尚未确认 diet、API、release 和许可。
- [VagDB](docs/resources/vagdb.md) 是阴道特异性 DADA2 参考序列，不是可查样本表型的数据库。
- [ODFM](docs/resources/odfm.md) 和 [MicroPhenoDB](docs/resources/microphenodb.md) 是有正式论文记录但本轮原入口不可用的历史资源，保留为文献检索线索。

另更新两个版本敏感条目：[Human Microbiome Compendium](docs/resources/human_microbiome_compendium.md) 当前 Zenodo release 为 v1.1.2（2026-08-20）；Microbiome Repo 官网当前报告 R2026.36 / package 1.30.0（2026-11-06）。引用计数时要区分 project、sample record 和 participant。

### 17. 第二轮扩展：项目型样本门户、biobank 和专题集合（2026-11-10）

第二轮再按可下载样本表/项目入口、受控或委托开放 collection、农作物/动物试验、多生态系统样本、taxon-level 注释检索，新增 8 条资源。它们的对象粒度和访问模式差异明显，适合并列导航但不能合并解释成同一类数据库。

- **Human Gut Microbiome Atlas（HGMA）：** 固定版人体肠道 shotgun compendium。论文整理 6,014 个样本、19 个国家和 23 类疾病；下载文件提供 sampleID.csv（age/sex/BMI/geography）、bioproj.csv、abundance matrix 和模型。它与全生态系统 MicrobeAtlas、以 16S 为主的 Human Microbiome Compendium 不是同一资源；v2 发布于 2022-10-25，按固定 release 使用。[官网/下载](https://www.microbiomeatlas.org/downloads.php) · [论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC11293553/)
- **Earth Microbiome Project（EMP）：** 特定大型协作项目整理数据，而非全领域 archive。mapping files、metadata、observation tables 和结果经 Zenodo/FTP/Qiita 发布；样本可通过 Qiita/Redbiom 以 metadata/feature 查找；EMPO 提供分层 habitat/sample-type 术语。[数据与代码](https://earthmicrobiome.ucsd.edu/data-and-code/) · [metadata guide](https://earthmicrobiome.ucsd.edu/protocols-and-standards/metadata-guide/) · [EMPO](https://earthmicrobiome.ucsd.edu/protocols-and-standards/empo/) · [原始论文](https://doi.org/10.1038/nature24621)。本轮另将 Redbiom 列入 tools.csv、EMPO 列入 standards.csv。
- **动物与农业项目门户：** HoloFood Data Portal 连接 animal 与 derived sample，官方文档说明 treatment search 会读取动物 BioSample 的采样时间、处理名称/描述、代码和浓度；门户列 9,889 samples、12,557 genomes、128,888 viral sequences。[API 文档](https://docs.holofooddata.org/api.html) · [论文](https://doi.org/10.1093/database/baae112)。AgMicrobiomeBase 覆盖 UK crop rhizosphere/bulk soil，并将样本/测序数据目录与 ENA、BioSamples、MGnify 等公共资源连接；它与 MicroAgroBiome（更广的作物相关 metagenome compendium）不同。字段筛选和批量导出尚未核实；访问前应查看当前门户与底层 archive 条款。[项目数据页](https://agmicrobiomebase.org/data/) · [Cryobank 论文](https://doi.org/10.1186/s43170-023-00190-2)。
- **collection/biobank 访问边界：** Global Microbiome Conservancy 的 metadata 需向项目方申请/联系，测序数据指向 dbGaP phs002235.v1.p1 并需正式 controlled-access request。[GMC access](https://microbiomeconservancy.org/our-work/our-biobanks/) · [dbGaP](https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/study.cgi?study_id=phs002235.v1.p1)。Microbiota Vault 列出 local collections、部分 ENA/BioSample accession 和 metadata templates；FAQ 明确 depositor 保留样本控制权、序列只有在 depositor 请求时公开。[collection list](https://www.microbiotavault.org/deposits-and-resources/) · [FAQ](https://www.microbiotavault.org/faq/)。二者属于发现并申请的路线，不等同可匿名批量下载的样本库。
- **MICROBE Data Portal：** 单个欧洲 MICROBE 项目的 portal/API，项目页索引显示 4,353 samples；GitHub 代码说明其缓存并连接 ENA、BioSamples 和 MGnify。当前在线门户访问超时，因此保留 active_partial，未将 API endpoint schema 当成已核实能力。[portal](https://data.microbeproject.eu/) · [official code](https://github.com/EBI-Metagenomics/microbe-data-portal)。
- **The Microbe Directory：** 物种性状和生态特征 knowledgebase，不是 sample archive。2025 论文报告近 18,000 个跨细菌、古菌、藻类、真菌、病毒物种的约 42 类特征；当前门户不可达，按 active_partial 保留。[论文](https://doi.org/10.1093/database/baaf060)。

上述资源分别落入 curated dataset、project platform、microbial knowledgebase；ID 类型、metadata domains、访问模式和限制已写入 resources.csv 与对应资源卡。资源状态不表示开放程度或数据完整度。

### 18. 第三轮交叉检索：样本表型、ID crosswalk 与配对多组学资源（2026-11-10）

本轮追踪三个与项目核心需求直接相关但功能不同的资源，并把对应工具纳入索引。

- **HMBR：** 人体肠道样本/文件发现平台。除 study、assay、race、smoking history、gender、age category 等筛选项外，官方 sample metadata manifest 示例还显示 subject accession、sample accession、PMID、disease、BMI、age category、body site、timepoint、药物和生活方式相关字段。file manifest 将 file ID、checksum、size、URL 与 sample ID 关联；其主体功能是研究集内检索、过滤和批量下载，不承诺跨数据库任意 accession 解析。[官方 Browse Portal](https://microbiome-bioactives.org/browse-portal/index.html) · [file/sample manifests](https://microbiome-bioactives.org/download-file-manifest/index.html) · [IGS Portal Client](https://github.com/IGS/portal_client) · [2026 IBD study](https://doi.org/10.1053/j.gastro.2026.06.023)。
- **MetaSUB Reproducible Metadata：** 项目专用的可复现 metadata collation 和多层 ID 映射范例。公开仓库包含源表、清理脚本与 crosswalk；README 报告 `map_collate` 生成 1,301 个 samples/FASTQs 的 metadata，并指出字段常缺失、barcode 可能丢失 leading zero、ID 可能经 plate/barcode/lab name 等层级间接关联。它为未来通用流程提供 provenance 与 unresolved handling 的设计案例，但只处理 MetaSUB 项目内资料。[仓库 README](https://github.com/MetaSUB/MetaSUB-metadata) · [样本命名与数据存储说明](https://metasub-bioinformatics.readthedocs.io/en/latest/data_storage.html) · [MetaSUB 2021 paper](https://doi.org/10.1016/j.cell.2021.05.002)。
- **HuMMANet：** 2026 年 preprint、Zenodo 数据记录与 Bioconductor/GitHub R package 描述了 46 个 paired gut microbiome–metabolome studies、59 个 study-units 和 14,405 个样本。研究包可包含 sample metadata、subject annotations、临床协变量、timepoint、body site、taxa abundance、原始/标准化 metabolite profiles 和 annotation tables。它适合从研究问题发现 paired multi-omics 数据，而非任意 accession resolver；原始数据权限按来源研究分别处理。[Zenodo](https://doi.org/10.5281/zenodo.22053943) · [Bioconductor package](https://bioconductor.org/packages/HuMMANet) · [GitHub documentation](https://github.com/ShivangiV-IIITD/HuMMANet) · [preprint](https://doi.org/10.64898/2026.08.24.746727)。
- **新增工具：** IGS Portal Client 以 HMBR cart 生成的 manifest 下载文件，并校验 MD5；MetaSUB `map_collate` 处理项目内部 ID indirection；HuMMANet R/Bioconductor 包按 study 加载对齐的 metadata 和 omics 数据。三者分别是下载客户端、项目专用 ID 整理工具和专题多组学数据访问包，不能代替通用 accession-to-metadata 系统。

第三轮结束时的快照：`resources.csv` 94 条（76 active_verified、10 active_partial、8 legacy；类型分布：11 archive、45 curated_dataset、2 literature_supplement、20 microbial_knowledgebase、16 microbiome_platform）；资源卡 67 张，tools.csv 23 项，standards.csv 6 项。该统计只代表第三轮结束时的目录状态。

### 19. 跨仓库疾病数据发现入口（2026-11-10）

- **NIAID Data Ecosystem Discovery Portal：** 这是跨仓库 discovery portal，不是微生物组专库或数据托管 archive。它整合多个感染性/免疫介导疾病和 generalist repositories 的 dataset、resource catalog、sample 与 tool metadata，当前收录源包括 MicrobiomeDB；可以用关键词、organism、disease、data type 或 advanced field query 搜索，导出 CSV/JSON，或用公开 API 批量取回标准化 metadata。点击 Access Data 后仍需沿原始来源获取数据。[Portal](https://data.niaid.nih.gov/) · [API 使用指南](https://data.niaid.nih.gov/knowledge-center/accessing-the-metadata-api) · [metadata 导出指南](https://data.niaid.nih.gov/knowledge-center/gathering-insights) · [FAQ](https://data.niaid.nih.gov/knowledge-center/frequently-asked-questions) · [2026 mSystems resource report](https://doi.org/10.1128/msystems.01270-25)。
- **适用边界：** Portal 自身声明不会托管数据；只覆盖已接入来源，源记录缺少字段时无法替它补出信息，generalist repositories 也会带来与 query 不相关的命中。因此它适合作为疾病/宿主研究问题的额外发现层，命中后要在源库、文章和补充材料中核实样本粒度及数据权限。
- **资源类型扩展：** 为准确表达“不托管数据、汇总其他来源 metadata”的 portal，在 `catalog/schema.md` 新增 `resource_discovery_portal` 类型；最初用于 NIAID，现也用于 NFDI4Health Health Study Hub。该类型与 archive 或专题 curated dataset 分开，后者保存/处理自身样本或数据对象。
- **新增工具：** `niaid_nde_api` 索引其公开 API；支持查询 Portal 索引 metadata，不下载源数据，也不绕过源库访问条件。

第四轮结束时快照：`resources.csv` 95 条（77 active_verified、10 active_partial、8 legacy；类型分布：11 archive、45 curated_dataset、2 literature_supplement、20 microbial_knowledgebase、16 microbiome_platform、1 resource_discovery_portal）；资源卡 68 张，tools.csv 24 项，standards.csv 6 项。此统计保留为历史快照。

### 20. 2026 NAR Database Issue 与微生物功能/病原体资源扩展（2026-11-10）

- **新增长读长人体数据与肠道功能资源：** HLRMDB 按样本/健康状态/采样上下文搜索长读长和 hybrid human metagenomes，并连接 MAG、功能和 ARG 结果；dbCAN-HGM 提供肠道 CAZyme gene clusters、glycan substrate 与群体层面的饮食/疾病 read mapping。后者不是个体饮食/临床 metadata 表。
- **新增生态与微生物参考资源：** DOO 连接深海物种、共生微生物和多组学记录；MicrobialScope 提供跨细菌、古菌、真菌和病毒的 genome/functional annotations；metaTraits 汇总实测及预测微生物性状；metagRoot 收录植物根际蛋白家族和生态上下文。
- **新增病毒与病原监测资源：** MetaVR 提供 UViGs/vOTUs、分类、预测 host 与蛋白资源；VirJenDB 将病毒序列与 BioSample/BioProject/SRA 和 host/sample metadata 对接；IVCDB 专注 iridovirus isolates/genomes/host range；AMRnet 将公共病原体 genomes 整理成 AMR 时空 surveillance 数据；ARKbase 提供 pathogen reference genomes、AST 与 AMR/virulence 注释。
- **使用边界：** 以上大多数扩展资源是专项整理数据库、参考功能知识库或病原监测平台，不能自动给普通 microbiome BioSample 补全参与者年龄、饮食和临床变量。HLRMDB 是本批最贴近样本/采样情境筛选的入口；VirJenDB 与已有病毒 accession 互链最相关；其他功能库主要提供辅助背景。
- **状态与方法：** 本轮以 2026 NAR 数据库 Issue 汇总表及各资源官方主页、官方文档和原始论文交叉发现。MetaVR、metaTraits、metagRoot、VirJenDB、AMRnet 标为 `active_partial`，原因分别是端点访问错误、scheduled maintenance、门户访问异常、主站检查失败和 API 未实测。NAR 汇总报告该年度数据库专刊有 182 篇文章、在线数据库目录 2,173 项，故它是重要候选来源，但不是微生物组数据库穷尽目录。
- **本轮工具入口：** 增加 metaTraits JSON API、MetaVR API、VirJenDB REST API 与 AMRnet API/数据快照索引；这些 API 提供 trait/virus/pathogen records，不等于通用样本 metadata resolver。

### 第六轮扩展：metadata 搜索、harmonization 和微生物模型资源（2026-11-10）

- **Celeri：** 新增针对 ENA 人体肠道研究的 AI-structured metadata explorer。需特别留意其结果来自 submitter XML、最近可见同步日期、未核实 API，以及条款对镜像/系统抓取的限制；当前仅作链接索引和人工发现入口。
- **OmicsMLRepoR / cMD 3：** 补入 ontology-aware 的 harmonized metadata R 包，并更正 cMD 3 的计数口径：包内可用数据与论文纳入额外研究后的分析总数不同。两者提供高质量的人体 shotgun metadata 参考，但只覆盖已整理队列。
- **Microbiome Research Data Toolkit：** 新增为采集/字段 harmonization 规范，可用于审阅人口学、anthropometrics、生活方式和饮食字段设计；不是公共数据检索库。
- **mOTUs-db、APOLLO、MicroMap：** 扩展纳入基因组/环境上下文与微生物代谢建模资源，分别标为间接背景/建模支持；不把物种或代谢模型信息误作 host phenotype。

### 第七轮补充：营养研究发现与 16S metadata 查询更新（2026-11-10）

- **Mica：** 新增 INTIMIC 的营养流行病学/肠道菌群 metadata portal，记录 study、变量、harmonization initiative/protocol 和 DataSHIELD/Opal federated analysis 路线。适合从 diet/nutrition 研究问题发现队列，但不能当作公开个体级数据仓库或通用 accession crosswalk。
- **PRIME：** 更新为 2026 NAR 论文报告的 53,449 个样本、111 项研究、93 个身体位点和 101 类 phenotype；补充 REST API v1 与 primeDB R client，并新增 `tools.csv` 工具记录。样本记录不等于参与者数。
- **GutBiomeDB：** 核对 2026 NAR 论文和官方 release：168,464 个人体肠道 16S sample records、482 个 BioProjects、72 个国家，含 disease/life-stage/sex/geography 等人工整理 metadata，Zenodo v1.0.0 与公开 REST endpoints；官网需 JavaScript，尚未逐一核验 API endpoint。

### 第八轮补充：健康研究与营养 metadata 门户（2026-11-10）

- **NFDI4Health Health Study Hub：** 加入跨领域研究发现门户索引。它收录临床、公共卫生和流行病学研究 metadata，具有 REST API；营养流行病学 metadata schema 含 dietary assessment 和 record-linkage 模块。它不是菌群数据库，使用者须继续确认 assay、测序 accession、数据权限和样本映射。
- **NFDI4Health Metadata Schema：** 作为独立标准记录，用于健康研究人群、设计、饮食评估和数据访问等字段组织；schema 不提供研究的实际 phenotype 值。
- **边界：** API 文档显示资源搜索 endpoint，但本轮没有调用 endpoint；仅记录可核实的官方说明，不声称已下载或遍历整个 Hub。

当前快照：`resources.csv` 112 条（88 active_verified、16 active_partial、8 legacy；类型分布：11 archive、48 curated_dataset、2 literature_supplement、30 microbial_knowledgebase、19 microbiome_platform、2 resource_discovery_portal）；资源卡 85 张，tools.csv 32 项，standards.csv 8 项。`datasets.csv` 13 条，其中 10 verified、2 unresolved、1 candidate。此目录尽量广泛检索、持续扩展，仍不声称穷尽全部已发表资源。

## 资源对本项目的结论

### 它们中谁最像“输入 ID 后自动查全”

目前所查资源里，Microbiome Repo 的采集与 evidence routes 最接近目标；MGnify 有 archive/分析集成和 publication text-mining 展示，但它自己也说明文章注释无法自动可靠地归属到具体 sample；GutBiomeDB/GMrepo/PRIME/cMD/HumanMetagenomeDB 是针对已收录研究的 curated database；MetaSRA 是归档字段标准化；MetaHQ 是多个现成注释库的合并入口；Qiita 是多组学 study/sample metadata 与分析平台。**没有一个已核实资源能承诺：任给一种公共测序 accession，它都能为所有物种、assay 和期刊自动找到原始论文、下载各种格式的补充材料，并把所有作者自定义 sample ID 无歧义映射回 accession。**

### 因此本项目需要自建的关键能力

1. accession 解析和实体关系核验；
2. BioProject/Study→原始数据论文发现，区分原始数据论文与 reuse/citation 论文；
3. supplement 文件发现与多格式抽取；
4. accession/sample alias/library ID/subject ID 的显式 crosswalk 建立与验证；
5. sample、subject、visit、group、study/cohort 等 scope 区分；
6. 逐条证据、冲突、未匹配项和访问失败记录；
7. 用人工核对 gold set 测量“正确链接率”和“误归属率”。

本项目已经把 MGnify、Qiita、SRA Toolkit 和 EDirect/PySRAdb 等入口分入 `catalog/resources.csv` 与 `catalog/tools.csv`；后续扩展时应继续区分“数据/样本 metadata 平台”“序列下载器”“archive 字段规范化”“论文/supplement 检索”，并记录工具的输入输出、服务对象与权限限制。当前清单仍有待核候选，不能视为已覆盖全部工具。

论文有宿主信息而没有样本 crosswalk 时，工具可以收录研究级背景，但必须把 sample mapping 结果留空/标记 unresolved。这个限制是来源数据关系本身的限制，不是增加语言模型推理即可可靠补齐的缺口。

## 官方或原始来源索引

- [NCBI SRA object model](https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/)
- [Europe PMC REST API](https://dev.europepmc.org/RestfulWebService)
- [PMC supplementary material BioC API](https://www.ncbi.nlm.nih.gov/research/bionlp/APIs/FAIR-SMART/)
- [PMC AWS article datasets](https://pmc.ncbi.nlm.nih.gov/tools/pmcaws/)
- [GSC MIxS](https://genomicsstandardsconsortium.github.io/mixs/)
