# European Nucleotide Archive (ENA)

**类型：** 公共序列归档　**目录层级：** Core　**已核查：** 2026-11-10

## 它是什么

ENA 是 INSDC 成员之一，保存并开放序列记录及其相关样本、研究和实验对象。它提供 Portal API、Browser API 和 file reports，可按 accession 搜索、取回关联记录和定位公开文件。

## 可提供什么

- Study/Project、Sample、Experiment、Run 等记录及其关联；
- 提交的样本/测序 metadata；
- FASTQ 等关联文件的公开下载位置（具体文件依记录而定）；
- 可通过 Browser API 获取与指定 Sample/Study 关联的其他记录。

## 何时使用

适合作为 SRA/INSDC 记录的补充查询入口，特别是批量展开 Run 清单、获取文件报告和检查跨库记录。`enaBrowserTools` 是配套命令行取数工具，另列在工具目录。

## 限制

归档里的宿主字段仍是提交 metadata；ENA 的 API 能力和字段不应被误解为自动抽取论文补充表。不同 INSDC accession 可能互为外部链接或别名，需保存 ID 类型和来源。

## 官方来源

- [ENA Programmatic Access](https://ena-docs.readthedocs.io/en/latest/retrieval/programmatic-access.html)
- [ENA Browser API](https://ena-docs.readthedocs.io/en/latest/retrieval/programmatic-access/browser-api.html)
- [ENA Browser](https://www.ebi.ac.uk/ena/browser/home)
