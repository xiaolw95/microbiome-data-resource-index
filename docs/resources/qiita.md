# Qiita

**类型：** 多组学 study/sample metadata 和分析平台　**目录层级：** Core　**状态：** active_verified

## 它是什么

Qiita 用 Study 管理研究，明确区分 biological sample information 与 preparation/sequencing information，并组织 sequence data、分析流程和 artifacts。官方 2026.01 文档说明，sample information 文件描述样本生物学背景，preparation 文件描述实验/测序方案；两类信息通过 `sample_name` 连接。

## 可提供什么

- Study 标题、联系人、摘要和研究描述；
- 每个 study 的样本表，含作者/提交者提供的 host 或环境相关字段；
- 每种实验 preparation 的实验室处理与测序方案字段；
- public study 的样本信息下载、原始/处理后文件、BIOM/QIIME 等 artifact（取决于公开和访问条件）。

## 何时使用

在已有 Study/论文/ENA 项目候选时，搜索 Qiita 是否存在对应研究；比较 sample information 与 preparation 文件，查看 accession 或作者 sample name 是否能建立明确 crosswalk。

## 限制

并非所有公开 microbiome study 都在 Qiita。样本名可能是研究内部 ID；需结合 Run/ENA accession 验证。官方 REST 文档将通用 study/sample 查询 API 标为内部、计划对普通用户开放；当前导航可依赖公开页面和文档化的下载，不默认依赖内部接口。Study 的共享权限由数据所有者管理。

## 官方来源

- [Qiita Documentation](https://qiita.microbio.me/static/doc/html/index.html)
- [Sample 与 preparation 信息说明](https://qiita.ucsd.edu/emp/static/doc/html/gettingstartedguide/index.html)
- [Qiita FAQ: sample vs preparation information](https://qiita.microbio.me/static/doc/html/faq.html)
- [Qiita REST API docs and access note](https://qiita.microbio.me/static/doc/html/dev/rest.html)
- [Qiita 论文](https://doi.org/10.1038/s41592-018-0141-9)
