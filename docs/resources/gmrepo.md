# GMrepo v3

**类型：** 人类肠道疾病微生物组 curated database　**目录层级：** Core　**状态：** active_verified（核心查询/下载文档已核；交互端未实测）

## 它是什么

GMrepo v3 是以人类肠道微生物组和疾病表型为中心的整理数据库/分析资源。近期论文描述了扩展后的疾病覆盖、跨研究 biomarker 分析，以及从公开 BioProject 和文献候选发现、人工确认与 metadata curation 的流程。

## 可提供什么

- 已收录的人类肠道研究和样本；
- 16S/WGS 相关数据、疾病/对照标签和微生物组 profile（以当前 release 为准）；
- 论文与公共归档链接、跨研究比较入口。
- 官方文档描述了按 NCBI/ENA Run/Sample ID 搜索、按项目查看 runs，以及下载全部项目元数据和项目级 run 表的路径。

## 何时使用

可作为 CRC 等肠道疾病主题的候选数据集发现和交叉核验来源。查到项目后仍需回到论文、BioSample/Run 和补充表，确认样本单位、纳入标准和病例/对照映射。

## 限制

资源范围以人类肠道为主；不能推断所有候选 accession 均被收录。疾病标签和样本数需依赖具体版本及其 curation 依据。官方文档与 v3 论文确认查询/下载设计，但本轮未逐项实测文件下载或 accession crosswalk；优先将其作为候选发现和交叉核验来源。

## 来源

- [GMrepo v3 paper](https://doi.org/10.1093/nar/gkaf1190)
- [GMrepo website](https://gmrepo.humandbs.org/)
- [Official help and data downloads](https://gmrepo.humangut.info/help)
- [Official usage documentation: find a run/sample](https://evolgeniusteam.github.io/gmrepodocumentation/usage/findrunandsample/)

The v3 paper describes curated sample metadata, taxonomic profiles, and microbial marker downloads. Official usage documentation describes run/sample ID lookup and project/run downloads. The current portal could not be interactively inspected during this review, so check the live release page and file documentation before selecting a dataset or relying on a count.
