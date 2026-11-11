# Meta-virus Resource (MetaVR)

**资源类型：** microbial knowledgebase　**优先级：** extended　**相关性：** indirect　**状态：** `active_partial`　**核查：** 2026-11-10

## 能提供什么

MetaVR 是 IMG/VR 的后续病毒资源，整合环境与 host-associated metagenomes/metatranscriptomes 中发现的 uncultivated viral genomes (UViGs)，并提供 vOTU、病毒分类、预测宿主、蛋白簇、结构预测及序列检索。2026 论文报告 24,435,662 个 UViGs，并描述了 REST API 与 web search。

## 适合什么任务

- 从已有病毒序列、vOTU 或蛋白序列出发检索病毒参考和潜在宿主联系。
- 发现人群相关或环境宏基因组中的病毒多样性与上下文记录。
- 为 virome 研究提供分类、蛋白和 genome catalog 背景。

## 边界与注意事项

- 这是病毒基因组/功能资源，并非 participant-level microbiome metadata 数据库。
- 预测宿主或环境上下文是病毒记录关联，不代表来源 BioSample 的宿主临床变量。
- 本轮官方入口与 API 文档请求返回访问错误；论文所述功能可确认，但当前在线交互/端点状态标为 partial。

## 入口与来源

- [MetaVR Portal](https://www.meta-virome.org/) · [API Swagger](https://meta-virome.org/api/docs)
- [原始论文](https://doi.org/10.1093/nar/gkaf1283)

相关目录行：[`resources.csv`](../../catalog/resources.csv) 中 `metavr`；API 条目见 [`tools.csv`](../../catalog/tools.csv) 中 `metavr_api`。
