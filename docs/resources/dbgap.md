# NCBI Database of Genotypes and Phenotypes (dbGaP)

**类型：** 人类遗传与表型研究归档　**优先级：** Core　**状态：** `active_verified`（首轮核对：2026-11-10）

## 用途

dbGaP 是查找人类基因型—表型研究、研究说明、变量字典和受控个体级数据的重要入口。对于微生物组研究，它可能提供病例/对照、暴露、人口学或问卷信息，并能在提交结构中表达 subject 与测序样本之间的映射；具体是否包含 microbiome data，以及样本表和表型是否开放，需要逐 study 核对。

## 可提供什么

- 公开 study 页面、研究摘要、变量说明、数据字典和研究文件。
- 按 study 查询可用的 phenotype/genotype 数据范围与访问条件。
- 经批准的受控访问数据可包含去标识的个体级表型和基因型。
- dbGaP 提交格式包括 Subject Sample Mapping (SSM)，用于将 subject ID 映射到提交的样本；实际 study 是否提供可用 crosswalk 需查看文件 manifest 和访问级别。
- 测序数据可能另存于 SRA，并由 dbGaP 管理访问限制。

## 如何使用

1. 用 `phs` study accession 或研究主题在 [dbGaP](https://www.ncbi.nlm.nih.gov/gap/) 中定位 study。
2. 先查看公开 study summary、phenotype variables、study documents 和数据访问等级。
3. 如果需要单个受试者的 phenotype、样本映射表或受控 sequence data，查看该 study 的 DAC，并按要求提交 Data Use Certification；获批后才可获取受控文件。
4. 将 subject、sample/BioSample、library/Experiment 和 Run 分开保存。公开 summary 或变量字典不能当作个体行级数据，也不能保证存在公开 subject-to-BioSample crosswalk。

## 权限与隐私边界

公开 summary/变量说明通常无需预先批准；个体级 phenotype/genotype 数据受 study-specific DAC 管理，通常需研究用途说明、机构签署和 Data Use Certification。dbGaP 明确禁止尝试重新识别受试者。数据可用性及允许用途必须按具体 study 页面判断。

## 来源

- [dbGaP 官方概览与访问模式](https://www.ncbi.nlm.nih.gov/projects/gap/cgi-bin/about.html)
- [dbGaP study submission guide：subject/sample mapping](https://www.ncbi.nlm.nih.gov/gap/docs/submissionguide/)
- [dbGaP Authorized Access Portal](https://dbgap.ncbi.nlm.nih.gov/aa/landing/)
- [NCBI：dbGaP 项目的 SRA 测序数据说明](https://www.ncbi.nlm.nih.gov/sra/docs/submitdbgap/)
