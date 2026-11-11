# ResMicroDb

**类型：** 人体呼吸道微生物组 curated database + analysis platform　**目录层级：** Core　**状态：** `active_verified`（核查：2026-11-10）

## 可提供什么

官方帮助文档报告收录 106,464 个 sample/run 记录、514 个项目和 489 篇出版物，覆盖 10 个呼吸道采样位点、146 个表型，并人工整理 32 个 metadata factors。字段包括 sample site/type、phenotype、sequencing type，以及年龄、性别、BMI、国家/位置、抗生素使用和采样时间点等。

用户可以按 metadata 过滤 Samples/Projects，查看项目中的样本/run、论文和测序信息，并下载 metadata 与 abundance tables。数据库还提供样本菌群组成、sample similarity search 和 cross-study analysis；论文汇总了 11,908 条微生物–疾病关联。

## 何时使用与限制

这是目前目录中与人体样本 metadata 查询直接相关、且聚焦呼吸道位点的资源，可用于按鼻腔、鼻咽、痰液、BALF、肺组织等位点和表型发现研究。它是有特定部位和纳入规则的 curated collection，不等于所有呼吸道研究或所有 SRA 项目的镜像。页面把条目称为 sample/run，因此复用计数时必须保留它的原始统计单位；个体特征能否对应到特定 BioSample 仍要检查每项研究的 ID crosswalk。

当前官网帮助文档与项目筛选页面提供了可审计的字段和流程说明；本轮没有实际提交单个 accession 并验证返回记录，故状态暂为 `active_verified`。

## 官方来源

- [ResMicroDb 官网](https://resmicrodb.cncb.ac.cn/)
- [官方帮助：功能、字段与下载](https://resmicrodb.cncb.ac.cn/help)
- [项目筛选页面](https://resmicrodb.cncb.ac.cn/project)
- [原始论文，NAR 2026](https://doi.org/10.1093/nar/gkaf1194)
