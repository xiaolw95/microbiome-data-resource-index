# Microbiome Datahub

**类型：** INSD 环境宏基因组项目与基因组 metadata 检索平台；**目录层级：** Core；**状态：** active_verified（官方手册/API 说明更新于 2026-03）

官方手册支持按环境、host taxon 和关键词筛选 INSD shotgun metagenome BioProjects，下载 TSV project metadata，并通过 BioProject accession 获取项目 metadata；还提供 genome/MAG 搜索、下载和 MEO environment annotations。手册列出 102,174 个项目记录与 218,653 个 genome entries。

**适用：** 从生态环境、宿主类群和关键词发现 metagenome 项目，与 MGnify、SPIRE、GOLD、NMDC 并行检索后回到 archive 核对。

**限制：** 项目和 genome 条目数不是 BioSample 或参与者数量；项目级环境信息不能直接赋给项目中的每个样本。inferred phenotype 是基于 taxonomy 的预测，不等同实验验证 phenotype。

**来源：** [官网](https://mdatahub.org/) · [官方手册](https://mdatahub.org/document/) · [下载 API 手册](https://mdatahub.org/apimanual) · [项目查询](https://mdatahub.org/projects)
