# Microbiome Repo

**类型：** Study registry + human shotgun curated catalog + evidence-linked releases；**目录层级：** Core；**已核查：** 2026-11-11

## 当前版本信息
官方文档标示 release R2026.36、data package 1.30.0（2026-11-06）。当前 curated catalog 有 5,052 个项目和 806,054 条样本记录；分开的 registry 列出所有已筛查 public studies，范围和数量与 curated catalog 不同。这里的样本数字不是独立受试者数。

## 能提供什么
- 项目/样本/Run accession、逐字段 metadata、证据摘录、来源路线、信息层级和 confidence；
- archive、论文、补充表、accession mapping、冲突和 coverage 记录；
- 页面可按研究主题、干预、疾病、年龄类别等查找项目；静态 JSON/CSV 和 Parquet 下载入口可用于程序化读取；
- Parquet/CSV/SQLite 等版本化数据包，具体以下载页为准。单项目 API 返回的样本表适合先检查命中研究，不必一开始下载全量表。

## 对本项目的价值
这是目前最接近“识别候选研究，再按 archive、论文和补充表逐字段保留证据”的实践。年龄、性别、疾病、country、抗生素暴露、body site、subject/timepoint 等的覆盖依实际来源而不同。可参考 registry→paper link、精确 ID join、逐字段 evidence、冲突记录和版本化交付。API 文件与字段语义以 [For LLMs & API](https://microbiomerepo.com/llms/index.html) 及当前 release 为准。

## 限制
它是 human-associated shotgun DNA/RNA 的限定目录，不覆盖所有 16S、assay、宿主或发表研究。其证据路线和置信度可帮助复核，但不能消除错配风险；使用时应确认 release 纳入范围、证据来源和上游引用。

## 来源
- [About and scope](https://microbiomerepo.com/about/index.html)
- [Methods](https://microbiomerepo.com/about/methods.html)
- [Downloads and releases](https://microbiomerepo.com/downloads/index.html)
- [Samples](https://microbiomerepo.com/samples/index.html)
- [For LLMs & API](https://microbiomerepo.com/llms/index.html)
- [Current data-package documentation](https://microbiomerepo.com/docs/README.html)
