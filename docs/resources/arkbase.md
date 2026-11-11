# ARKbase

**资源类型：** microbial knowledgebase　**优先级：** extended　**相关性：** indirect　**状态：** `active_verified`　**核查：** 2026-11-10

## 能提供什么

ARKbase 是针对优先病原细菌的 antimicrobial resistance knowledgebase。官网分 Reference Genome、Curated Genome AST 与多个 insight modules；可查病原体参考基因组、经整理的抗菌药敏实验结果、AMR/virulence/COG 注释、operons、结构与宿主-病原互作，并提供 sequence/advanced search 和 genome browser。

## 适合什么任务

- 从已知 pathogen genome 或物种出发查看 AST 与 AMR 相关基因组上下文。
- 对公共病原基因组做比较分析或追查特定抗性、毒力和宿主互作机制。
- 为 infection/AMR 项目提供 isolate-level pathogen phenotype 与 genotype 参考。

## 边界与注意事项

- ARKbase 里的 AST phenotype 是细菌分离株的药敏表型，不是人体受试者的健康状态。
- 它聚焦特定 priority pathogen，不是综合 microbiome sample metadata 数据库。
- 论文说明不同数据库/分析工具并用；核对具体数据的来源、标准版本和 accession，再解释表型。

## 入口与来源

- [ARKbase portal](https://datascience.imtech.res.in/anshu/arkbase/) · [FAQ](https://datascience.imtech.res.in/anshu/arkbase/faq.php)
- [原始论文](https://doi.org/10.1093/nar/gkaf1307)

相关目录行：[`resources.csv`](../../catalog/resources.csv) 中 `arkbase`。
