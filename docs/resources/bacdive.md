# BacDive（Bacterial Diversity Metadatabase）

**类型：** 细菌/古菌菌株级知识库　**目录层级：** Extended　**状态：** `active_verified`（核查：2026-11-10）

## 它是什么

BacDive 汇集细菌和古菌菌株层级的标准化信息，官网提供菌株搜索、advanced search、isolation-source search 和 genome browser。可检索 taxonomy、morphology、physiology、cultivation、isolation origin、sequence accessions 等多类字段。官网 2025 release 公告称收录菌株已超过 100,000；具体统计会随版本更新。

## API 与使用

官方 REST API v2 返回 JSON 菌株记录；官网说明自 2026 年 2 月起 API 无需注册。v2 之后续 release 为准，旧 v1 endpoint 保持兼容但不再更新。`catalog/tools.csv` 单列 BacDive API 作为程序化入口。

## 与样本 metadata 的边界

BacDive 的实体是可培养菌株/菌种及其分离来源，不是人群队列的 biological sample。它可帮助解释已发现菌株的培养、来源、taxonomy 和序列背景，但不能直接恢复受试者年龄、饮食、疾病、BioSample/Run 对应或队列级临床表型。

本轮确认了官网、API v2 文档及其公开访问说明，但未实际请求单个 BacDive ID；所以目录状态为 `active_verified`。

## 官方来源

- [BacDive 官网](https://bacdive.dsmz.de/)
- [BacDive API](https://api.bacdive.dsmz.de/)
- [API 字段说明](https://api.bacdive.dsmz.de/strain_fields_information)
- [原始论文，NAR 2025](https://doi.org/10.1093/nar/gkae959)
