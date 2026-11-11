# 母婴、多身体位点微生物组数据集检索指南

**首轮检索日期：** 2026-11-10　**索引：** [catalog/datasets.csv](../../catalog/datasets.csv)　**主题标签：** maternal_infant

## 1. 研究问题

从“我想找母婴微生物组”进一步筛选到：母亲和婴儿是否都采样、采了哪些身体位点、是否有母婴配对、采样时间是否纵向，以及是否能把这些信息对应回具体 BioSample/Experiment/Run。目标是帮助研究者发现候选数据，而不是仅根据论文描述推断每个样本的属性。

## 2. 范围与纳入标准

### 纳入

- 人类母亲/孕妇与新生儿/婴儿/儿童的微生物组研究；
- 至少有可核验的研究或项目 accession/数据下载入口；
- 研究报告一个或多个明确位点，例如母亲肠道、阴道、口腔、皮肤、鼻腔、乳汁，婴儿肠道、口腔、皮肤或鼻腔；
- 论文、官方归档或补充资料至少能确认人群、位点、assay、研究设计中的主要信息；
- 对“母婴配对”或“纵向”标签，须有研究设计或样本 crosswalk 依据。

### 排除或单独标记

- 只涉及动物或仅含益生菌菌株、不含母婴样本项目的资源；
- 只有母亲或只有婴儿样本、但没有足够关联信息证明其属于母婴研究的问题；此类项目可作为外围候选，不能标成配对队列；
- 论文提到饮食、健康或人群特征，但没有说明该变量是否对应到样本/受试者；仅保留为研究级描述；
- 同一研究被多个 BioProject、EGA dataset 或二次分析重复收录时，先保留所有 accession 及来源，完成样本去重前不合并计数。

## 3. 检索路径

### A. 先用专题整理资源缩小范围

1. 使用 [MAMI resource 下载页](https://bioinfo.ioz.ac.cn/mami/resource.php)，按 Mother/Infant 和身体位点查看 accession/abundance 表。MAMI 论文覆盖母亲六类位点和婴幼儿四类位点，并记录时间信息；它适合找专题候选，不是所有样本临床 metadata 的统一仓库。详见[资源卡](../resources/mami.md)。
2. 使用 [Microbiome Repo 的 mother-infant 筛选页](https://microbiomerepo.com/studies/index.html?sampling=mother_infant)发现公开 INSDC human shotgun DNA/RNA 项目。当前页面标记纵向、相关人群、多位点、病例对照和 metadata 申请等属性；它的筛选范围不是全 assay 的母婴微生物组全集，amplicon 项目仍应另行搜索。
3. 需要母婴肠道 16S 汇总 profiles 时，可从 [Human Microbiome Compendium](https://doi.org/10.5281/zenodo.8186993) 与 [GutBiomeDB](https://academic.oup.com/nar/advance-article/doi/10.1093/nar/gkag1125/9013047)追踪其中的研究 accession；不能假设这些资源提供所有身体位点或配对样本。

### B. 再到原始归档与论文补充材料核对

推荐分别使用 [NCBI SRA/BioProject](https://www.ncbi.nlm.nih.gov/sra/)、[ENA](https://www.ebi.ac.uk/ena/browser/home) 和 [DDBJ](https://www.ddbj.nig.ac.jp/dra/index-e.html)按 accession 与主题词检索。首轮检索词可组合：

- “mother-infant” OR maternal OR pregnancy OR newborn OR infant OR neonatal
- microbiome OR microbiota OR metagenome
- multi-site OR multiple body sites OR transmission OR longitudinal

常见身体位点和别名应同时检索并保留原文：stool/feces/faeces/gut、vagina/vaginal、breast milk/milk、oral/saliva/tongue、skin、nares/nasal/nasopharynx。找到项目后，依次打开 BioProject/Study、BioSample、Experiment、Run，检查样本标题、organism、isolation source、collection time、library strategy、论文和 supplement 的 accession crosswalk。

### C. 追踪论文和补充表中的宿主信息

- 用 PMID/DOI 在 Europe PMC、PMC 或期刊主页打开全文、Data Availability、Methods 与 Supplementary Tables。
- 优先查找把 sample ID/BioSample/SRA accession 连到 subject/dyad、visit、body site、时间点和 phenotype 的表。
- 对问卷、临床或敏感字段，检查是否另有 EGA/dbGaP 等受控数据集；“SRA reads public”不意味着所有个体 metadata 同样公开。
- 记录来源表格、sheet/列、信息层级以及缺失情况；饮食等作者在讨论中提及的变量，只有出现在具体研究表/问卷中且有 ID mapping 时才记为可复用 metadata。

## 4. 首轮可用候选

下表是第一轮可追踪候选，不代表该主题的穷尽清单。逐项目字段与链接见 [catalog/datasets.csv](../../catalog/datasets.csv)。

| 候选 | 主要价值 | 样本/计数口径 | 可获得信息与限制 |
|---|---|---|---|
| [PRJNA322188](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA322188) | 母亲/婴儿多身体位点，16S 与 WGS，纵向到约 6 周 | 论文：2,581 个采集 specimens，1,429 个进入 QC 后分析；NCBI：1,928 BioSamples、1,836 SRA Experiments | 论文和 archive 数量不等价；Methods/补充表给出队列流失、位点和时间信息。不能用 Experiment 数代替受试者数。[论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC5345907/) |
| [PRJNA352475](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA352475) | 25 个母婴 dyads，多母体位点，婴儿肠道/口腔；shotgun | 论文 25 dyads、216 个高质量 metagenomes；NCBI 230 BioSamples/Experiments | 论文补充表、SRA 和 curatedMetagenomicData 可互相核对；后者提供 profiles/metadata。[论文](https://pmc.ncbi.nlm.nih.gov/articles/6716579/) |
| [PRJNA833324 / MUIS](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA833324) | 120 个母婴 dyads，多母体/婴儿位点，16S V4 | 论文报告 2,453 个 samples；BioProject narrative 报告 2,319；当前 NCBI 页面列 1,842 BioSamples 和 1,842 SRA Experiments；120 dyads 与 4 位部分采样母亲 | 状态为 unresolved：论文与归档描述/当前 accession 记录数量不同，并提示部分数据曾在其他 BioProject 发布；按 BioSample ID 去重前不汇总唯一样本数。[论文](https://www.sciencedirect.com/science/article/pii/S1931312823000434) |
| [PRJNA911205](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA911205) | 121 母婴 dyads 的肠道 16S；89 dyads 有 WMS；含心理社会逆境研究 | 121 dyads；NCBI 458 BioSamples/Experiments | Supplementary Data 2 把详细 metadata 对到 SRA accession，并附标准化 abundance；适合检查 sample-to-host metadata crosswalk。[论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC10509221/) |
| [Lifelines NEXT / MOM MATTERS](https://www.ega-archive.org/studies/EGAS50000000133) | 714 dyads，孕期到婴儿 1 岁，多时间点；粪便、乳汁和阴道相关数据 | 论文报告 4,526 个纵向粪便 specimens；EGA 页面列出 4,577 条 fecal metagenomics/phenotype-linked records | SRA 有一部分公开去人源 shotgun reads；问卷和临床 metadata 及部分 reads 需 EGA/Lifelines 申请。EGA 项目页列出生长、孕周、产次、母亲年龄、吸烟、高血压、婴儿性别、分娩方式、出生体重、母乳喂养和 eczema 等字段。[论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC13626959/) |

EGA 计数与论文样本计数可能来自不同 release/freeze 或记录口径；目录保留各自来源，不将 4,577 直接当作 unique biological specimens。

## 5. 适合检索的 metadata 范围

| 信息域 | 可能来源 | 需要确认的映射 |
|---|---|---|
| 年龄、孕周、产次 | BioSample attributes、Methods、问卷、EGA | 受试者 vs 采样 visit；采样时年龄和出生日期不可混用 |
| 性别、种族/民族、人群/地点 | BioSample、论文表格、supplements、EGA | 研究队列层 vs 具体 subject/sample；分类名以作者原文为准 |
| 身体位点、采样时间、分娩方式 | BioSample、SRA sample title、样本 crosswalk、补充表 | 每个 specimen 的 host、visit、site 与 Run 映射 |
| 喂养、饮食、抗生素、健康状态 | 问卷、临床表、正文和 supplements；有时受控 | 变量测量窗口、定义、是否可连接至 subject/dyad |
| 测序策略、平台、文库/Run | SRA/ENA/DDBJ Experiment/Run | Experiment 或 Run 层；同一生物样本可有多次测序 |

目录字段只能记录“来源明确支持的可用领域”。例如某论文分析过母亲饮食，并不自动说明每个 SRA 样本都有饮食值或可链接饮食变量。

## 6. 建议的复现与筛选记录

每个项目至少保存：查询式/资源、检索日、原始题名、稳定 accession、论文 DOI/PMID、作者报告人群和位点、assay、研究 count 与单位、BioSample/Experiment/Run 数、补充文件/表格定位、开放/受控状态、metadata scope、pairing 是否能回到具体 ID、判断理由和 unresolved 项。

## 7. 限制与待扩展项

- 这是首轮索引，不保证穷尽已发表研究；后续应追踪 MAMI 引用、Microbiome Repo 的新增项目、母婴系统综述和 SRA/ENA 新提交。
- 历史 accession 可能重复包含在不同项目或二次分析中；统一样本数需要对 BioSample/样本名去重和人工复核。
- 样本与受试者、dyad、visit 可能是一对多或多对多关系；没有 crosswalk 时只能记录研究级信息。
- 一些高价值临床/问卷信息受控访问，公开 accession 只能作为发现入口。
