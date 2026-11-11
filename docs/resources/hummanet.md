# HuMMANet

**全名：** Human Microbiome Metabolome Annotation Network　**资源类型：** 配对肠道 microbiome–metabolome 整理数据集与 R/Bioconductor 数据包　**当前状态：** `active_verified`　**核查日期：** 2026-11-10

## 能提供什么

HuMMANet 聚合已发表、同时具有肠道微生物组与宿主代谢组数据的跨研究样本。2026 年 preprint 与 Zenodo v1 记录报告 46 个 paired studies、59 个 study-units、14,405 个样本，涵盖 13 个疾病类别和健康/对照组。其 R/Bioconductor 包按研究提供 sample metadata、microbial species profiles、原始和 harmonized metabolite profiles，以及代谢物 ID、pathway、microbial producer、疾病和药物相似性注释。

## 怎么检索和使用

- 先在 [Zenodo 数据记录](https://zenodo.org/records/22053943)查看版本、文件和引用信息。
- [HuMMANet R 包](https://bioconductor.org/packages/HuMMANet) 可枚举 study、查看可用 modality，并加载单个研究或指定的 metadata/omics 数据块。
- 包说明以 study identifier 作为主要入口；样本级 metadata 与相应 profile 在 study bundle 中对齐。

## 适合的任务

- 从头发现有 paired microbiome/metabolome、疾病分层或特定 specimen matrix 的公开研究。
- 找可用于 microbiome–metabolite 关联、跨研究 harmonization 或方法评估的样本级数据包。
- 以 study-specific metadata 查看样本标识、subject annotation、临床协变量、时间点和身体位点。

## 边界

- HuMMANet 是范围明确的 paired gut microbiome–metabolome compendium，不是通用样本 accession 查询服务。
- 其 preprint 说明来源数据不按 HuMMANet 统一重新分发；应回到各来源研究和 archive 核实原始数据、权限与许可。
- `study-unit`、样本、受试者和重复时间点不可混为一个样本数。具体 ID 映射要按研究包单独审查。
- 当前核查到的是 2026 年 preprint、Zenodo 记录和公开代码/包文档；应随正式发表及后续 package release 更新版本状态。

## 来源

- [Zenodo v1 数据记录](https://doi.org/10.5281/zenodo.22053943)
- [HuMMANet GitHub / 使用文档](https://github.com/ShivangiV-IIITD/HuMMANet)
- [HuMMANet bioRxiv preprint](https://doi.org/10.64898/2026.08.24.746727)
