# Genome Sequence Archive (GSA, CNCB-NGDC)

**类型：** 公共组学原始测序数据归档　**目录层级：** Core　**状态：** active_verified

## 它是什么

CNCB-NGDC 维护的原始 reads 归档，按 Project、Sample、Experiment、Run 组织记录。它既收录 GSA 自有项目，也提供 INSDC 数据的元数据整合与统一检索；因此一个生物样本或 Run 可能在不同归档入口出现多条互链记录。

## 可提供什么

- 项目、样本、实验和测序反应之间的归档关系；
- 项目描述、提交者、样本属性、文库和测序字段，以及公开数据下载入口；
- 对 GSA 自有提交，常见 ID 包括 CRA、PRJCA、SAMC、CRX、CRR；INSDC 整合记录仍可能使用各归档原有 accession。

## 何时使用

当研究使用 GSA/NGDC accession，或希望对 NCBI/ENA/DDBJ 已收录的公开测序项目进行跨库搜索时，可用 GSA 浏览入口核对项目、样本和 Run 关系，并查看数据下载路线。

## 限制

- GSA 的对象和 Run 数不能直接解释成独立受试者或 biological sample 数；
- GSA 对 INSDC 的元数据整合会产生与原始归档相同的项目/样本记录，合并时需保留 provider 和原始 accession 并按关系去重；
- 归档字段取决于提交内容；GSA 不会自动恢复论文补充表中的饮食、生活方式或临床样本映射；
- 本轮确认了官方浏览/下载与记录模型，但没有验证通用的 GSA REST API 或逐 accession crosswalk。

## 官方来源

- [GSA 官方入口](https://ngdc.cncb.ac.cn/gsa/)
- [GSA 浏览页](https://ngdc.cncb.ac.cn/gsa/browse/)
- [CNCB-NGDC 资源论文（NAR 2026）](https://doi.org/10.1093/nar/gkaf1172)
- [官方 GSA 使用介绍](https://ngdc.cncb.ac.cn/education/tutorials/gsa/)
- [re3data 记录](https://www.re3data.org/repository/r3d100012342)
