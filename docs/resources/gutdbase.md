# gutDBase

**类型：** 肠道疾病多组学整理数据库与浏览平台　**目录层级：** Extended　**状态：** `active_verified`（官方 2026 NAR 论文确认 browse/search/download 能力；门户未逐项实测）

## 它是什么

gutDBase 是 2026 年 11 月发表的肠道疾病资源，整合 15 类 gut-related disease 中来自 161 篇研究的 175 个 bulk RNA-seq、single-cell RNA-seq 和 microbial datasets。其范围同时包括人和小鼠，关注宿主转录组、微生物组成及宿主–微生物关联。

## 可提供什么

- 按疾病和数据类型浏览整理研究；
- 查看微生物组成、alpha/beta diversity、LEfSe 和 host-microbe correlation；
- 查询跨研究差异表达基因和差异微生物；
- 下载部分 gene-expression profiles、差异表达结果与细胞标记数据；论文描述 Search 与 Download 页面及相关数据对象。

## 何时使用

适合从肠道疾病机制或 host–microbe interaction 问题出发，发现对应的转录组/微生物组研究并查看已处理结果。若用户需要原始微生物测序 accession、具体 BioSample 对应关系或补充表中的宿主特征，需沿数据集记录回原论文和 archive 核实。

## 限制

gutDBase 面向有限的肠道疾病、多组学数据集合，不是公共 SRA/ENA 项目的全面目录，也不是通用样本 ID metadata resolver。官网为 JavaScript 应用；官方论文确认核心功能，但本轮未逐项测试下载文件、ID crosswalk、许可和 API。

## 来源

- [gutDBase 官网](https://bio-computing.hrbmu.edu.cn/gutDBase/)
- [2026 NAR 论文与数据库说明](https://doi.org/10.1093/nar/gkag1136)
- [分析代码](https://github.com/liangcheng-hrbmu/gutDBase) · [Zenodo 记录](https://doi.org/10.5281/zenodo.22901200)
