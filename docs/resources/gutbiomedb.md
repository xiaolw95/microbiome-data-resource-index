# GutBiomeDB

**类型：** 人类肠道 16S 整理数据库与分析平台　**目录层级：** Core　**状态：** `active_verified`（2026-11-10 核查）

## 它是什么

GutBiomeDB 于 2026 年 11 月发布，整合了 168,464 个来自 482 个 BioProjects 的人类肠道 16S 样本。论文称其复用既有统一分类丰度 profiles，并在此基础上整理疾病表型、年龄/生命阶段、性别和地理来源；所报告的 46 个公开 REST endpoints 用于查询和分析。

## 可提供什么

- 样本、项目、疾病、分类组成和代谢功能的浏览与过滤；
- 人工整理的疾病、年龄组/生命阶段、性别和地理 metadata；
- taxonomy profiles 与 metadata 的 [Zenodo 下载](https://zenodo.org/records/22952317)；
- 差异分析、跨研究 meta-analysis、共现网络、生命周期图谱和基于输入 genus profile 的相似性/健康指数分析；
- 公开 API 与 [平台源代码](https://github.com/zhai199887/GutBiomeDB)。

## 何时使用

对人类肠道 16S 队列，可检查样本或 BioProject 是否已进入整理集合，比较疾病/人群分布，并用 Zenodo metadata/profile 做复用或交叉核验。需要宿主变量的原始定义或样本到 subject/visit 的映射时，仍回到对应原始研究和补充材料。

## 限制

该资源是预先整理的人类肠道 16S compendium，不是通用 accession-to-paper 检索器，也不覆盖所有身体位点或 shotgun 数据。论文所述的 API 数量不等于本项目已审计每个 endpoint；API base URL/schema 尚未单独记录。论文描述的主要宿主变量不包括饮食或完整临床问卷，不能据此假定字段存在。官网是 JavaScript 应用；本轮确认首页可解析到应用入口，未逐项操作页面功能。

## 来源

- [GutBiomeDB 官网](https://gutbiomedb.online/)
- [2026 NAR 论文与方法](https://doi.org/10.1093/nar/gkag1125)
- [Zenodo profiles 与 metadata](https://zenodo.org/records/22952317)
- [平台源代码](https://github.com/zhai199887/GutBiomeDB)
