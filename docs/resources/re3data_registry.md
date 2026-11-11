# re3data

**类型：** 研究数据仓库注册库；二级发现入口　**层级：** Extended　**核查：** 2026-11-11

## 它是什么

re3data 描述全球研究数据仓库。每条记录主要说明仓库的学科、内容类型、认证、持久标识符、元数据标准、数据访问/上传模式及 API 等，不是其中每个 dataset、project、BioSample 或 Run 的目录。

## 适合怎么用

- 用 `microbiome`、`metagenome`、`genomics`、`environment` 等主题或学科词搜索候选仓库；
- 用官方 facets 筛选开放/受限访问、持久标识符、认证、元数据标准等属性；
- 通过仓库 ID 查看详细记录，随后进入仓库自己的搜索界面查项目、论文、accession 和数据文件。

## 程序化访问与限制

当前文档为 API v4.0，提供 repository index 与单仓库 detail；官网另外提供在线仓库每日 XML 导出。re3data 仓库 metadata 标为 CC0，但这不影响各源仓库对实际数据设定的使用条件。对“找到仓库”与“找到可用的微生物组研究数据”必须分别留证。

## 官方来源

- [re3data About](https://www.re3data.org/about)
- [API 文档](https://www.re3data.org/api/doc)
- [每日 XML 导出与数据许可](https://www.re3data.org/data)
- [FAQ](https://www.re3data.org/faq)
