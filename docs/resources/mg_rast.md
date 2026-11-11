# MG-RAST

**类型：** Metagenomics 数据/分析平台与 REST API　**目录层级：** Core　**状态：** active_verified

## 它是什么

MG-RAST 保存平台项目、样本、metagenome 作业及分析产物，使用自己的 ID 体系（常见形式包括 project `mgp`、sample `mgs` 和 metagenome `mgm`）。官方 REST API 支持按 MG-RAST ID、metadata、function 或 taxonomy 搜索，也提供 project、sample、metagenome 与 metadata 查询接口。

## 可提供什么

- MG-RAST 项目、样本、metagenome 记录；
- metadata JSON、项目/样本信息和相关数据产品；
- 平台处理后的分类与功能注释、profile 和可下载结果；
- 通过项目/样本模板提交的字段。提交模板将 project、sample 和 library/assay 信息分开，使用 MIxS 相关字段和受控词表。

## 何时使用

当项目或样本已经有 MG-RAST ID 时查询平台记录；若只有 SRA/ENA accession，可将其作为候选外部链接去查，但不能假定平台一定有对应项目。

本轮对官方公开样本 metagenome 请求 `https://api.mg-rast.org/1/metagenome/mgm4440026.3?verbosity=full` 做只读核验，返回 HTTP 200 和包含 sample link/metadata 的 JSON。通用公开搜索请求也返回 HTTP 200，但当前搜索条件得到 0 条，因此状态只表示已验证样本级 API 查询可用；搜索召回、过滤语法和对任意 SRA/ENA accession 的映射仍须进一步校准。

## 限制

MG-RAST 是平台自有记录和分析入口，不是任意 SRA ID 的通用宿主信息恢复器。官方 API 文档说明，公共数据可不带 key 查询，私有数据需要有效授权 key。API 和 metadata 模板文档可供设计流程时参考；具体平台 ID 与 INSDC accession 的交叉链接仍须逐条确认。

## 官方来源

- [MG-RAST API Documentation](https://help.mg-rast.org/api.html)
- [MG-RAST Search API Explorer](https://www.mg-rast.org/mgmain.html?mgpage=searchapi)
- [MG-RAST User Manual: metadata templates](https://help.mg-rast.org/user_manual.html)
- [MG-RAST](https://www.mg-rast.org/)
- [REST API 论文](https://doi.org/10.1371/journal.pcbi.1004008)
