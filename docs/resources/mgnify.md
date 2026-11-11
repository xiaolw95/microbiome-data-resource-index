# MGnify

**类型：** 微生物组数据浏览、分析平台和 API　**目录层级：** Core　**已核查：** 2026-11-10

## 它是什么

MGnify 将 ENA Study 中提交到其流程分析的研究与样本、Runs、assemblies 和分析结果相连。提供可检索网页和 REST API；API 当前文档列出 studies、samples、runs、biomes 和 analyses 等资源。

## 可提供什么

- ENA 来源的样本 metadata 和 BioSamples 链接；
- 研究中相关 sample/run/analysis 的关系；
- 依数据类型和流程版本提供 QC、taxonomy、功能注释、assembly/MAG 等结果；
- 部分样本的 ELIXIR Contextual Data Clearing House 补充/修正；
- Europe PMC/EMERALD 提供的论文文本挖掘 annotation。

## 何时使用

输入 ENA/Sample/Study ID 或研究名后，检查是否已有 MGnify 分析及可复用结果；API 可用于程序化查询关联对象。它也可作为 metadata 的第二来源，需保留数据实际来源是 ENA、BioSamples、CCH 还是论文 annotation。

## 限制

论文 annotation 可能补充 archive 中没有的线索，但 MGnify 明确指出无法自动且有把握地确定 annotation 对应的具体样本。不能把 publication-level annotation 写成 BioSample-level 值，除非另有明确 crosswalk。

## 官方来源

- [MGnify Portal and Metadata](https://docs.mgnify.org/src/docs/portal.html)
- [MGnify REST API v2](https://docs.mgnify.org/src/docs/api.html)
- [MGnify API](https://www.ebi.ac.uk/metagenomics/api/v2/)
