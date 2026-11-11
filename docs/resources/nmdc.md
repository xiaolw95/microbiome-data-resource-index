# National Microbiome Data Collaborative (NMDC)

**类型：** 环境微生物组数据门户、提交平台与 API　**优先级：** Core　**状态：** `active_verified`（首轮核对：2026-11-10）

## 用途

NMDC 为环境微生物组数据提供标准化的研究/生物样本 metadata、多组学数据发现、统一处理结果和程序化查询。它由 Submission Portal、Data Portal、统一 schema 与 REST API 组成；既是数据资源，也提供提交和检索基础设施。

## 覆盖与对象

- 官方文档覆盖 metagenome、metatranscriptome、metaproteome、metabolome、lipidome 等环境多组学数据。
- API 可以查询 study、biosample、data object、planned process 和 workflow records，并通过 NMDC persistent IDs 连接对象。
- 样本描述以 MIxS、GOLD ecosystem classification、EnvO 等标准为基础；数据由贡献者提交，经 metadata 审核和 NMDC workflow 处理后进入门户。
- **范围限制：** NMDC FAQ 明确说明当前不支持 human microbiome data，因此不能作为人体年龄、饮食或疾病 metadata 的补充来源。

## 如何使用

1. 在 [NMDC Data Portal](https://data.microbiomedata.org/) 按研究、样本、环境和组学类型筛选。
2. 已知 NMDC ID 时，可通过 [Runtime API](https://api.microbiomedata.org/) 查询 `/studies`、`/biosamples`、`/data_objects` 等端点；过滤语法与字段定义见 [API GUI 使用指南](https://docs.microbiomedata.org/howto_guides/api_gui/)。
3. 单个 study/sample 页面可下载 metadata，主搜索页支持批量 metadata 下载。完整数据文件下载需要 ORCID 登录；具体文件还要看各记录和 workflow 的可用状态。
4. 把 NMDC ID 与外部 BioSample/Project/Run accession 分列保存；仅在记录本身提供互链时建立 crosswalk。

## 访问与复用

官方 Data Use Policy 说明 NMDC 数据采用 Creative Commons Attribution 4.0 International (CC BY 4.0)，并要求正确引用数据集及贡献者。Data Portal 文件下载使用 ORCID 登录；API 中部分端点也可能需要认证。NMDC 是整理后的贡献型数据集合，不是所有公开 microbiome accession 的镜像。

## 来源

- [NMDC 官方主页](https://microbiomedata.org/)
- [Data Portal 使用指南](https://docs.microbiomedata.org/howto_guides/portal_guide/)
- [Runtime API](https://api.microbiomedata.org/)
- [API GUI 使用指南](https://docs.microbiomedata.org/howto_guides/api_gui/)
- [NMDC Data Use Policy](https://microbiomedata.org/nmdc-data-use-policy/)
- [NMDC 2022 NAR 论文](https://doi.org/10.1093/nar/gkab990)
