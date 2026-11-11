# HoloFood Data Portal

**类型：** 动物生产系统的 host–microbiome 多组学项目门户与 REST API；**目录层级：** Core；**状态：** active_verified

门户可搜索样本和动物 accession、标题、处理条件、样本类型与 taxonomy，并导出过滤后的 TSV。官方 API 提供 sample、animal、analysis summary、genome catalogue 和 viral catalogue 端点；sample 记录连接 BioSamples、ENA、MGnify 和 MetaboLights。门户首页当前列出 9,889 个 samples、12,557 个 genomes 和 128,888 条 viral sequences。

**适用：** 从鸡/鲑鱼等养殖动物和 feed intervention 研究查找样本、动物、处理/喂养条件、采样时间、代谢组和宏基因组链接。API 明确区分宿主动物与其衍生的样本，适合研究 host-to-specimen-to-assay 关系。

**限制：** HoloFood 是特定项目门户，不能视为覆盖所有动物微生物组的通用数据库。处理条件属于动物或 trial metadata 时，不能未经验证复制给每个样本；数据文件许可应按其链接的 archive 和研究逐项判断。

**来源：** [门户](https://www.holofooddata.org/) · [API 文档](https://docs.holofooddata.org/api.html) · [网站使用说明](https://docs.holofooddata.org/website.html) · [原始论文](https://doi.org/10.1093/database/baae112)
