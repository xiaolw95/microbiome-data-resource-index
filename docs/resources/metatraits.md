# metaTraits

**资源类型：** microbial knowledgebase　**优先级：** extended　**相关性：** indirect　**状态：** `active_partial`　**核查：** 2026-11-10

## 能提供什么

metaTraits 将 BacDive、BV-BRC、JGI IMG/GOLD 的培养/实验性状与 proGenomes、SPIRE 等来源的基因组预测性状统一到 NCBI/GTDB 分类体系。官网报告覆盖 220 多万个基因组与 140 多项 harmonized traits，包含形态、生理、代谢、环境偏好和生活方式类别，并提供 genome lookup、taxon-level summaries、porTraits genome annotation、sumTraits community profile annotation、批量下载和 JSON API。

## 适合什么任务

- 为已知菌名、taxonomy ID、genome accession 或 MAG 添加微生物自身的性状背景。
- 从 taxonomic profile 估计/汇总社区层面的 trait 分布。
- 沿 trait 来源链接追溯实验观察与预测模型。

## 边界与注意事项

- 这里的“trait”是微生物物种/基因组性状，不是人类受试者的年龄、饮食、性别或健康状况。
- 汇总可能同时含实测与预测结果；官网将预测值标为 AI/prediction，并提示百分比不是置信度，少于 85% 共识时不强行给单一结论。
- 本轮官网提示 scheduled maintenance，故资源和 API 暂记 `active_partial`；使用时需确认接口恢复及响应版本。

## 入口与来源

- [metaTraits 官网](https://metatraits.embl.de/) · [Documentation / API](https://metatraits.embl.de/documentation) · [Traits catalog](https://metatraits.embl.de/traits)
- [原始论文](https://doi.org/10.1093/nar/gkaf1241)

相关目录行：[`resources.csv`](../../catalog/resources.csv) 中 `metatraits`；API 条目见 [`tools.csv`](../../catalog/tools.csv) 中 `metatraits_api`。
