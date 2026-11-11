# AMRnet

**资源类型：** curated dataset / AMR surveillance dashboard　**优先级：** extended　**相关性：** supporting　**状态：** `active_verified`（公开 TSV/S3 下载已由官方文档确认；API 需要免费注册密钥）　**核查：** 2026-11-11

## 能提供什么

AMRnet 将公共细菌基因组数据整理成病原体 AMR surveillance 数据集和交互式地图/趋势面板。官方文档明确提供每个 organism 页面免注册 TSV 下载，以及每周更新的公开 S3 CSV 快照；REST API 位于 `api.amrnet.org`，需免费注册取得 API key。记录包含国家、年份、基因型/lineage、AMR marker、耐药预测，以及 organism-specific 信息。

## 适合什么任务

- 从病原体与抗菌药物耐药问题出发，探索公开基因组的时空流行趋势。
- 查找经过整理的病原体 genome accession 和耐药标记/预测。
- 将特定菌株的耐药基因组背景作为感染或 One Health 研究的辅助线索。

## 边界与注意事项

- AMRnet 是有限病原体范围的 genomic surveillance data product，不是通用微生物组样本库。
- 国家、年份、pathotype 和 AMR marker 不能替代参与者年龄、饮食、健康问卷或病人结局。
- 官网主体为 JavaScript 应用；本轮核实官方数据访问文档，未实际下载 TSV/S3 文件或调用 API。若仅需公共快照可不认证，使用 API 则需 API key。

## 入口与来源

- [AMRnet dashboard](https://www.amrnet.org/) · [official data access documentation](https://amrnet.readthedocs.io/en/latest/data.html) · [REST API docs](https://api.amrnet.org/api-docs)
- [原始论文](https://doi.org/10.1093/nar/gkaf1101)

相关目录行：[`resources.csv`](../../catalog/resources.csv) 中 `amrnet`；API/快照条目见 [`tools.csv`](../../catalog/tools.csv) 中 `amrnet_api`。
