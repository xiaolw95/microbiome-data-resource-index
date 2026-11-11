# Celeri Microbiome Studies Explorer

**类型：** ENA 派生的微生物组研究/样本 metadata 搜索平台　**目录层级：** Core（人体肠道范围）　**状态：** `active_partial`　**已核查：** 2026-11-11

## 它是什么

Celeri 的 Microbiome Studies Explorer 是一个面向人体肠道 raw-read 研究的 metadata 搜索页面。平台说明数据来自 ENA XML 中由提交者填写的研究、样本、实验信息；Celeri 使用 AI 对非结构化、异质字段进行抽取和标准化，并将 Study、Sample、Experiment 和 Run 组织成关联层级。它不托管测序文件。

## 可提供什么

- Study 层：研究标题/项目 accession、host 状态与年龄分类、疾病、干预、纵向设计/时间点、样本来源国家、采集年月、关联文章、MGnify study 和临床试验编号等；
- Sample 层：样本 accession、来源国家/日期、host ID、疾病/干预/反应、host 年龄/性别/体重或 BMI、临床信息、实验数和 Run 数等；
- Experiment 层：文库 layout 与 selection 等技术信息。

字段由其 AI 从 ENA 提交者提供的 XML 描述和 attributes 中归纳/映射；字段存在并不表示已从论文补充文件中恢复或经过人工逐样本验证。AI 推断值应回到原 ENA 记录和文章核实。

## 适用场景

适合从人体肠道 shotgun 研究主题筛选 ENA 候选项目，再按 Study、Sample、Experiment、Run accession 回到 ENA、MGnify 和论文继续核实。它可作为发现入口和研究者自建 ID-to-metadata 工具的设计参考，不是所有微生物组领域的通用检索器。

## 限制与使用条款

- 范围仅为其声明的人体肠道微生物组研究；不是跨身体位点、生态系统和 assay 的全领域目录。
- 其元数据起点是 ENA XML；没有证据表明平台系统检索论文全文或 supplement 来补回 ENA 未提交的信息。
- 站点说明称通常每周同步；2026-11-11 页面显示 “No update available” 且表格仍在加载。此前可见最近同步时间为 2026-05-28，因此当前更新情况记为 `active_partial`。
- 页面未提供已核实的公开 API 文档。条款页标注 CC BY-SA 4.0，同时附加禁止镜像/系统性抓取等限制；本目录只提供官方链接，不复制平台数据或自动批量抓取。使用、再发布和构建衍生资源前应阅读[当前条款](https://www.celerilab.com/data/license)。

## 官方来源

- [Explorer](https://www.celerilab.com/data)
- [数据处理与字段说明](https://www.celerilab.com/learn-more)
- [License & Terms of Use](https://www.celerilab.com/data/license)
