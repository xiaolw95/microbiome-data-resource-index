# PMC BioC Supplementary Materials API

**类型：** 论文补充材料检索入口　**目录层级：** Core supporting　**已核查：** 2026-11-10

## 它是什么

NCBI 提供针对 PMC Open Access 子集中补充材料的 BioC 接口。可列出某文章的 supplementary material 文件，并对支持的文件提供 BioC XML/JSON 形式内容或原始附件入口。

## 可提供什么

- PMID/PMCID 对应的补充文件列表；
- 特定附件的机器可读文本/表格表示（视文件和转换能力而定）；
- 大文件附件的下载入口。

## 何时使用

在 Europe PMC 或项目关联中确定候选论文后，用 PMID/PMCID 获取 supplement 清单，再针对含样本映射、临床特征或采样信息的附件进行解析。保留原始文件名、表号、sheet/row 和原文定位。

## 限制

服务范围是 PMC Open Access 补充材料集合，不代表覆盖所有期刊附件。PDF 和复杂表格可能无法保留行列结构；解析后仍需核实样本 ID 与 accession 的对应证据。

## 官方来源

- [PMC BioC supplementary materials API](https://www.ncbi.nlm.nih.gov/research/bionlp/APIs/FAIR-SMART/)
- [PMC Developer APIs](https://pmc.ncbi.nlm.nih.gov/tools/developers/)
