# NIAID Data Ecosystem Discovery Portal

**资源类型：** 跨仓库数据/工具 metadata 发现门户　**当前状态：** `active_verified`　**核查日期：** 2026-11-10

## 能提供什么

该门户由 NIAID Data Ecosystem 维护，跨多个感染性和免疫介导疾病相关仓库索引 dataset、resource catalog、sample 和 computational tool 的 metadata。其收录源包括 MicrobiomeDB 等专题仓库及 generalist repositories，因此可以作为疾病相关微生物组数据的额外“从问题找数据”入口。

门户允许关键词和 advanced search，按 disease、organism、data type、source 等 metadata fields 搜索；结果 metadata 可导出为 CSV/JSON，也能通过公开 API 查询。数据本体仍托管在原始仓库，门户负责统一描述和链接。

## 使用路径

1. 从 [NIAID Portal](https://data.niaid.nih.gov/) 输入 disease、organism、microbiome 等关键词，或在 Advanced Search 中指定 metadata field。
2. 使用 filters 缩小结果，检查资源类型、source repository、measurement technique、disease/organism 和 access 信息。
3. 导出筛选后 CSV/JSON，或通过 [metadata API](https://data.niaid.nih.gov/knowledge-center/accessing-the-metadata-api) 做程序化检索。
4. 点击原始来源的 Access Data 链接，按该仓库自己的访问和申请政策获取 dataset。

## 适合的任务

- 从疾病（如 IBD、感染性疾病）或宿主/病原体出发，发现多个仓库中的候选数据集和资源目录。
- 补充查找 MicrobiomeDB 以及其他 NIAID/一般性仓库的记录。
- 批量下载跨源 catalog metadata，用于趋势盘点或项目候选筛查。

## 边界

- 门户只索引并链接来源 metadata，不托管数据文件，也不代替原始仓库的权限流程。
- 数据源清单有限且持续变化；并非所有微生物组数据库或相关数据都会被收录。
- 来源 metadata 可能不完整，generalist repositories 还可能带来与疾病或 microbiome 无关的搜索命中。
- 门户层面的结果不证明宿主变量能映射到某个 BioSample；需沿原始论文、样本表和 accession crosswalk 追溯证据。

## 来源

- [NIAID Data Ecosystem Portal](https://data.niaid.nih.gov/)
- [Metadata API guide](https://data.niaid.nih.gov/knowledge-center/accessing-the-metadata-api)
- [FAQ: scope, source data and missing fields](https://data.niaid.nih.gov/knowledge-center/frequently-asked-questions)
- [2026 mSystems resource report](https://doi.org/10.1128/msystems.01270-25)
