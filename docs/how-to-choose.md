# 按任务选择检索路径

## 我想先找到适合的数据库、仓库或工具

从[资源发现注册库指南](guides/resource_discovery_indexes.md)按目标选择 FAIRsharing、re3data、bio.tools、NAR Database Collection 或疾病/队列门户；这些入口用于定位候选资源，命中后再回官方服务查数据。

## 我已经有一个样本或测序 ID

1. 先识别 ID 和对象层级：NCBI/INSDC 的 BioSample、BioProject、Study、Experiment、Run；GSA 的 CRA、PRJCA、SAMC、CRX、CRR；GSA-Human 的 HRA/HRS；以及 GEO、EGA 等 accession 都不能互相替代。GSA 会整合 INSDC metadata，跨库汇总时要按原始 accession 去重。
2. 对单个 accession 或 DOI，可用 [`ffq`](../catalog/tools.csv)展开 GEO/SRA/ENA/DDBJ/BioSample 的已链接归档对象；NCBI ID 可用 EDirect/PySRAdb 检索核对。对于 NCBI 项目/样本筛 Run 并导出 RunInfo 表，可用官方 SRA Run Selector；需要 GSA 输入或多归档 ID 时可用 `iSeq`。
3. 对批量 accession 清单，`nf-core/fetchngs` 可生成 ENA metadata samplesheet 并下载 FASTQ；`fastq-dl`、Kingfisher 和 `iSeq` 都可解析归档 Run/metadata 并准备 reads，其中 `iSeq` 额外支持 GSA。`metatools_ncbi` 面向 BioSample 与 RunInfo 批量 metadata，`grabseqs` 支持 SRA/MG-RAST 的 metadata 和 reads，GEOfastq 面向 GEO accession 到 ENA FASTQ。ENA Browser Tools 适用于按 ENA Sample/Study/Run 拉取文件及 Run XML；浏览器选择可用 SRA Explorer。
4. 回到官方 archive 复核 Project/Study、BioSample、Experiment、Run 关系；Run/Experiment 不等于受试者或 biological sample 数。
5. 从 Project 页面、论文 Data Availability、Europe PMC/PMC 和 supplement 找来源表与 sample crosswalk；如果目标字段没有出现在公开 archive，再检查 curated resource 或受控 EGA/dbGaP 入口。
6. 为每个字段保留来源链接、层级、更新时间、公开/受控状态和不确定性。

对人体肠道 ENA shotgun 样本，可补查 [Celeri Microbiome Studies Explorer](resources/celeri.md) 的 AI-structured study/sample metadata；结果要回 ENA 和论文核验，因为它的底层来源是 submitter XML，未确认会从 supplements 补录信息。若研究已被 cMD 收录，可用 [OmicsMLRepoR](../catalog/tools.csv) 浏览 ontology-harmonized cMD metadata；这两个路径都是范围有限的二级查询，而非通用 accession resolver。

上述 CLI/平台可显著降低 archive 层 accession 解析和下载准备成本，但它们读取的仍是上游公开记录；不保证找到文章或 supplement 才有的饮食、生活方式和临床变量。各工具的安装、输出和限制见 [tools.csv](../catalog/tools.csv)。

当前仓库提供资源导航和人工查找步骤，尚未提供输入 ID 后自动跨站补充 metadata 的程序。

## 我从头开始找某类数据

1. 把问题拆成人群/host、condition、body site、assay、study design、时间和访问条件。
2. 从 [资源类别导航](resource-categories.md)选择专题数据库、归档和文献入口。
3. 使用 [母婴多位点指南](guides/maternal_infant_multisite.md) 或 [CRC 指南](guides/crc_microbiome.md)查看已发现候选。
4. 对疾病/病原体相关问题，可补查 [NIAID Data Ecosystem Discovery Portal](resources/niaid_data_discovery_portal.md)；营养和流行病学队列可查 [NFDI4Health](resources/nfdi4health.md) 与 [Mica](resources/mica.md)，再追到原始仓库。
5. 在专题指南中区分论文人数、specimens、BioSamples、Experiments 和 Runs；确认各研究是否有 patient/dyad/visit crosswalk。
6. 沿下载链接到 archive 进行逐项目核验。只有整理后 profiles/metadata 的数据集，说明其 release、筛选和底层 raw-data accession。

可按数据主题追加检索：

- **食品/发酵食品：** FoodMicrobionet 强在食品分类和 BioSample/Run 关联；FoodMicroDB 强在食品来源 amplicon 组成与时间序列；cFMD 强在 shotgun metagenomes、functional profiles 和 MAGs。三者互补，食品来源标签不能当作人体饮食暴露。
- **环境 shotgun：** Microbiome Datahub 可按环境、host taxon 和 BioProject 查 INSD 项目并下载项目 metadata；MGnify、SPIRE、GOLD/NMDC 可并行查样本和项目 context。汇总时记录项目级或 sample 级范围。
- **全球环境样本与标准化生态分类：** Earth Microbiome Project 可从 Qiita/Redbiom 搜索 EMP 样本 metadata/features，并下载 mapping files 和 observation tables；EMPO 为样本 habitat/type 提供分层分类。它是特定数据项目和配套发现链，不是所有公开样本的注册库。
- **海洋：** Ocean-M 是多组学样本/研究入口；OMDB 强调海洋样本地图、MAG、基因和 BGC；MMP 偏海洋微生物 reference genome/context database。三者不是同一个库，也不主要解决人体临床 phenotype。
- **农作物/根际：** MicroAgroBiome 提供作物相关 shotgun metagenomes 和统一处理结果；AgMicrobiomeBase 连接 UK crop/soil samples、ENA 和 MGnify；PLaBAse 用于植物相关菌株、基因组和性状参考，而不是 sample archive。使用前应核对门户和底层 archive 的适用条款。
- **动物：** AnimalMetagenome DB 提供动物 metagenome 项目/样本记录；AnimalMetaOmics 侧重多组学与功能目录；HoloFood Data Portal 则可按动物、feed treatment、采样时间和衍生样本关联查询。门户范围和 accession 层级需分别核对。
- **人体多位点：** Majorbio HMD 可按身体位点、国家、年龄、性别、health condition 等过滤候选；CNGBdb MDB 的官方帮助称可按 sample/project ID 查询并按 phenotype 筛选，但本轮服务访问超时。两者命中后仍需回原始论文和 archive 验证 crosswalk。
- **人体肠道 shotgun：** HGMA 提供 6,014 个人体肠道 shotgun 数据的固定下载表，包含 sampleID、年龄/性别/BMI/地理和源项目索引；Microbiome Repo 提供更大的、字段带证据的当前 curated catalog，但两者口径、技术范围和更新模式不同。
- **人体肠道 metadata harmonization：** cMD 3 提供人工整理、机器校验的人体 shotgun 数据与 metadata；OmicsMLRepoR 提供 cMD harmonized metadata、ontology-aware search、同义词和 ontology descendants 筛选。cMD 论文的 22,710 计数含额外纳入的 122 个样本，Bioconductor harmonized 表当前例子为 22,588 行，引用时需标注口径。
- **饮食/营养与肠道菌群队列：** Mica 可按研究、变量和 harmonization initiative 发现参加 INTIMIC/NFDI4Health 等网络的观察研究，并查看饮食暴露与菌群研究的 harmonization protocol；它公开的是研究级 metadata 导航，不等于获得个体饮食数据。PRIME 可供人体 16S 样本级 phenotype/metadata 和丰度查询，覆盖范围更偏公开整理的 16S cohorts。
- **德国健康/营养队列发现：** NFDI4Health Health Study Hub 有更广的健康研究目录和 REST API，metadata schema 包含 dietary-assessment 与 record-linkage 模块；命中研究后须再确认其是否有 microbiome sequencing accession，以及原始数据是否公开。
- **饮食—菌群具体研究：** [HPP 2026 diet–microbiome](guides/diet_nutrition_microbiome.md) 是已有 app-based diet log 与 shotgun metagenome 的代表案例；论文分析人数和当前 EGA 页面样本数不同，目录将其保留为 unresolved，说明主题检索还需要 accession/freeze/sample crosswalk 复核。
- **微生物代谢建模：** APOLLO 提供 microbial genome-scale reconstructions 和 sample-specific community models；MicroMap 提供这些模型的网络可视化。两者用于代谢/机制探索，不能提供或推断样本饮食与临床暴露。
- **物种/基因组背景：** mOTUs-db 可浏览 mOTU、MAG、isolate genome、注释和采样环境，mOTUs CLI 可做 reads taxonomic profiling 与关联基因组下载；适合分类参考和来源上下文，不等于受试者 metadata。
- **人体长读长/Hybrid shotgun：** HLRMDB 可按 sample、采样情境、health state 和平台筛选 38 项研究中的 1,672 个长读长/混合数据集，并浏览组装 MAG 与功能结果；使用前核对学术/商业条款和每个 sample 的 Run 映射。
- **肠道糖类利用功能：** dbCAN-HGM 可从 CAZyme/CGC、底物或 taxonomy 维度检索人体肠道功能参考，并浏览不同 diet/disease 组的 read mapping；该分组不能当作任一 BioSample 的个体饮食或疾病表型。
- **深海生态多组学：** DOO 为深海动物及其 symbionts 提供 genome、metagenome、transcriptome、单细胞记录与下载；若需研究级 sample metadata，再追到原始研究和归档。
- **病毒样本/宿主字段：** VirJenDB 可从病毒 accession 或 SRA/BioSample/BioProject 互链开始查看 collection、host、taxonomy 字段并调用 API；MetaVR 更适合检索 UViG/vOTU、病毒分类、预测 host 与蛋白簇。两者对象是病毒记录，不能直接视为人类参与者 metadata。
- **微生物性状/基因组功能：** metaTraits 可为 taxon/genome/profile 汇总微生物 traits；MicrobialScope 可按 genome ID 查询功能注释、ARG/virulence；metagRoot 适合从植物根际蛋白家族开始发现。它们补的是微生物层信息，不能填补宿主年龄、饮食、健康状态。
- **病原体耐药研究：** AMRnet 提供限定菌种的地理/时间/AMR surveillance；ARKbase 提供病原菌 genome、AST 和耐药/毒力知识；IVCDB 关注 Iridoviridae isolate、宿主范围和地理分布。用作 pathogen 背景或专题候选，不应混同通用微生物组数据库。
- **人体肠道临床表型筛选：** HMBR 的官方 portal facets 和 advanced search 支持按 study、assay、race、smoking history、gender、age category 等筛样本；file manifest 与 sample metadata manifest 显式保存 file ID—sample ID 关系及 subject/sample accession 字段。适合目标条件明确并且需要核对文件访问类型的场景。
- **配对 microbiome–metabolome：** HuMMANet 汇总跨研究的配对肠道样本 metadata、菌群 profile、原始/标准化代谢组 profile 与 metabolite annotations；适合发现多组学候选，不是通用 archive 或任意样本 ID 查询平台。
- **复杂项目 ID 映射案例：** MetaSUB `map_collate` 和其 source spreadsheets 展示 FASTQ filename、MetaSUB name、H.A. ID、barcode、plate position 等多层关系。可借鉴 provenance/清理思路，但字段不完整且只针对 MetaSUB。
- **本地 collection/biobank：** Global Microbiome Conservancy 和 Microbiota Vault 可发现多地区 collection、数据联系人与部分 BioSample/ENA accession；GMC 数据需 dbGaP 或联系申请，Microbiota Vault 的样本/序列开放状态由本地 depositor 决定。
- **动物物种性状：** The Microbe Directory 可补充 taxon-level phenotype/ecology 解释；它不能补某个 BioSample 的宿主饮食、年龄或疾病值。
- **跨仓库疾病数据发现：** NIAID Data Ecosystem Discovery Portal 可按感染性/免疫介导疾病、organism 或数据类型检索跨来源 metadata，并导出 CSV/JSON；它只索引来源记录、不托管原始数据，且 source coverage 和 metadata 完整度有限。

## 我需要下载 raw reads

- 先确定原始 Run accession 和所有 Runs，而不是只从 paper title 推断。
- 检查数据是否 public、controlled 或 embargoed，记录许可和申请入口。
- 核对样本与 library/Run 的一对多关系、Run 大小、layout 和测序策略。
- 下载流程入口见 [NCBI SRA download docs](https://www.ncbi.nlm.nih.gov/sra/docs/sradownload/)；下载 FASTQ 会产生大量本地数据，README/数据目录不放这些文件。

## 我需要年龄、饮食、生活方式、健康状态或临床变量

- 先看原始文章和 supplements 是否明确提供字段及 ID mapping。
- 再看主题 curated resources 是否公开整理该字段。
- 若数据受控，使用 EGA/dbGaP 的授权流程；受控状态不是可通过搜索或脚本绕开的障碍。
- 如果文章只报告 cohort-level demographics，输出仍标 cohort-level，不自动复制到每条 sample。

## 快速比较

| 入口 | 最擅长 | 不应期待 |
|---|---|---|
| SRA/ENA/DDBJ | Raw read 项目与技术记录、样本 accession | 每个样本均有完整人口学/饮食/生活方式 |
| `ffq` | 单个 ID/DOI 到关联 archive accession 的自动展开 | 解析文章补充文件中的自定义样本 ID 或个体表型 |
| NCBI SRA Run Selector | 以 Study/Sample/Experiment accession 筛 Run 并导出 RunInfo | 读取文章/补充表中的自定义 ID 或恢复缺失 phenotype |
| `iSeq` | 在 GSA、SRA、ENA、DDBJ 间解析 accession、metadata 和 reads | 文章/补充材料中未归档的 host metadata；镜像记录需去重 |
| Kingfisher | Run/BioProject 到 NCBI metadata；多源 reads 获取 | 归档未提供的 participant metadata 或 crosswalk |
| `nf-core/fetchngs` / `fastq-dl` | 批量 accession 的 archive metadata samplesheet 与 reads 下载准备 | 不经复核直接把归档字段当作完整 participant metadata |
| `metatools_ncbi` / `grabseqs` / GEOfastq | NCBI BioSample/RunInfo、SRA/MG-RAST 或 GEO→ENA 的专门路径 | 全面跨论文补充材料的样本/受试者映射 |
| SRA Explorer / ENA Browser Tools | 网页检索、样本选择、Run 文件/归档 XML 获取 | 全文检索或跨论文的 subject/sample crosswalk |
| MAMI / Microbiome Repo | 按主题、site 或测序范围发现候选 | 全 assay、全 publication 的完备覆盖 |
| Celeri | ENA 人体肠道研究的 AI-structured metadata 搜索 | supplement recovery、已验证的公开 API 或全 microbiome 覆盖；注意当前同步日期和限制性条款 |
| Mica | 营养/肠道菌群观察研究、variables 和 harmonization potential 的发现 | 通用 SRA/BioSample resolver 或无申请的个体级饮食问卷下载 |
| NFDI4Health Study Hub | 德国健康/营养流行病学研究、变量和访问路径的发现 | 微生物组专属数据库或一键下载所有 cohort 的个体数据 |
| HMBR | 按人体肠道样本表型筛选并导出文件/sample manifests | 全微生物组领域通用 accession resolver；所有文件都开放 |
| HLRMDB | 按人类长读长/Hybrid 样本情境筛选并关联 MAG/功能结果 | 任意测序项目的通用 metadata resolver；商业用途无需确认 |
| dbCAN-HGM | 人体肠道 CAZyme/CGC 与糖类利用功能参考 | 个体样本饮食/疾病字段或 cohort crosswalk |
| VirJenDB / MetaVR | 病毒序列 accession、host/context 字段或 UViG/vOTU/蛋白搜索 | 普通人类 microbiome sample 的完整临床变量 |
| metaTraits / MicrobialScope / metagRoot | 微生物 taxonomy、genome traits、功能和植物根际蛋白家族 | 宿主受试者年龄、性别、饮食或健康问卷 |
| AMRnet / ARKbase / IVCDB | 病原基因组、AMR/AST、病毒 isolate 和宿主范围背景 | 通用微生物组人群表型或参与者级 metadata |
| HuMMANet | paired microbiome–metabolome study packages 和匹配 metadata | 不限疾病/身体位点/多组学组合的通用目录 |
| MetaSUB `map_collate` | MetaSUB 项目内的多级样本 ID/文件名 crosswalk 案例 | 可复用于其他研究的通用样本映射工具 |
| NIAID Data Ecosystem Discovery Portal | 从疾病/病原体出发跨来源找 datasets、tools 和 catalog metadata | 所有微生物组数据的完整目录或底层数据下载仓库 |
| FoodMicrobionet / FoodMicroDB / cFMD | 食品来源 amplicon、食品类别/样本关系、食品 shotgun/MAG | 人体 participant 饮食、行为或临床 metadata |
| Microbiome Datahub | INSD shotgun BioProject 环境/host 分类、项目 metadata TSV/API、MAG 搜索 | 项目级环境注释直接映射到每个 BioSample |
| CNGBdb MDB / Majorbio HMD | 平台内样本/项目筛选和 phenotype/body-site 查找 | 完整字段覆盖、稳定跨平台 resolver 或未声明的 API/许可 |
| Ocean-M / OMDB / MMP | 海洋样本、环境位置、多组学或基因组参考 | 人类宿主临床表型 |
| MicroAgroBiome / PLaBAse | 作物相关 metagenomes、植物相关菌株/性状参考 | 每个样本均有完整作物/地块/宿主映射 |
| curatedMetagenomicData / CRC compendium | 标准化 profiles 与 curated metadata | 代替原始研究定义、supplement 或许可条款 |
| OmicsMLRepoR | cMD/cBioPortal harmonized metadata 下载与 ontology-aware 浏览 | 任意 accession 的多源检索、论文 supplement 解析或包外研究覆盖 |
| PRIME / primeDB | 人体 16S sample phenotype metadata、profiles、REST API 与 R client | shotgun 或所有身体位点/生态系统的全覆盖；样本记录数等于参与者数 |
| mOTUs-db / mOTUs profiler | 原核生物参考基因组、taxonomy、environment 和 profiling | 人体参与者饮食、年龄、疾病等 phenotype |
| APOLLO / MicroMap | 微生物代谢模型与机制可视化 | 生物样本真实饮食、药物暴露或临床 metadata |
| Europe PMC / PMC / supplement | 研究设计、变量定义、样本映射线索 | 结构完全一致、易解析的单一 metadata 文件 |
| EGA / dbGaP | 受控 human clinical/phenotype 数据申请 | 未获批前获取完整受控字段或数据文件 |
| MIxS / STORMS / ontologies | 字段结构、术语和报告核查 | 补出原始研究未提供的属性 |
