# mBodyMap

**类型：** 人体多身体位点、疾病与菌群 profiles 整理数据库　**目录层级：** Extended　**状态：** `active_verified`（核心浏览/下载能力由 2022 NAR 论文确认；当前数据版本未复核）

## 它是什么

mBodyMap 汇总公共人体微生物组项目，将测序样本/Run 按身体位点和健康/疾病状态组织，提供微生物分类与丰度结果，并从论文、补充材料和归档记录人工整理宿主及采样 metadata。它覆盖多身体位点，可用于从研究问题进入具体项目和样本记录。

## 可提供什么

- 按身体位点、健康/疾病状态浏览研究和样本/Run，并查看 taxon abundance/prevalence；
- 人工整理的 host metadata，包括年龄、性别、国家、BMI 和疾病状态（字段完整性因研究而异）；
- Data 页面提供论文所述的 project 与 sample/run metadata 下载，并链接 NCBI BioProject、SRA 等原始归档；
- 论文报告的 2022 年数据库快照为 63,148 runs（14,401 metagenomic、48,747 amplicon），跨 136 projects、22 个身体位点和 56 种疾病；其中 61,913 runs 通过论文定义的质控并有有效 profile。以上是论文发表时统计，不代表当前 release 数量。

## 如何使用

1. 从 [mBodyMap 首页](https://mbodymap.microbiome.cloud/)按身体位点或疾病浏览；
2. 在论文描述的 Data 页面下载整理后的项目、样本/Run metadata；
3. 沿记录中的 BioProject、SRA/ENA 和 publication 链接回查原始数据及补充表；
4. 如需将宿主信息用于单个 BioSample，应确认表中的 Run/Sample ID 与归档 ID 的明确 join，不以研究级纳排条件替代样本级映射。

## 限制

- 资源只覆盖其纳入的人体研究，且数据单位混有 sample 和 run；进行计数或合并前需按 biological sample 去重。
- 年龄、性别、国家、BMI、body site 与 disease 等字段来源和完整率不同；引用队列统计时不能默认每个样本都具备这些信息。
- 网页入口可访问，但本轮未下载数据包或逐 ID 测试；论文报告的是 2022 年快照，需在实际使用前确认当前数据版本、文件格式和 ID crosswalk。
- mBodyMap 是专题整理资源，不是所有公共 accession 的通用解析器。

## 来源

- [mBodyMap 官网](https://mbodymap.microbiome.cloud/)
- [2022 NAR 原始论文](https://academic.oup.com/nar/article/50/D1/D808/6413603) · [PMC 全文](https://pmc.ncbi.nlm.nih.gov/articles/PMC8728210/)
