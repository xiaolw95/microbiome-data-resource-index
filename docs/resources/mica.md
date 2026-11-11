# Mica (INTIMIC metadata portal)

**类型：** 营养流行病学/肠道菌群研究 metadata 与 harmonization portal　**目录层级：** Core（主题发现）　**状态：** `active_verified`　**已核查：** 2026-11-10

## 它是什么

Mica 是 INTIMIC 项目参与研究的 metadata portal，面向营养流行病学和肠道微生物组的人体观察性研究。它将 individual studies、collected datasets、变量、harmonization initiatives 和 harmonization protocols 放在同一检索入口中，帮助用户判断不同研究是否测量了感兴趣的变量、是否可比较或参与联合分析。

## 可提供什么

- 研究/队列描述、入组人群、项目和公开 metadata 的发现线索；
- 饮食、营养、肥胖/健康结局及肠道菌群研究的 harmonization initiatives 和变量信息；
- 针对不同研究的 harmonization protocols；
- 通过 DataSHIELD/Opal 思路进行不集中转移个体数据的联邦分析路径。具体数据是否能访问、可分析到什么粒度，由数据所有者和对应审批条件决定。

## 适用场景

从研究问题出发寻找包含 diet/nutrition 暴露及肠道菌群的数据集、比较队列变量是否对齐，或发现可申请参与的 federated analysis 网络。对你提出的“饮食、生活方式与菌群”检索需求，Mica 可作为专题发现入口，与直接搜索测序 accession 的资源互补。

## 限制

- Mica 是参与项目网络的 metadata inventory，不是全领域公共测序 accession 索引，也不是开放的个体级 phenotype 下载库。
- Mica 的部分 harmonization initiative 会与 NFDI4Health 协作/互链；NFDI4Health 是范围更广的德国 health-study portal，而非另一个 Mica microbiome database。
- 公开可见的 study metadata、变量列表或 harmonization protocol，不代表样本层数据已公开；部分数据保留在研究方 Opal server，通过授权/合作申请后才能联邦分析。
- 官网未在本次核查中提供一个可确认的通用 API 或所有队列统一的 BioSample/Run crosswalk；用来发现研究后，仍需沿具体研究页追溯到论文、测序 archive 和 ID 映射。
- 本项目仅索引官网与文档，不复制受限数据或将研究级信息下推到样本级。

## 官方来源

- [Mica metadata portal](https://mica.mdc-berlin.de/)
- [Individual studies](https://mica.mdc-berlin.de/individual-studies)
- [Collected datasets](https://mica.mdc-berlin.de/collected-datasets)
- [Harmonization protocols](https://mica.mdc-berlin.de/harmonized-datasets)
- [INTIMIC Knowledge Platform paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC9100002/)
