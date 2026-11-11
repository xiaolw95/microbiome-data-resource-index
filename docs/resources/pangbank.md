# PanGBank

**类型：** 原核生物泛基因组数据库与 API　**目录层级：** Extended　**状态：** `active_verified`（核查：2026-11-10）

## 它是什么

PanGBank 提供按 GTDB species clusters 组织的预计算原核生物泛基因组图。初版论文报告覆盖超过 4,600 个物种、超过 393,000 个基因组，来源包括 isolate genomes、MAGs 和 single-cell amplified genomes。平台提供 Web 界面、REST API、CLI 和下载。

## 何时使用

适合做广谱原核生物 comparative genomics、gene family partition、genomic plasticity 和功能模块分析。若检索问题是“某个菌是否在哪类环境出现”，可从相关 genome collection 的背景标签获得线索，再沿原 genome/sample accession 回到 archive。

## 与样本 metadata 的边界

PanGBank 的核心对象是 genome、gene family、species cluster 和 pangenome，不是 BioSample、受试者、疾病队列或饮食信息表。它属于本目录中的间接支撑资源，不会替代样本/研究 metadata 检索。

## 官方来源

- [PanGBank 官网](https://pangbank.genoscope.cns.fr/)
- [REST API 和使用说明](https://pangbank.genoscope.cns.fr/about/)
- [API 源代码](https://github.com/labgem/PanGBank-api)
- [原始论文，NAR 2026](https://doi.org/10.1093/nar/gkag948)
