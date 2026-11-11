# Human Microbiome Bioactives Resource (HMBR)

**资源类型：** 人体肠道样本/文件发现与下载平台　**当前状态：** `active_verified`　**核查日期：** 2026-11-10

## 能提供什么

HMBR 面向人体肠道微生物组研究与 bioactive discovery。它的门户将研究、样本和文件关联起来，并允许按样本属性或文件属性筛选。官方文档给出的样本 facets 包括 study、assay preparation、race、smoking history、gender 和 age category；其他可搜索字段可通过 Add a Filter 浏览。文件结果包含访问类型、URL、数据类别、文件格式和大小。

HMBR 的 sample metadata manifest 还展示了更细的字段：sample ID、study、subject accession、source sample accession、PMID、gender、disease、race、BMI、age category、smoking history、alcohol、medication、body site、sample type、timepoint、family ID 等。字段并不保证每个研究/样本都有值；跨 study 的编码和 crosswalk 仍应逐项核实。

## 怎么检索和导出

1. 在 [HMBR Portal](https://portal.microbiome-bioactives.org/) 用 study、样本 facets 或高级查询筛选。
2. 按需从结果的 Files 选项卡加入 cart；可将多个查询的文件合并到购物车。
3. 下载 file manifest 和 sample metadata manifest。官方说明 manifest 会将 file ID、校验和、大小、URL 与关联 sample ID 对应起来；一份 sample metadata manifest 可进一步关联样本属性。
4. 用 [IGS Portal Client](../../catalog/tools.csv) 或其他支持的下载方式获取文件，并按每条记录显示的 access type 检查权限。

## 适合的任务

- 从 IBD/肠道研究中按年龄段、性别、吸烟史或研究队列找候选样本。
- 先筛文件类型/组学，再获取文件清单与关联样本表。
- 查看门户内已整理的疾病、药物、身体位点、时间点等表型信息。

## 边界

- HMBR 是聚焦的人体肠道研究门户，并非覆盖所有微生物组领域的通用 accession resolver。
- 门户出现 subject/sample 信息，并不自动证明 subject 与公共 BioSample、Experiment、Run 一一对应；需检查 sample accession、study、论文或 supplement 中的 ID crosswalk。
- 文件可能具有不同 access type。公开浏览、公开 metadata 与数据文件可下载性应分别记录。
- 不要把 cohort-level demographics 下推到样本；只有显式映射证据支持时才建立 subject/visit/sample 关联。

## 来源

- [HMBR Browse Portal 指南](https://microbiome-bioactives.org/browse-portal/index.html)
- [下载 manifests 指南](https://microbiome-bioactives.org/download-file-manifest/index.html)
- [IGS Portal Client 指南](https://microbiome-bioactives.org/download-portal-client/index.html)
- [2026 年 IBD metagenome 研究](https://doi.org/10.1053/j.gastro.2026.06.023)：报告 HMBR 中可获取样本级 metadata、taxonomic/functional profiles 和 raw sequencing links。
