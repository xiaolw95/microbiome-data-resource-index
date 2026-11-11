# dbCAN-HGM

**资源类型：** microbial knowledgebase　**优先级：** extended　**相关性：** indirect　**状态：** `active_verified`　**核查：** 2026-11-10

## 能提供什么

dbCAN-HGM 汇总人类肠道微生物中的 carbohydrate-active enzyme (CAZyme) gene clusters。官网报告 6,031 个 species-level representative MAG、121,883 个 CAZyme gene clusters，并可按 taxonomy、continent、glycan substrate 等浏览和下载；页面也展示来自不同饮食类型和 UC/Crohn’s disease 组的 metagenomic read mapping。

## 适合什么任务

- 比较肠道微生物潜在糖类利用功能与基因簇。
- 按基因簇、底物、分类或地理范围探索可复用的功能参考。
- 初步了解资源中的 diet/disease 分组 read-mapping 证据。

## 边界与注意事项

- 这不是受试者饮食、诊断或生活方式字段的样本登记表。饮食/疾病信息用于数据映射/比较；不能仅据此给任一 BioSample 指定临床表型。
- 预测的底物归属需要实验验证，数据库页面有明确提示。
- 该库补充功能性与群落背景知识，不能替代论文 supplement 或 participant-to-sample crosswalk。

## 入口与来源

- [dbCAN-HGM 官网](https://pro.unl.edu/dbCAN_HGM/) · [原始论文](https://doi.org/10.1093/nar/gkaf1185)
- [论文代码与数据说明](https://github.com/azureycy/dbCAN-HGM)

相关目录行：[`resources.csv`](../../catalog/resources.csv) 中 `dbcan_hgm`。
