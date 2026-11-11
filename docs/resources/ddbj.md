# DDBJ Sequence Read Archive (DRA)

**类型：** 公共序列归档　**目录层级：** Core　**已核查：** 2026-11-10

## 它是什么

DDBJ Sequence Read Archive (DRA) 是 INSDC 的序列 reads 归档服务之一。DDBJ 页面提供 DRA accession 查询和公开数据下载，支持 HTTPS/FTP/Aspera 等入口；DDBJ Search 用于定位 DRA accession 的文件路径。

## 可提供什么

- DRA project/sample/experiment/run records 和 accession；
- 记录关联的公共 SRA/FASTQ 文件路径；
- DDBJ flat-file 数据库的 getentry WebAPI（但官方说明 DRA retrieval 要使用 DDBJ Search，getentry 本身不取 DRA 数据）。

## 何时使用

作为 INSDC 多区域 archive 入口；输入 DRA 项目或 Run ID 后查询关联记录和文件。与 NCBI/ENA 重复交叉记录时，保留原始 accession namespace，不把不同前缀折叠成一个未标注的 ID。

## 限制

DDBJ Search、getentry 和 DRA 下载是不同服务；不要将 getentry API 描述成 DRA 的完整查询接口。宿主/采样信息仍取决于提交属性，公开 reads 的下载路径不等于完整 phenotype metadata。

## 官方来源

- [DDBJ DRA public data access](https://www.ddbj.nig.ac.jp/faq/ja/how-to-download-data.html)
- [DDBJ getentry WebAPI and DRA limitation](https://www.ddbj.nig.ac.jp/services/getentry-e.html)
- [DDBJ DRA](https://www.ddbj.nig.ac.jp/dra/index-e.html)
