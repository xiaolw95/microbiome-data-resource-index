# 资源类别导航

**主数据源：** [resources.csv](../catalog/resources.csv)（完整、可筛选的机器可读目录）　**核查日期：** 2026-11-11

本页按资源的主要用途导航。类别是方便发现的组织方式，不代表资源只能承担一种角色。`active_verified` 表示官方入口/文档或原始论文确认了至少一项核心能力，不等于已对任意 accession 做端到端测试；`active_partial` 与 `legacy` 的边界详见目录行和资源卡。跨平台查到的宿主信息仍须核实是否能映射到具体 BioSample、subject 或 visit。

## 跨领域资源发现注册库

这些入口先帮助你找数据库、仓库、工具或标准；它们多数不保存实际测序文件或逐样本表。用法和边界见[资源发现注册库指南](guides/resource_discovery_indexes.md)。

- [FAIRsharing](resources/fairsharing_registry.md) — 数据库/仓库、标准和政策之间的策展注册与关系链接。
- [re3data](resources/re3data_registry.md) — 研究数据仓库元数据、开放性、标准和 API 发现。
- [bio.tools](resources/biotools_registry.md) — 生物信息学软件、服务、数据库和工作流目录。
- [NAR Molecular Biology Database Collection](resources/nar_database_collection.md) — 年度数据库论文与多领域数据库目录。

## 公共序列、样本、研究与表型归档

适用于从 BioProject/Study、BioSample、Experiment、Run、GEO accession、论文或样本关键词开始寻找归档记录。公开 reads 与个体临床表型的开放程度不是一回事。

- [NCBI Sequence Read Archive (SRA)](resources/ncbi_sra.md) — 原始测序 Run 及关联 Study、Experiment、BioSample。
- [NCBI BioSample](resources/ncbi_biosample.md) — 提交者提供的生物样本属性；字段完整度由提交者和项目规范决定。
- [NCBI BioProject](resources/ncbi_bioproject.md) — 研究/项目叙述、关联样本和序列数据 accession。
- [European Nucleotide Archive (ENA)](resources/ena.md) — INSDC 项目、样本、实验、Run、API 与文件下载入口。
- [DDBJ Sequence Read Archive (DRA)](resources/ddbj.md) — INSDC 原始数据归档，可与 ENA/NCBI 记录互链。
- [Genome Sequence Archive (GSA, CNCB-NGDC)](resources/gsa.md) — 原始 reads 归档和 INSDC 元数据整合；跨库镜像记录需按原始 accession 去重。
- [Genome Sequence Archive for Human (GSA-Human)](resources/gsa_human.md) — 人类个体/样本/实验层级的公开与受控组学归档；需遵守 DAC 访问条件。
- [NCBI Gene Expression Omnibus (GEO)](https://www.ncbi.nlm.nih.gov/geo/) — 功能基因组研究 accession、样本和 processed files；高通量测序 reads 通常由 GEO broker 到 SRA。
- [EMBL-EBI BioStudies](https://www.ebi.ac.uk/biostudies/) — 跨学科研究记录、论文关联、metadata 和附件/补充文件检索；不能假定其中每个附件都有 sample crosswalk。
- [European Genome-phenome Archive (EGA)](resources/ega.md) — 人类遗传/组学研究的公开项目描述与受控数据申请入口。
- [NCBI Database of Genotypes and Phenotypes (dbGaP)](resources/dbgap.md) — 人类研究、变量字典和受控 phenotype/genotype；获批项目可能提供 subject–sample 映射。

## 微生物组分析、数据浏览和协作平台

平台可能提供预处理结果、样本表或分析工作区；平台内部 ID 与 SRA/ENA accession 的对应关系要逐项确认。

- [CNGBdb Microbiome Database (MDB)](resources/cngb_mdb.md) — 官方帮助描述按 sample/project ID 检索、Experiment/Run/Assembly 浏览和 170 多项 phenotype 过滤；当前页面超时，且它不同于美国 MicrobiomeDB。
- [Integrated Human Microbiome Database and Analysis System (Majorbio HMD)](resources/majorbio_ihmd.md) — 人体多位点项目/样本浏览，官方页面列出年龄、性别、country、body site 和 health-condition filters；饮食字段、API 与许可尚未确认。

- [MGnify](resources/mgnify.md) — ENA reads 的微生物组分析、样本和分析结果。
- [Human Microbiome Bioactives Resource Portal (HMBR)](resources/hmbr.md) — 人体肠道/IBD 样本与文件门户，可按年龄、性别、race、吸烟史、研究和 assay 等筛选，并导出文件—样本 manifests。
- [Celeri Microbiome Studies Explorer](resources/celeri.md) — 将 ENA 人体肠道研究的 submitter metadata 用 AI 结构化并提供 study/sample 搜索；不搜索补充文件，当前同步日期和批量使用条款需留意。
- [Mica (INTIMIC metadata portal)](resources/mica.md) — 从营养流行病学/肠道菌群研究开始查 study、变量、harmonization protocols 和 federated-analysis 入口；个体数据可能仍在研究方服务器并需申请。
- [MG-RAST](resources/mg_rast.md) — 项目、样本、library、metagenome 和功能分析；本轮已验证公开 metagenome API 返回样本 metadata。
- [iMicrobe](resources/imicrobe.md) — 历史微生物组发现/data-broker 平台；当前官方主站访问异常，按 Legacy 保留。
- [Qiita](resources/qiita.md) — 微生物组 study/sample metadata、preparation 和可复用分析结果。
- [National Microbiome Data Collaborative (NMDC)](resources/nmdc.md) — 环境微生物组标准化多组学门户与 API；不收录 human microbiome data。
- [JGI Data Portal](https://data.jgi.doe.gov/) — 检索 JGI genome/metagenome 文件及 metadata，通过网页、API、CLI 或 Globus 获取。
- [IMG/M (Integrated Microbial Genomes and Microbiomes)](https://img.jgi.doe.gov/) — JGI 微生物组装配、功能注释和比较分析；关联 metadata 来自 GOLD。
- [MicrobiomeDB](resources/microbiomedb.md) — 收录研究的样本描述/本体映射与丰度查询（`active_partial`：本轮 app 的研究表未成功初始化）。
- [Human Microbiome Project Data Portal](https://www.ihmpdcc.org/data.php) — HMP/iHMP 数据目录；公开资源可浏览，受控人体数据需按原仓库和 dbGaP 条件访问。
- [Ocean-M](resources/ocean_m.md) — 海洋多组学样本、环境梯度、MAG、功能和生态互作浏览。
- [Deep Ocean Omics (DOO)](resources/deep_ocean_omics.md) — 深海生物、共生微生物及其 genome、metagenome、transcriptome 和单细胞多组学目录；关注深海生态，不是人体宿主 metadata 数据库。

## 整理型数据集与主题数据库

适合按宿主、人群、疾病、身体位点、生态环境或 assay 发现已整理数据。其收录范围通常有限，不是任意 accession 的通用解析器。

### 人体、人群、疾病和身体位点

- [African Human Microbiome Portal](resources/african_human_microbiome_portal.md) — 面向非洲人群微生物组研究，提供 BioProject/BioSample 检索、地图与下载；页面在本轮报告 70 个 BioProjects、14,889 个 BioSamples。
- [curatedMetagenomicData 3](resources/curatedmetagenomicdata.md) — 人体 shotgun 研究的人工整理 metadata 与标准化 profiles；包内 22,588 样本和论文 22,710 样本的统计口径不同。
- [gcMeta](https://gcmeta.wdcm.org/) — 全球人类肠道菌群研究与样本/表型相关整理数据。
- [GMrepo v3](resources/gmrepo.md) — 人类肠道研究、疾病/健康标签、taxonomic profiles 和 Run/Sample 搜索说明。
- [GutBiomeDB](resources/gutbiomedb.md) — 人类肠道 16S 研究及年龄/生命阶段、性别、地理和疾病信息；支持 metadata/profile 下载。
- [gutDBase](resources/gutdbase.md) — 肠道疾病 host transcriptomics、microbiome profiles 与 host–microbe association 的多组学浏览。
- [Human Microbiome Compendium](resources/human_microbiome_compendium.md) — 可下载的统一处理人体肠道 16S 数据集；固定版本资源。
- [Human Gut Microbiome Atlas (HGMA)](resources/human_gut_microbiome_atlas.md) — 人体肠道 shotgun 整理集，提供 sampleID、age/sex/BMI/geography、disease、abundance profiles 和源 BioProject 线索；Version 2 是 2022 年固定版。
- [HLRMDB](resources/hlrmdb.md) — 人类长读长与 hybrid metagenomes 的样本/研究/基因组 bin 查询、采样情境和 health-state 索引，并提供 assembly、功能和 ARG 结果；学术使用免费，商业使用需联系项目方。
- [dbCAN-HGM](resources/dbcan_hgm.md) — 人类肠道 CAZyme gene clusters 与 glycan-utilization 功能库；可查看饮食/疾病组 read mapping，但不是个体饮食或诊断 metadata 表。
- [APOLLO](resources/apollo.md) — 人体微生物代谢模型及 sample-specific community models；用于建模微生物代谢潜力，不是一般的 phenotype 查询库。
- [HuMMANet](resources/hummanet.md) — 配对肠道微生物组—代谢组研究的整理数据集与 Bioconductor 数据包，提供样本 metadata 和 study-aligned profiles；不是任意 accession resolver。
- [HumanMetagenomeDB](https://web.app.ufz.de/hmgdb/) — 人体 metagenome 样本、年龄/BMI 等信息及 raw/processed 下载；当前可访问的是有明确 release 日期的固定版本（2020）。
- [mBodyMap](resources/mbodymap.md) — 多身体位点和疾病相关研究；原论文描述项目及 sample/Run metadata 下载，含年龄、性别、国家、BMI 和疾病字段。
- [MAMI (Microbiome Atlas of Mothers and Infants)](resources/mami.md) — 母婴人群及多个身体位点的 accession、样本/研究和 abundance 发现入口。
- [Global Microbiome Conservancy](resources/global_microbiome_conservancy.md) — 多地区人类肠道样本和菌株 biobank；metadata 联系 GMC，测序数据需走 dbGaP 受控访问。
- [Microbiota Vault](resources/microbiota_vault.md) — 人类与发酵食品本地 collections 的目录、metadata 模板和部分 ENA/BioSample 线索；序列公开取决于 depositor 授权。
- [Meta2DB](https://zenodo.org/records/17315984) — 可下载 metadata CSV、字段字典和处理后 profiles 的多研究整理数据集；许可需按记录确认。
- [Metalog](resources/metalog.md) — 跨研究 contextual metadata 浏览/过滤、分类和下载；当前网站有反爬访问限制，论文说明核心能力。
- [MiCoDa](resources/micoda.md) — 多生态系统的整理型 16S 数据资源。
- [Microbiome Repo](resources/microbiome_repo.md) — 人体相关 shotgun DNA/RNA 研究、主题筛选和 evidence routes。
- [MicrobiomeHD](https://github.com/cduvallet/microbiomeHD) — 已整理的人体肠道 16S 病例/对照固定数据集；GitHub 仓库已归档，按历史分析资源使用。
- [NIBN Japan Microbiome Database (NIBN JMD)](resources/nibn_jmd.md) — 日本人群肠道队列，公开版含年龄组、性别、地区，部分队列有饮食/营养信息；部分浏览需注册，详细表型可能受限。
- [PRIME](resources/prime.md) — 53,449 个样本、111 项人类 16S 研究，含人工整理 phenotype、metadata/abundance 下载和 REST/R 访问。
- [ResMicroDb](resources/resmicrodb.md) — 人体呼吸道样本、表型、年龄/性别等 curated metadata 与 profiles。

### 环境、动物和古代样本

- [Microbiome Datahub](resources/microbiome_datahub.md) — 按 environment、host taxon 和关键词检索 INSD shotgun metagenome BioProjects，并提供项目 metadata TSV/API 与 MAG 搜索；项目级上下文不能直接下推到每个样本。
- [Earth Microbiome Project (EMP)](resources/earth_microbiome_project.md) — 多生态系统样本和标准化数据集；metadata/observation tables 可由项目 archive、Qiita/Redbiom 搜索，配套 EMPO。
- [MetaSUB Reproducible Metadata](resources/metasub_metadata.md) — 城市公共交通微生物组项目的 metadata 清理和多层 ID crosswalk 范例，连接样本名、barcode、plate、实验室 ID 与 FASTQ 名称；字段有缺失且不适用于通用 accession 查询。
- [MICROBE Data Portal](resources/microbe_data_portal.md) — 项目级样本/API 门户，连接 ENA、BioSamples 与 MGnify；当前 API 行为待在线复核。
- [AnimalMetaOmics](resources/animalmetaomics.md) — 非人动物 microbiome 的 metagenome、metatranscriptome、metaproteome 和 pangenome 多组学；当前门户访问状态待核。
- [HoloFood Data Portal](resources/holofood_data_portal.md) — 鸡/鲑鱼生产系统多组学样本与 animal/treatment metadata API；适合 feed intervention 场景。
- [Ocean Microbiomics Database (OMDB)](resources/ocean_microbiomics_db.md) — 海洋坐标样本、MAG、基因/BGC 和地图下载；官网标注功能仍在开发，区别于 Ocean-M。
- [Marine Metagenomics Portal (MMP)](resources/marine_metagenomics_portal.md) — MarRef/MarDB 等海洋微生物 genome 与 contextual metadata 参考目录，含 environment/host、taxonomy、phenotype 等字段。
- [Genomes OnLine Database (GOLD)](https://gold.jgi.doe.gov/) — JGI 维护的 genome/metagenome project 与 biosample 注册信息、生态系统分类和 metadata 搜索。
- [MarineMetagenomeDB](https://web.app.ufz.de/marmdb/) — 海洋 shotgun metagenome 的环境 metadata、空间/水体属性与下载。
- [TerrestrialMetagenomeDB](https://web.app.ufz.de/tmdb/) — 陆地 metagenome 环境属性筛选和 CSV 导出；网页所示 release 为 2021 年。
- [MicrobeAtlas](https://microbeatlas.org/) — 全球样本组、项目、出版物和 taxa 浏览/下载；完整 schema 和逐 accession 查询尚未实测。
- [SPIRE](resources/spire.md) — shotgun 样本环境上下文标注，并连接研究、样本、MAG 和基因目录。
- [VIRE](resources/vire.md) — 将公共 metagenome 病毒基因组关联到环境、study 与 SPIRE/MetaLog 上下文。
- [AnimalMetagenome DB](https://doi.org/10.6084/m9.figshare.19728619) — 动物 metagenome metadata 数据记录，链接 project、sample、experiment 和文献；其旧门户当前不可达。
- [AnimalAssociatedMetagenomeDB](https://web.app.ufz.de/aamdb/) — 动物相关 metagenome 的查询、地图、CSV 导出及 reads 下载；使用时注意其历史 release 时间。
- [Animal Microbiome Database (AMDB)](https://www.amdb.online/) — 已发表的动物肠道 16S 整理资源；旧门户当前超时，作为 `legacy` 线索保留。
- [Murine Microbiome Database](http://leb.snu.ac.kr/mmdb/) — 2019 年发表的小鼠 16S 历史整理资源；旧站本轮超时，状态为 `legacy`。
- [AncientMetagenomeDir](https://github.com/SPAAM-community/AncientMetagenomeDir) — 社区维护的古代 metagenome sample/library accession 与论文索引，带版本化发布和 CC BY 4.0；轻量索引而非完整 phenotype 数据库。
- [Online Ancient Genome Repository (OAGR)](https://doi.org/10.4225/55/59ae2d4038294) — 古代人类基因组/微生物组原始及处理数据和 provenance；[Research Data Australia/Adelaide University](https://researchdata.edu.au/online-ancient-genome-repository/1604205) 保留历史 DOI 目录记录，但 [re3data](https://www.re3data.org/repository/r3d100011632) 标注仓库自 2022 年离线，按 `legacy` 作为历史发现入口。

### 食品、发酵和农业相关数据

- [FoodMicrobionet](resources/foodmicrobionet.md) — 食品细菌/真菌 amplicon 研究、食品分类和 BioSample/Run 关系；当前维护页列 v5.1.2。
- [FoodMicroDB](resources/foodmicrodb.md) — 食品来源 16S/18S/ITS 项目、样本、食物分类和 time-series 组成数据。
- [curatedFoodMetagenomicData (cFMD)](resources/cfmd_food_metagenomes.md) — 食品 shotgun metagenomes、curated context、functional/taxonomic profiles 与 MAGs。
- [MicroAgroBiome](resources/microagrobiome.md) — 作物/根际 shotgun 数据和统一 taxonomy/function/MAG/BGC 结果，保留原始 NCBI accession 线索。
- [AgMicrobiomeBase](resources/agmicrobiomebase.md) — UK crop rhizosphere/bulk-soil samples、BioSample/ENA/MGnify links 和 cryobank context；复用前需查看门户及底层 archive 的条款。

### 通用 metadata 注释与 ID 规范化辅助资源

- [MetaSRA](https://metasra.platformx.wisc.edu/) — 对特定公共 RNA-seq/ChIP-seq 样本 metadata 做 ontology 标准化并提供 API/导出；不覆盖 16S 或 shotgun metagenome。
- [MetaHQ](https://github.com/krishnanlab/meta-hq) — 汇聚多个公共 omics 注释来源并提供 CLI，可按 tissue、disease、sex、age、证据层级等提取带来源的注释；不是微生物组专库，也不是输入任意 microbiome accession 的保证型 resolver。

## 微生物知识库与参考数据库

它们可提供疾病关联、物种/基因组参考、功能或菌株背景，通常不能代替宿主样本 metadata。

- [BacDive (Bacterial Diversity Metadatabase)](resources/bacdive.md) — 细菌/古菌菌株 taxonomy、分离来源、培养/表型和序列信息。
- [PLaBAse](resources/plabase.md) — 植物相关细菌菌株、plant sphere、host interaction phenotype、genome 与促生性状；下载维护状态需留意。
- [VagDB](resources/vagdb.md) — 阴道特异性 16S 参考序列集，可用于分类，不是样本 metadata 库。
- [Marine Metagenomics Portal (MMP)](resources/marine_metagenomics_portal.md) — 海洋微生物参考基因组和采样环境/宿主 contextual fields。
- [ODFM](resources/odfm.md) — 发酵食品微生物组学历史数据库；论文所列门户当前无法访问。
- [MicroPhenoDB](resources/microphenodb.md) — 微生物—疾病关联历史知识库；当前官方服务状态未确认，association 不等于样本临床信息。
- [BugSigDB](https://bugsigdb.org/Help:Contents) — 发表研究中微生物组特征/签名的人工整理和导出。
- [Disbiome](resources/disbiome.md) — 疾病—微生物—检测方法/实验与文献关联；公开 JSON experiment API 已返回记录。
- [Expanded Human Oral Microbiome Database (eHOMD)](https://www.homd.org/) — 人类口腔/呼吸道微生物分类、参考基因组和 16S 序列。
- [GIMICA](https://gimica.idrblab.net/ttd/) — 宿主遗传/免疫因子与菌群、疾病的关联数据；页面数据更新时间较早，且许可为保留权利。
- [MiMeDB (Human Microbial Metabolome Database)](resources/mimedb.md) — 2026 年 2.0 版整合人体微生物、代谢物、身体位点、宿主健康/疾病及饮食/暴露知识；不是样本 accession 数据库。
- [gutMDisorder](https://bio-computing.hrbmu.edu.cn/gutMDisorder/browse.dhtml) — 人/鼠菌群与疾病、干预、饮食相关关联知识。
- [gutMGene v2.0](https://bio-computing.hrbmu.edu.cn/gutmgene/) — 微生物—代谢物—宿主基因互作和证据。
- [gutMSNP](resources/gutmsnp.md) — 人体肠道微生物 SNP、参考基因组和表型分层变异模式；项目级表型不能自动下推到单个样本。
- [HRGM2 (Human Reference Gut Microbiome v2)](resources/hrgm2.md) 与 [MRGM (Mouse Reference Gut Microbiome)](resources/mrgm.md) — 人/小鼠肠道微生物参考基因组、分类与功能资源。
- [mOTUs-db](resources/motus_db.md) — 物种层级 mOTU、MAG/基因组、功能注释及环境/研究来源查询；样本来源信息不等于 participant-level phenotype。
- [MicroMap](resources/micromap.md) — 连接 VMH 的微生物代谢模型网络可视化与 Dataverse 发布，不提供常规 BioSample/宿主 metadata。
- Human OncoBiome Database — 2020 年论文描述的癌症微生物组数据集目录；当前第一方服务入口未定位，按 `legacy` 历史线索保留。
- [MOMD (Mouse Oral Microbiome Database)](resources/momd.md) — 小鼠口腔微生物 taxonomy、16S 参考序列和 draft genomes。
- [PanGBank](resources/pangbank.md) — 原核生物 pangenome 图谱与 REST API，用于比较基因组分析。
- [The Microbe Directory](resources/microbe_directory.md) — 多类群微生物的人工整理物种性状和生态 trait 知识库，不是样本/宿主 metadata 库。
- [metaTraits](resources/metatraits.md) — 汇总微生物实测与预测性状，支持 genome/taxon 查询及 community-profile trait 汇总；不能提供人类受试者表型，官网本轮提示 scheduled maintenance。
- [MicrobialScope](resources/microbialscope.md) — 跨细菌、古菌、真菌和病毒 genome accession 的基因组/功能注释、ARG 和下载入口。
- [metagRoot](resources/metagroot.md) — 植物根际微生物蛋白家族、HMM、生态上下文和结构参考；主要对象不是样本 metadata，门户可用性待复核。
- [MetaVR](resources/metavr.md) — 宏基因组病毒序列、vOTU、预测宿主和蛋白簇数据库；官方论文记录 API，本轮服务入口返回访问错误。
- [VirJenDB](resources/virjendb.md) — 病毒序列及其 BioSample/BioProject/SRA accession、host/sample 字段和 metadata schema/API 的 FAIR 平台；字段来源和规范化程度需逐条核查。
- [Iridovirus Comprehensive Database (IVCDB)](resources/ivcdb.md) — 虹彩病毒 isolate/genome 地理分布、宿主范围、core genes 和疫苗/检测知识。
- [ARKbase](resources/arkbase.md) — 优先病原菌参考基因组、curated AST、耐药和毒力背景；细菌药敏表型不是宿主临床表型。
- [AMRnet](resources/amrnet.md) — 部分病原菌的 genome-derived 时空 AMR surveillance 数据和下载面板；不是全微生物组样本库。

## 跨仓库数据发现门户

- [NIAID Data Ecosystem Discovery Portal](resources/niaid_data_discovery_portal.md) — 以感染性/免疫介导疾病研究为主的跨仓库 dataset、resource catalog 和工具索引，可按 disease、organism、data type 等检索并下载 CSV/JSON metadata；它只索引外部来源，不托管底层数据。
- [NFDI4Health Health Study Hub](resources/nfdi4health.md) — 德国临床、公共卫生和流行病学研究 metadata portal/API，含 nutritional-epidemiology schema module；可发现队列和变量，但需另核实菌群 assay、accession 和底层数据权限。

## 文献与补充文件检索

- [Europe PMC](resources/europe_pmc.md) — DOI/PMID/PMCID、摘要/全文链接和文献 API。
- [PMC BioC Supplementary Materials](resources/pmc_bioc_suppl.md) — 帮助发现 PMC 文章补充文件的接口与数据对象。
- 论文检索后，优先查看 Methods、Data Availability、Supplementary Tables 和明确的 accession-to-sample/subject crosswalk；文件被发现不代表其中 ID 已成功映射。

## 工具与标准

- [tools.csv](../catalog/tools.csv)：EDirect、PySRAdb、ffq、nf-core/fetchngs、fastq-dl、ENA Browser Tools、SRA Explorer、Redbiom、MetaSUB `map_collate`、HuMMANet R package、IGS Portal Client、NIAID/NFDI4Health metadata API、PRIME/OmicsMLRepoR/mOTUs client、metaTraits/MetaVR/VirJenDB/AMRnet API、SRA Toolkit、NMDC/JGI/PanGBank/BacDive API 和 MetaHQ CLI 等。工具自身不等于数据库，也不保证上游记录包含缺失的宿主信息。
- [standards.csv](../catalog/standards.csv)：MIxS、STORMS、EMPO、NFDI4Health Metadata Schema、Microbiome Research Data Toolkit 及相关本体/报告规范。
- 字段定义、状态含义和对象粒度见[字段字典](../catalog/schema.md)。

## 按任务选择入口

- **只有 accession：** 先按前缀进入 NCBI/ENA/DDBJ，解析 BioSample、Experiment、Run 关系；再搜索已整理库、论文和补充材料。
- **从研究问题找数据：** 先看[母婴多身体位点指南](guides/maternal_infant_multisite.md)或[CRC 指南](guides/crc_microbiome.md)，再用 `datasets.csv` 按 body site、assay、研究设计和访问模式筛选。
- **要找宿主/临床信息：** 优先核查专题 curated dataset、原始论文、补充表、EGA/dbGaP；检查其信息粒度与样本 crosswalk，避免把队列级信息误当单样本字段。
- **要下载 reads：** 从原始 archive 获取 Run 文件，核实文件大小、许可/访问权限和空间需求；平台分析文件与原始 reads 不是同一数据对象。

