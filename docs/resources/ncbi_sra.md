# NCBI Sequence Read Archive (SRA)

**类型：** 公共序列归档　**目录层级：** Core　**已核查：** 2026-11-10

## 它是什么

NCBI SRA 是高通量测序 reads 的归档。其逻辑对象包括 Study（与 BioProject 对应）、Sample（与 BioSample 对应）、Experiment 和 Run。Experiment 主要描述文库/测序实验设置；Run 关联实际序列文件。一个 BioSample 可能被不同 Study 共享，也可能关联多个 Experiment/Run，因此不能把 Run 数当作生物学样本数。

## 可提供什么

- Study/Project、Sample、Experiment、Run 的 accession 及关联；
- Experiment 层的文库、策略、layout、仪器等技术信息；
- Run 的序列文件和测序统计信息；
- BioSample 与 BioProject 的链接。

宿主、年龄、性别、采样部位等内容主要看相关 BioSample 属性；不能假设 Run 页会给出完整宿主表型。

## 何时使用

输入 SRR 时先用 SRA 关系/Run Selector 展开 Experiment、BioSample 和 BioProject；输入 Study/Project 时下载关联 Run 清单，再按 BioSample 汇总。用 BioSample 作为样本主表，Run/Experiment 保存在关系表。

## 限制

SRA 的技术字段和 BioSample 的提交属性依赖提交者填写；同一研究的临床/生活方式信息可能只在论文或补充表中。SRA 不负责将论文中作者内部样本名自动映射到 BioSample。

## 官方来源

- [SRA Metadata and Submission Overview](https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/)
- [SRA](https://www.ncbi.nlm.nih.gov/sra/)
