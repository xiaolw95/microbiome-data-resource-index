# mOTUs genome database (mOTUs-db)

**类型：** 微生物参考基因组与分类背景数据库　**目录层级：** Extended　**状态：** `active_verified`　**已核查：** 2026-11-10

## 它是什么

mOTUs-db 是与 mOTUs taxonomic profiler 配套的原核生物基因组资源。数据库论文报告 124,295 个 species-level mOTUs，由约 2.83 million 个 MAG 和 919,090 个 isolate/single-cell genomes 构成；MAG 来自 117,902 个样本、70 余种 habitat。官网当前介绍数据库覆盖 50 余种环境。数据库适合查看 taxonomic profile 中某个 mOTU 的 genome-resolved 背景。

## 可提供什么

- 按 genome、mOTU、taxonomy、study 等对象检索与筛选；
- 下载 genome sequence、annotation 和选定记录摘要；
- 查看环境分布和采样地点；基因组注释包括 KEGG、Pfam、eggNOG 等；
- 通过配套 mOTUs CLI 对 reads 进行 taxonomic profiling，或按 mOTU/taxonomy 下载匹配 genomes。

## 适用场景与边界

适合做原核生物参考基因组检索、物种层级 profiling 解释、MAG 与环境分布查询。Study/sample 关联可以提供来源和生态背景线索，但它不是人体参与者 metadata 数据库，不能预期取得年龄、生活方式、疾病或饮食问卷；样本级使用要另行追踪原始研究和 archive accession。

官网称数据采用 CC BY 4.0。大批量检索可用官方 mOTUs profiler/下载命令；具体 API 和数据库版本以[官方文档](https://motus-tool.org/database/index.html)为准。

## 官方来源

- [mOTUs-db](https://motus-db.org/)
- [mOTUs database 论文](https://doi.org/10.1093/nar/gkae1004)
- [mOTUs profiler GitHub](https://github.com/motu-tool/mOTUs)
- [数据库文档](https://motus-tool.org/database/index.html)
