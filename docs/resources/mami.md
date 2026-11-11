# MAMI (Microbiome Atlas of Mothers and Infants)

**类型：** 母婴微生物组整理型数据库　**优先级：** Core　**状态：** `active_verified`（首轮核对：2026-11-10）

## 用途

MAMI 汇集母亲和婴幼儿微生物组研究，并提供按人群类别和身体位点组织的 accession 清单及丰度表；该站点还收录适用于婴幼儿的益生菌相关资源。它适合作为“从母婴研究问题发现候选项目”的专题入口，而不是所有 accession 的实时通用解析器。

## 覆盖对象

数据库论文描述母亲的六类采样位点：肠道、皮肤、鼻腔、口腔、阴道和母乳；婴幼儿包括肠道、皮肤、鼻腔和口腔。论文还说明其整理了来源国家、临床特征和采样时间信息。网站下载区按 Mother/Infant 和 body site 分组，提供 accession 文本和 abundance 表。

## 如何使用

1. 打开 [MAMI resource 页面](https://bioinfo.ioz.ac.cn/mami/resource.php)。
2. 先按 Mother/Infant 选择人群，再选择 gut、vagina、breast milk、skin、oral cavity、nasal cavity 等位点。
3. 下载对应的 accession 列表，回到 INSDC 原始归档核查 BioSample、Experiment、Run、原始字段和数据下载入口。
4. 将 MAMI 的 abundance 表视为整理结果；如需研究设计、样本配对、年龄、饮食或临床指标，继续回查原论文和补充表。

## 能提供的信息与限制

- **适合：** 母亲与婴幼儿分组、多身体位点的候选 accession 发现，以及已整理的微生物丰度信息。
- **不应假设：** 每个 accession 都有年龄、性别、饮食、健康状态、母婴配对 ID 或原始 FASTQ 直链；这些字段受每项原始研究提交内容和 MAMI 的整理范围影响。
- **权限与许可：** MAMI 可公开浏览/下载其页面所列资源，但下游原始研究的许可和访问限制仍应分别核实。
- **数据层级：** accession/abundance 表可能指向样本或研究，不应把母亲/婴儿的研究级信息直接赋值给每个样本，除非有清楚的 crosswalk。

## 来源

- [MAMI 官方资源页面](https://bioinfo.ioz.ac.cn/mami/resource.php)
- [MAMI 数据库论文](https://doi.org/10.1093/nar/gkad813)
- [论文全文与数据库覆盖说明](https://academic.oup.com/nar/article/52/D1/D738/7306670)
