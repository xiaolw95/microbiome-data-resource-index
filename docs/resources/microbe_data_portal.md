# MICROBE Data Portal

**类型：** 项目样本与外部数据库关联的平台/API；**目录层级：** Extended；**状态：** active_partial；**已核查：** 2026-11-11

MICROBE Data Portal 面向 MICROBE 项目收集和生成的 samples/datasets。官方首页本轮显示 4,353 个 samples，并提供 API 与使用文档入口；链接的仓库包括 ENA、BioSamples、MetaboLights 和 MGnify。公开代码说明门户缓存并整合外部样本 metadata、测序数据 availability 和 analysis/catalogue links。

**适用：** 对 MICROBE 项目样本 accession 查询 BioSamples/ENA/MGnify 关联；参考其将外部 archive metadata 汇入一个项目门户的实现方式。

**限制：** 这是单个项目的门户，不是面向全领域的微生物组数据库。本轮确认门户首页和 API/docs 入口可见，但没有调用 API，也未核实完整结果分页或逐样本 crosswalk，因此维持 active_partial。门户代码仓库不等于当前在线服务 SLA。

**来源：** [官方门户](https://data.microbeproject.eu/) · [官方代码与文档](https://github.com/EBI-Metagenomics/microbe-data-portal)
