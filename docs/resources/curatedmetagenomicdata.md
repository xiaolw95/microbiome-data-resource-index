# curatedMetagenomicData

**类型：** 人工整理的人类微生物组数据包　**目录层级：** Core　**已核查：** 2026-11-10

## 它是什么

curatedMetagenomicData（cMD）是 Bioconductor 数据包，提供人工整理的人类微生物组 sample metadata 以及标准化的宏基因组分类和功能数据，供 R 分析流程加载。2025 年发表的 cMD 3 论文报告包中包含 22,588 个样本、93 项 dataset；论文主分析另外纳入一项 122 样本研究，因此摘要/主分析合计报告 22,710 个样本、94 个 cohort。两种计数口径不可混为同一包内记录数。

## 可提供什么

- 纳入研究中的样本级 metadata；
- 人工整理并经机器校验的 100 余类参与者特征/样本技术字段（论文举例包括 body site、国家、年龄、生活方式、测序信息、健康/疾病信息；每个字段覆盖率不同）；
- 不同 body sites 的 taxonomic abundance、gene families、pathway abundance/coverage 等标准化结果；
- R 中可加载的 SummarizedExperiment/TreeSummarizedExperiment 数据结构。

## 何时使用

若项目或样本已在其研究范围内，可将其作为现有 curated metadata/profile 来源和标准化字段参考；特别适合研究者希望在 R 中复用既有人体 shotgun cohorts。可再用 OmicsMLRepoR 查询对应的 ontology-harmonized cMD metadata。

## 限制

它是纳入研究集合的数据包，不是通用实时 accession 抓取器，也不代表所有已发表数据都能匹配。未纳入的研究仍需从 archive、论文和 supplement 自行发现；比较 metadata 时要记录 package release 和 cohort 版本。包内字段的定义和覆盖率应按列检查，不能仅因论文报告某种信息，就推断每个样本都有该字段。

## 官方来源

- [Bioconductor package](https://bioconductor.org/packages/release/data/experiment/html/curatedMetagenomicData.html)
- [Source repository](https://github.com/waldronlab/curatedMetagenomicData)
- [cMD 3 论文](https://doi.org/10.1038/s41467-025-66888-1)
