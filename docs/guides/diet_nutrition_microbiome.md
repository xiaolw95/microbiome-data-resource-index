# 饮食/营养与肠道菌群数据检索指南

**首轮检索日期：** 2026-11-10　**索引：** [catalog/datasets.csv](../../catalog/datasets.csv)　**主题标签：** `diet` / `nutrition`

## 1. 先区分你要找的是什么

“饮食与菌群数据”可能是以下不同任务：

1. **筛选相关队列：** 查找哪些公开/受控队列同时有 dietary exposure 和 microbiome 数据；
2. **查变量定义：** 了解饮食评估工具、问卷、时间窗口、摄入量编码以及菌群采样时间；
3. **复用样本级饮食值：** 需要 participant/subject ID 与 diet record、specimen/BioSample/Run 的明确 crosswalk；
4. **复用处理结果：** 想下载已经整理好的 16S/shotgun profiles 和样本 metadata；
5. **申请个体数据：** 饮食日志、问卷和临床变量往往比 raw reads 更受限，可能需要伦理、数据使用协议或安全计算环境。

项目介绍、论文队列总表或“研究饮食”的描述只能支持 study/cohort 层结论。没有样本/subject/visit 映射表时，不把 cohort-level diet information 写到每个 BioSample。

## 2. 推荐的检索顺序

1. **先找研究网络和变量：** 使用 [Mica](../resources/mica.md) 搜索 nutrition/gut microbiome studies、变量和 harmonization protocol；同时可查 [NFDI4Health Health Study Hub](https://www.nfdi4health.de/en/service/health-study-hub.html) 的临床/流行病学研究 metadata。两者帮助评估候选队列和变量可比性，不保证数据已公开。
2. **再找 microbiome 样本与 profile：** 对人体 16S，可查 [PRIME](../resources/prime.md)；对人体 shotgun，可查 [Microbiome Repo](../resources/microbiome_repo.md) 和 [curatedMetagenomicData](../resources/curatedmetagenomicdata.md)。它们有各自的 assay/人群范围，且每列字段覆盖率不同。
3. **对特定人群补查队列数据库：** 如日本肠道队列可查 [NIBN JMD](../resources/nibn_jmd.md)，并逐个核对饮食字段是否公开、是否属于相同时间点。
4. **回原论文和 archive：** 找 dietary assessment method、sample collection timeline、SRA/ENA/EGA accession、supplement 和 subject–sample crosswalk；分别保存 Project、BioSample、Experiment、Run、subject、visit 的 ID。
5. **核实权限和数据版本：** 把 raw reads、基础 phenotype、饮食问卷、临床/化验数据分别标注为 public、controlled、request-to-author、secure workspace 或 unavailable。

## 3. 代表候选：Human Phenotype Project（HPP）

2026 年一篇研究报告使用 HPP 的 app-based diet logs 和 shotgun metagenomics 研究 10,068 人的饮食—菌群关联。论文称 raw individual-level gut metagenome data 与 age/sex/BMI 可通过 EGA accession `EGAS00001007204` 获取，其他 HPP 数据需通过项目申请访问；研究代码另在 GitHub/Zenodo 发布。

**当前关键 unresolved：** 论文分析人数是 10,068 participants，但 EGA 当前 Study 页面描述的关联 Dataset `EGAD00001010925` 有 7,190 份粪便 metagenomic samples。两者可能代表总体参与者、具有序列的数据子集或不同数据 freeze；在对照 participant/sample/Run crosswalk 前，不能将 10,068 当作 EGA 可下载样本数，也不能假定 diet logs 与 EGA raw reads 完全一一对应。目录中因此把 HPP 记为 `unresolved` 候选。

| 数据入口 | 当前能确认的内容 | 使用边界 |
|---|---|---|
| [Nature Medicine 2026 论文](https://doi.org/10.1038/s41591-026-04312-x) | 10,068 人、app-based diet logs、shotgun metagenomics 和 diet–microbiome analyses | 10,068 是论文分析人群计数，不应视为当前 EGA dataset 样本数 |
| [EGA EGAS00001007204](https://www.ega-archive.org/studies/EGAS00001007204) | 页面当前列出一个 7,190 粪便宏基因组 Dataset；个体数据需遵循 EGA DAC 流程 | EGA 当前页面名称/关联论文与 2026 论文使用关系需要进一步对照；未解析 count discrepancy |
| [HPP Data Access](https://humanphenotypeproject.org/data-access) | 可联系项目方申请其他 HPP 数据，官网列 secure research environment | 论文称部分数据仅向合格研究者、非商业目的提供；需单独确认 diet-log 的具体条款 |
| [研究代码](https://github.com/TmrSegev/diet-microbiome) / [Zenodo archive](https://doi.org/10.5281/zenodo.18959226) | 代码与分析版本 | 代码可复用不代表数据可公开下载 |

该例说明：检索工具应同时保留论文报告计数、archive dataset 计数、accession、访问条件和 unresolved 状态，而不是只产出一个拼接后的 metadata 表。

## 4. 主题检索词

- **研究与暴露：** diet, dietary intake, dietary pattern, food frequency questionnaire, 24-hour recall, diet log, food processing, nutrition, nutrient intake, supplementation；
- **菌群与检测：** gut microbiome, gut metagenome, 16S, shotgun metagenomics, stool, faecal/fecal；
- **人群与设计：** cohort, longitudinal, repeated measures, intervention, case-control；
- **数据和映射：** supplementary table, sample manifest, subject ID, participant ID, visit, BioSample, SRA Run, EGA.

建议先从 Mica、PRIME、Microbiome Repo、NIBN JMD 等主题/人群资源发现候选，再用 `ENA/NCBI/EGA + 论文/补充表` 回溯，避免只靠关键词检索遗漏资源内部 ID。

## 5. 可交付的筛选结果

每个候选至少记录：研究题目、论文 DOI/PMID、公开 archive accession、样本材料和 assay、论文报告人数及单位、archive BioSample/Experiment/Run 数、diet assessment 工具和时间窗、提供 diet 值的文件/字段、subject/sample crosswalk、数据权限、发布日期/freeze、证据链接以及 unresolved 项。不要把研究总体的生活方式描述复制成逐样本值。
