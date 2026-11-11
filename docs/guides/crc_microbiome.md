# CRC 微生物组数据集检索指南

**首轮检索日期：** 2026-11-10　**索引：** [catalog/datasets.csv](../../catalog/datasets.csv)　**主题标签：** crc

## 1. 研究问题拆分

“CRC 微生物组数据”至少包含不同的可检索任务：

1. **粪便病例–对照：** CRC、腺瘤、健康/对照分开标记；常见 16S 或 shotgun。
2. **肿瘤组织与邻近正常组织：** 关注配对病人和明确的组织位点，可有 16S、shotgun、RNA/DNA 深度测序。
3. **肿瘤阶段、位置或转移：** 需要 stage、肿瘤左右侧、转移状态等临床字段及样本级映射。
4. **跨研究汇总：** curated metadata 和标准化丰度适合候选发现与复用，但需检查纳入规则、污染标记和项目间批次。

## 2. 纳入/排除标准

### 纳入

- 人类 CRC 或 colorectal adenoma 相关微生物组研究；
- 可追溯到论文/正式数据资源以及项目 accession 或公开下载文件；
- 能确认样本材料（stool、tumor、adjacent normal、其他 mucosa 等）和 assay 类型；
- 临床 metadata 的具体字段和范围按来源记录；若只有论文队列统计，保持 study/cohort scope。

### 分开标注或排除

- adenoma、CRC、healthy control 不能合成一个疾病标签；
- feces 与 tumor tissue、adjacent normal、blood、oral 等 body sites 分开；
- DNA/RNA、16S/shotgun、metatranscriptomics 不混成同一测序类型；
- 无法找到论文或数据来源的关键词命中先标 candidate/unresolved，不标成已验证公开数据集；
- 只在二次分析中出现的样本数不能归给单个 accession，需保留原始研究数、纳入数、处理后数的差别。

## 3. 检索词和资源组合

在 NCBI SRA/BioProject、ENA/DDBJ、Europe PMC/PMC、curatedMetagenomicData、Microbiome Repo 及相应专题文章中组合以下术语：

- colorectal cancer OR CRC OR colorectal neoplasia OR adenoma
- microbiome OR microbiota OR metagenom* OR 16S
- stool OR feces OR faeces OR tumor OR tumour OR mucosa OR adjacent normal

检索路径建议：

1. 如果需求是跨研究粪便 shotgun，先查 [curatedMetagenomicData](https://bioconductor.org/packages/release/data/experiment/html/curatedMetagenomicData.html)、[CRC public stool compendium](https://doi.org/10.57745/7IVO3E) 和 [Microbiome Repo](https://microbiomerepo.com/)；
2. 如果需求是具体公开原始数据，用 project accession 回到 NCBI/ENA，并从 BioSample 找每份 specimen 的字段；
3. 如果需求是配对肿瘤/邻近组织，重点核对 sample ID/患者 ID 和文件名的对应表；
4. 如果要 stage、治疗、转移、饮食/生活方式等字段，检查 supplement/临床表以及 dbGaP、EGA 等受控入口；公开 reads 不代表临床表开放。

## 4. 首轮候选及适用任务

| 候选 | 适合的检索任务 | 已核实的数量/访问口径 | 关键信息与限制 |
|---|---|---|---|
| [CRC public stool shotgun compendium](https://doi.org/10.57745/7IVO3E) | 从头找跨国家 stool shotgun CRC/adenoma/control；获取整理 metadata 和 profiles | 2,340 stool specimens；15 cohorts、14 public BioProjects、10 countries | 提供样本关联 metadata、taxonomy/species、function/strain profiles。资源注明污染质控和未报告健康状态样本处理；reads 仍在各自归档，不是单一 raw project。[资源页](https://entrepot.recherche.data.gouv.fr/dataset.xhtml?persistentId=doi:10.57745/7IVO3E) |
| [Colobiome / PRJEB35990](https://www.ebi.ac.uk/ena/browser/view/PRJEB35990) | 组织 swab、邻近健康组织和 stool 的 CRC 16S | 508 SRA Experiments + 508 BioSamples（归档登记数） | 不是 508 位患者；逐患者配对关系需要核对 BioSample/补充表。[项目描述](https://www.ncbi.nlm.nih.gov/bioproject/PRJEB35990) |
| [AC-ICAM](https://pmc.ncbi.nlm.nih.gov/articles/PMC10202816/) | 肿瘤–邻近正常组织配对 16S；连接免疫、临床和 host omics | 246 个配对患者 = 492 个 16S specimens；另有 42 个 tumour-only specimens；另含 167 个 tumour WGS 样本 | 16S 与 WGS 的开放/受控状态不同；16S 与 WGS 子集不能混合计数。样本文件命名保留 patient/tissue 信息，部分 host genomics 在受控访问下。论文报告队列年龄、性别和 stage 等，但样本表需单独核查。 |
| [FFPE adenoma/carcinoma 5R 16S / PRJNA1476454](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA1476454) | 腺瘤 vs CRC 肿瘤组织 | 论文 50 tissue specimens；另 4 个公开 sampling negative controls，SRA/BioSample 合计 54 记录 | 10 个 DNA extraction/PCR negative controls 需向作者申请；论文称其余 FASTQ 在 SRA。阴性对照不能作为患者样本。[论文](https://www.frontiersin.org/journals/microbiology/articles/10.3389/fmicb.2026.1880194/full) |
| [PRJNA943491](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA943491) | 健康/肿瘤 colorectal tissue 的细菌和病毒 DNA/RNA | 论文 10 CRC + 10 matched controls；NCBI 40 BioSamples/Experiments | 40 条归档记录不等于 40 位参与者或 40 个 unique specimen；论文数据可用性描述为对齐的非人 reads，具体 assay 与样本 crosswalk 仍需查补充材料。[论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC10557870/) |
| [CRC pooled shotgun 18 cohorts](https://pmc.ncbi.nlm.nih.gov/articles/PMC12283368/) | disease stage、左右侧肿瘤位置、strain-level 跨队列分析 | 3,741 stool metagenomes：2,116 来自 12 个已有公共队列，1,625 来自 6 个新队列 | MetaPhlAn 4/HUMAnN 3.6 profiles 和 metadata 在 [Zenodo 10.5281/zenodo.15069068](https://doi.org/10.5281/zenodo.15069068)。新队列 reads 分布在四个 ENA 项目、NHSII PRJNA1237248 和 PRJNA1167935；3,741 不能归到任一单个项目。[数据可用性](https://pmc.ncbi.nlm.nih.gov/articles/PMC12283368/) |
| [公共 V4 16S 二次分析 cohort set](https://www.nature.com/articles/s41467-021-23265-y) | 病例/对照和 adenoma 的 16S V4 原始数据发现 | 4 个 discovery BioProjects + 2 个 validation projects；当前不合并样本数 | accession 包括 PRJNA389927、PRJEB6070、PRJNA290926、PRJNA362366、PRJNA534511、PRJNA280026。这些不是一项 study 的统一队列；各项目 counts、纳入排除和 metadata 需分别核对。 |

候选及状态也见 [catalog/datasets.csv](../../catalog/datasets.csv)。表中的数量保留来源口径：论文参与者、specimens、BioSamples、Experiments、Runs 和二次分析纳入数不互换。

## 5. 把需求映射到数据集的快速规则

| 用户问题 | 首选入口 | 下载/使用前检查 |
|---|---|---|
| CRC/adenoma/对照 stool shotgun，想要整理 profiles | CRC stool compendium、curatedMetagenomicData、18-cohort meta-analysis | disease label、study ID、是否包含重复/污染样本、metadata 字段及 profiles 版本 |
| CRC tumor 与 adjacent normal 组织的配对 16S | AC-ICAM、Colobiome | 一位患者是否有成对记录；每个 BioSample 是否可映射 tissue type；排除仅 tumour-only subset 时的设计差异 |
| 腺瘤与癌组织差异 | FFPE 5R 16S 等 tissue studies | 组织学分组和阴性对照；样本数、是否配对、临床协变量是否能对应 |
| CRC stage 或肿瘤左右侧 | 18-cohort meta-analysis 与其 Zenodo metadata | stage/location 在新队列中较细，但并非所有旧队列都有相同覆盖；按 study 分层后再分析 |
| 细菌/病毒以及 DNA/RNA 活性 | PRJNA943491 | 确认提供的是原始 reads 还是去人源/对齐后 reads；DNA/RNA 库与组织 specimen 的 crosswalk |

## 6. 样本 metadata 核查规则

- **疾病：** 保留 CRC、adenoma、healthy/control 的来源标签；核实定义和病理诊断，不仅凭项目题名。
- **位点：** stool、tumour、adjacent normal、mucosa、metastasis 等逐项保留；不能把组织样本当作 gut stool。
- **临床字段：** age、sex、stage、site, MSI、treatment 等可能只在患者或论文队列层出现。只有明确的 subject/specimen ID mapping 才下推至样本行。
- **计数：** 对 raw archive 单独记录 BioSample/Experiment/Run；对研究文章分别记录入组人数、采集 specimens、分析样本和 QC 后样本。
- **访问：** 区分开放 SRA/ENA、controlled dbGaP/EGA、申请作者和仅公开处理结果；不把开放 accession 当作完整 metadata 开放证明。

## 7. 局限与下一轮扩展

此清单是经过多来源交叉发现的一轮样板，而非 CRC 所有公开项目的穷尽目录。后续可按 assay 和 sample type 拆分更多专题页（例如 CRC fecal 16S、CRC stool shotgun、肿瘤组织、肝转移、多组学、CRC 饮食/生活方式队列），并对 SRA/ENA 的 BioSample 和 supplement 逐样本核查。若样本级临床 crosswalk 不公开，应标明限制，而非推断或尝试绕过访问控制。
