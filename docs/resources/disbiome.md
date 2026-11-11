# Disbiome

**类型：** 微生物—疾病关联知识库　**目录层级：** Extended　**状态：** active_verified

## 它是什么

Disbiome 汇总研究中报道的疾病与微生物丰度差异关联，支持按疾病、微生物或检测方法搜索，并提供实验结果和文献线索。它是文献证据的关联知识库，不是原始测序归档，也不是 BioSample accession 查询服务。

## 可提供什么

- 疾病、微生物分类名称和关联研究；
- 提升/降低等定性结果、病例/对照 abundance 信息、检测方法和文献引用；
- 公开 JSON endpoint 中的 experiment、disease、organism 和 publication 记录。

## 使用方式

可以在[官网](https://disbiome.ugent.be/)按 disease、organism 或 detection method 搜索；程序化访问可从[官方导出说明](https://disbiome.ugent.be/export)查看 JSON 路径。本轮对 `https://disbiome.ugent.be:8080/experiment` 和 `/disease` 做了只读请求，均返回 HTTP 200。

## 限制

- 记录粒度是文献/实验关联，而不是逐个 biological sample；
- 关联方向或 abundance 信息不能直接映射成某个 accession 的样本属性；
- 数据库受使用条款和数据库权利约束，商业再利用前需核实许可；
- 不能代替论文方法、supplement 或具体 participant/sample crosswalk。

## 官方来源

- [Disbiome 官网](https://disbiome.ugent.be/)
- [帮助页](https://disbiome.ugent.be/help)
- [JSON 导出与 API 说明](https://disbiome.ugent.be/export)
- [2018 BMC Microbiology 论文](https://doi.org/10.1186/s12866-018-1197-5)
