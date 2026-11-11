# NCBI BioSample

**类型：** 生物样本归档　**目录层级：** Core　**已核查：** 2026-11-10

## 它是什么

BioSample 保存产生归档数据的物理生物材料描述，并与相关序列归档记录及 BioProject 互链。BioSample 的样本描述通常是结构化属性名—值对；部分属性使用 harmonized name 和 package，提交者也可添加自定义属性。

## 可提供什么

若提交者提供，属性可能包含 `host`、`host_subject_id`、`host_tissue_sampled`/body site、`collection_date`、地理位置、`sex`、`age`、`health_state` 或 `diet` 等。BioSample 有属性同义名和 package 文档，适合用来构建属性名称归一化映射。

## 何时使用

输入 SAMN/SRS 或从 SRA/ENA 解析到 BioSample 后，读取属性并保留原始键和值；规范化字段必须另外保存，不能覆盖原字段。可用 BioSample → BioProject 和 SRA/ENA 链接寻找研究及测序记录。

## 限制

属性名和填写完整度随提交者、样本类型和提交年代不同。识别某属性“可接受”不代表每个记录都填写了该属性；空字段也不能推出阴性、健康或未暴露。

## 官方来源

- [BioSample Documentation](https://www.ncbi.nlm.nih.gov/biosample/docs/)
- [BioSample Attributes](https://www.ncbi.nlm.nih.gov/biosample/docs/attributes/)
- [BioSample Packages](https://www.ncbi.nlm.nih.gov/biosample/docs/packages/)
