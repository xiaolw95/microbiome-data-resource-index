# gutMSNP

**类型：** 人类肠道菌群 SNP/表型关联知识库　**目录层级：** Extended　**状态：** `active_verified`（核查：2026-11-10）

## 它是什么

gutMSNP 汇总人类肠道 metagenome 的微生物单核苷酸变异及其表型分层模式，并提供微生物参考基因组和 SNP 查询/分析界面。2026 年论文报告 4,386 个样本、21 个宿主表型、164,015,783 个 SNP、8,146 个代表性参考基因组，以及 364 个 species-level 和 8,251 个 gene-level 记录。

## 可提供什么

- 按表型浏览 SNP 分布、相关物种和基因；
- 按 project accession、PMID、sample source、Disease Ontology term、sequencing platform 和样本计数查看研究级背景；
- 下载参考基因组，或上传微生物基因组进行 SNP 检测与注释。

## 与宿主 metadata 的边界

它把已纳入研究按宿主表型分层，并提供项目/论文和样本来源信息，适合发现“某类疾病涉及哪些微生物基因变异”的研究线索。论文表中的样本计数和 phenotype 仍是研究/组别层级；不能据此给每个 BioSample 自动赋予诊断、年龄、性别或其他个体属性。项目 accession 与样本 accession 的具体 crosswalk 需回到来源研究核对。

## 官方来源

- [gutMSNP 官网](https://bio-computing.hrbmu.edu.cn/gutMSNP/)
- [原始论文，NAR 2026](https://doi.org/10.1093/nar/gkaf1205)
