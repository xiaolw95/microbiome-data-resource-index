# MicrobiomeDB

**类型：** 微生物组数据发现与分析平台　**目录层级：** Extended　**状态：** `active_partial`（核查：2026-11-10）

## 它是什么

MicrobiomeDB 将研究的样本描述、微生物群落数据和可视化分析工具放在一起，目标是让用户按实验 metadata 查询已收录研究。官方说明称样本字段会映射到 MIxS；不匹配的原始字段经人工整理后进入自定义 ontology，并可用浏览器内分析应用查看查询结果。

## 可提供什么

- 研究和样本层级的实验 metadata 与 taxon abundance；
- 按样本属性构造查询，并在 Shiny 应用中探索结果；
- 公开 study 的处理后数据。MicrobiomeDB 37（2024 年 5 月）公告增加了 93 项 shotgun 研究、超过 22,000 个样本。

## 使用限制

旧版论文主要描述 16S 工作流；2024 年 release 公告补充了 curatedMetagenomicData 的 shotgun studies。当前首页可访问，但本轮浏览器抽取显示研究表初始化失败，因此不能据此声称现行交互查询已经完整可用；API、最新可下载数据和逐 accession 映射仍待直接测试。它只覆盖平台已加载的研究，不是公共 archive 的全量镜像。

## 官方来源

- [MicrobiomeDB 首页](https://microbiomedb.org/mbio/app)
- [官方 About：metadata 与查询机制](https://microbiomedb.org/mbio/app/about)
- [Release 37 公告](https://microbiomedb.org/mbio/app/static-content/MicrobiomeDB/news.html)
- [原始论文，NAR 2018](https://doi.org/10.1093/nar/gkx1027)
