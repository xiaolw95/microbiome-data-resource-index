# MetaSUB Reproducible Metadata

**资源类型：** 项目级整理 metadata 与样本 ID crosswalk　**当前状态：** `active_partial`　**核查日期：** 2026-11-10

## 能提供什么

[MetaSUB-metadata GitHub 仓库](https://github.com/MetaSUB/MetaSUB-metadata)汇集原始项目 metadata 表、清理脚本、样本名表和多个 identifier mapping 表。仓库中的 `map_collate` 包尝试沿多层 ID 间接关系把样本 metadata 与 FASTQ 名称连接；README 报告由它生成的表覆盖 1,301 个 samples/FASTQs，同时明确说明许多字段不完整。

映射表示例包括：MetaSUB 样本名 ↔ H.A. 实验室编号、barcode、plate position、提交表格编号、library/FASTQ 文件名等。仓库还保留清理前后的数据，例如 barcode 被表格软件转成数字、导致 leading zero 丢失，或字段错列后通过脚本清理的案例。

## 适合的任务

- 理解公共研究中为什么 accession、样本标签、plate/barcode、library 和 FASTQ 名称可能需要多跳 crosswalk。
- 研究如何从分散在不同工作表中的 mapping 关系重建样本表，并保留原始表格和转换步骤。
- 从城市/项目样本名发现 MetaSUB 相关样本和可用 metadata。

## 怎么使用

仓库提供 `metasub-generator best-effort > metadata.csv` 的生成入口和 `map_collate` 源码；也可直接检查仓库中的清理表和 crosswalk 文件。若需 raw sequencing files，沿样本名/项目 accession 回到对应 archive 或项目数据包，并单独核对其访问条件。

## 边界

- 这是 MetaSUB 项目专用的数据清理和 ID 映射案例，不是可输入任意 SRA/BioSample accession 的通用工具。
- README 明确说许多字段不完整；映射质量依赖源工作表，遇到歧义或缺失时必须保留 unresolved。
- GitHub 上的 metadata 仓库公开，不代表 MetaSUB 的全部 data packet、reads 或 consortium 数据均公开。
- 城市/表面采样 metadata 不属于人体宿主临床或饮食信息。

## 来源

- [MetaSUB-metadata repository](https://github.com/MetaSUB/MetaSUB-metadata)
- [MetaSUB sample naming/storage documentation](https://metasub-bioinformatics.readthedocs.io/en/latest/data_storage.html)
- [MetaSUB global urban metagenome paper](https://doi.org/10.1016/j.cell.2021.05.002)
