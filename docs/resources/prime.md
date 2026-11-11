# PRIME

**类型：** 人类 16S 数据库与 phenotype reference　**目录层级：** Core　**状态：** active_verified

## 它是什么

PRIME 面向可标准化处理的人类相关 16S rRNA amplicon 研究。2026 NAR 论文报告其包含 53,449 个样本，来自 111 项公开研究，覆盖 93 个身体位点和 101 类 phenotype。数据来自 NCBI，经过人工检查和标准化；每个样本可关联 metadata 和 SILVA 138.2/Greengenes2 2024.09 的分类丰度结果。

## 可提供什么

- 人工整理的 study/sample-level metadata：疾病、人口学、body site、BMI、生活方式、地理、测序参数和研究设计等；字段覆盖因样本而异；
- 多 taxonomy level 的 observed counts 和 relative abundance；
- Web browse、filter、metadata 下载、phenotype/身体位点/地理浏览；REST API v1 和 primeDB R client；
- 以 Project accession 或 Run ID 上传清单并生成自定义 abundance 表。

## 何时使用

用作人类 16S 数据集发现、样本 phenotype 参考和 accession/Run 交叉核验。对需要从疾病、人群、身体位点或饮食相关字段筛选 16S 队列的用户，PRIME 是优先入口之一；若将结果回并到 BioSample 主表，仍要保留 Run↔BioSample 关系和来源证据。

## 限制

仅覆盖入选研究和 16S 范围；53,449 是样本记录数，不等于受试者数。论文称 API 当前无需认证且无速率限制；使用时仍应遵守服务方当前文档。开放学术使用的许可声明需和特定数据文件的再分发条件分开核对。

## 来源

- [PRIME 2026 NAR paper](https://doi.org/10.1093/nar/gkaf1057)
- [PRIME website](https://primedb.sjtu.edu.cn/)
- [PRIME Help: filtering and downloads](https://primedb.sjtu.edu.cn/help)
- [PRIME Download Center](https://primedb.sjtu.edu.cn/download)
- [primeDB R client](https://github.com/reckonzzz/primeDB)
- [PRIME API v1](https://primedb.sjtu.edu.cn/api/v1)
- [Zenodo release](https://doi.org/10.5281/zenodo.15711237)
