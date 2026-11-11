# NFDI4Health Health Study Hub

**类型：** 临床/流行病学研究 metadata portal 与 REST API　**目录层级：** Extended（德国健康研究发现）　**状态：** `active_verified`　**已核查：** 2026-11-10

## 它是什么

NFDI4Health Health Study Hub 是德国临床、公共卫生和流行病学研究的 FAIR metadata 目录。它聚合 DRKS、ClinicalTrials.gov、WHO ICTRP 等公开注册信息，也收录数据持有者提交或由 data stewards 收集的研究描述、变量、文件和访问权信息。研究 metadata 可用网页或 API 检索；这不是统一存储所有研究个体数据的仓库。

## 对菌群和饮食研究的价值

- 从德国健康研究和营养流行病学研究出发查找 study、substudy、data collection、变量及相关研究文件；
- 根据公开 metadata 做语义检索，部分记录可探索到 variable/item level；
- 其 NFDI4Health Metadata Schema 有 nutrition/epidemiology 等定制模块，营养模块描述 dietary assessment instruments，另有 record-linkage、数据访问、设计和人群信息；
- 可与 [Mica](mica.md) 互补：NFDI4Health 范围更广，Mica 更聚焦参与 INTIMIC 的营养—肠道菌群观察研究和 harmonization initiatives。

## 限制

- 它是 health-study metadata portal，不是微生物组专库；检索到营养/流行病学研究后，还需确认是否实际含 microbiome assay 和样本 accession。
- Portal 中的 study metadata 可公开检索，但底层数据能否下载、申请或联邦分析依项目 owner 和伦理/法律许可而异。
- Health Study Hub API 的公开文档提供 `POST /api/resources/` 搜索入口；本目录没有实际提交 API 查询，也没有确认任意研究 ID 到 BioSample/Run 的映射。
- 目录只保留索引和 schema 链接，不复制 study files、问卷或受限数据。

## 官方来源

- [Health Study Hub overview](https://www.nfdi4health.de/en/service/health-study-hub.html)
- [Health Study Hub portal/API](https://health-study-hub.de/api/docs/)
- [OpenAPI schema](https://health-study-hub.de/api/openapi.yaml)
- [NFDI4Health Metadata Schema](https://www.nfdi4health.de/en/service/metadata-schema.html)
- [Frequently Asked Questions](https://www.nfdi4health.de/en/service/health-study-hub/frequently-asked-questions.html)
