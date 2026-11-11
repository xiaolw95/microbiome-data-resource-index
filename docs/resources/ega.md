# European Genome-phenome Archive (EGA)

**类型：** 人类组学与表型数据归档　**优先级：** Core supporting　**状态：** `active_verified`（首轮核对：2026-11-10）

## 为什么列入微生物组资源目录

EGA 不是微生物组专用数据库，但许多与人类微生物组关联的临床、问卷、遗传或样本关联信息受同意书和隐私政策限制，可能只在 EGA 或其他受控归档中提供。它可以补充公共 INSDC 记录里缺失的宿主 metadata，并提供研究、样本、实验、Run、文件和受控数据集之间的持久标识与关联。

## 可查询对象与 ID

EGA 的公开 metadata REST API 支持 Study (`EGAS`)、Dataset (`EGAD`)、Sample (`EGAN`)、Run (`EGAR`) 等对象查询，并可进行对象间 cross-query。公开 API 返回可公开的 metadata；授权数据的详细 metadata 和文件需要登录并获得相应 Data Access Committee (DAC) 批准。

## 检索步骤

1. 从文章、BioProject、SRA 或 ENA 中找到 EGA study/dataset accession，或在 [EGA Datasets](https://ega-archive.org/datasets/) 搜索研究名称。
2. 查看公开 Study/Dataset 页面、样本数和 DAC 信息；可用 [公开 metadata API](https://ega-archive.org/discovery/metadata/public-metadata-api/) 查询样本/Run 关联。
3. 若需要临床表型、问卷或受控 reads，按照页面要求向 DAC 提交访问申请。授权前只使用公开 metadata，不尝试访问受控对象。
4. 获批后通过 EGA 的 metadata 下载入口或受支持客户端获取授权范围内的文件。

## 示例：Lifelines NEXT

Lifelines NEXT 同时链接 NCBI SRA accession `PRJNA1468137` 与 EGA 的 `EGAS50000000133`、`EGAD50000001187`、`EGAD50000002469`、`EGAD50000002677`。论文说明 SRA 有公开的去人源、质控 shotgun reads；EGA 提供粪便/乳汁/阴道相关数据及带问卷和临床信息的 metadata，但这些数据须通过研究申请流程获取。这个案例说明“公共 reads 可下载”不等于“样本临床 metadata 也开放”。

## 限制

- EGA 收录的是广义人类研究数据，不保证某项 study 包含微生物组数据。
- 公共 API 返回的是公开字段；完整样本映射、临床字段和数据文件可能受控。
- EGA accession 与 BioSample、Run accession 是不同标识体系，需要用归档记录或论文的 crosswalk 明确连接。

## 来源

- [EGA 官方主页](https://ega-archive.org/)
- [EGA Public Metadata API 文档](https://ega-archive.org/discovery/metadata/public-metadata-api/)
- [EGA metadata 下载和授权说明](https://ega-archive.org/access/download/metadata/)
- [Lifelines NEXT EGA Study 页面](https://www.ega-archive.org/studies/EGAS50000000133)
- [Lifelines NEXT 论文数据可用性说明](https://pmc.ncbi.nlm.nih.gov/articles/PMC13626959/)
