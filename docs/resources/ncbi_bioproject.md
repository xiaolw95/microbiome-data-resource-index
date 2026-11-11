# NCBI BioProject

**类型：** 项目/研究归档　**目录层级：** Core　**已核查：** 2026-11-10

## 它是什么

BioProject 用于描述公共生物学数据项目，通常提供项目标题、摘要、研究组织信息及与样本、SRA 等记录的关联。它是追踪一项研究所提交数据的入口，不是逐个受试者/样本的完整 metadata 表。

## 可提供什么

- 项目 accession、标题和项目描述；
- 与 SRA、BioSample 等归档对象的链接；
- 项目级研究背景和可用于发现论文的关键词。

## 何时使用

输入 PRJNA 或从 Run/BioSample 解析到 BioProject 后，用它定位研究范围及关联样本，再结合论文和补充文件核对原始数据论文和样本 crosswalk。

## 限制

BioProject 的简介通常是项目级描述。不能把队列的共同背景直接复制成每个样本的个体信息；还要区分原始数据论文和后续复用该项目的论文。

## 官方来源

- [NCBI BioProject](https://www.ncbi.nlm.nih.gov/bioproject/)
- [BioProject FAQ](https://www.ncbi.nlm.nih.gov/bioproject/docs/faq/)
- [BioProject and BioSample Submission](https://submit.ncbi.nlm.nih.gov/about/bioproject-biosample/)
