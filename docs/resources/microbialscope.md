# MicrobialScope

**资源类型：** microbial knowledgebase　**优先级：** extended　**相关性：** indirect　**状态：** `active_verified`　**核查：** 2026-11-10

## 能提供什么

MicrobialScope 是跨细菌、古菌、真菌和病毒的基因组与功能注释资源。可以用 genome accession 搜索记录，并浏览基因组、蛋白、tRNA/tmRNA、CRISPR-Cas、次级代谢基因簇、信号肽、毒力因子、抗生素抗性基因和跨膜蛋白。官网还提供 metadata/FASTA 等定制下载 API，并有序列分析与比较分析模块。

## 适合什么任务

- 从 genome accession 出发补充微生物本体的注释、ARG、毒力和代谢功能。
- 从候选病原体或微生物 genome list 开始做参考查询、比对和比较分析。
- 下载序列、metadata 或功能注释，作为样本分析结果的参考背景。

## 边界与注意事项

- 输入主要是微生物 genome ID；不能把它当作 BioSample/Run accession 到受试者 metadata 的解析器。
- 它所含 ARG/virulence 等是微生物基因组层注释，不等于宿主感染诊断或临床结局。
- 官网披露的数据库数值随版本更新；大规模使用前应记录下载日期和数据版本。

## 入口与来源

- [MicrobialScope 官网](https://microbial.deepomics.org/) · [原始论文](https://doi.org/10.1093/nar/gkaf1234)

相关目录行：[`resources.csv`](../../catalog/resources.csv) 中 `microbialscope`。
