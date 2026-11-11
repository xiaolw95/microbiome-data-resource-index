# FoodMicrobionet

**类型：** 食品 16S/ITS 研究与样本数据库；**目录层级：** Extended；**状态：** active_verified（2026-11-10）

官方维护页报告 v5.1.2 含 302 项研究、17,174 个 bacterial samples 和 3,175 个 fungal samples。表结构覆盖 study、sample、SRA BioProject/BioSample/Run、食品描述、FoodEx2 和论文信息；提供 Shiny 浏览器、脚本和 Zenodo processed data。

**适用：** 按食品类型/食品环境发现研究，检查样本与 SRA accession、文献注释的连接。

**映射注意：** 论文指出细菌/真菌表和重复提交可能使一个生物样本出现多次，并加入 matchId 帮助跨表匹配。样本数不必然等于唯一 biological specimen 数。FoodEx2 食品类别也不等于 participant dietary exposure。

**来源：** [官方当前版本](https://web.unibas.it/parente/?page_id=761) · [GitHub](https://github.com/ep142/FoodMicrobionet) · [v5 论文](https://doi.org/10.3390/foods13111689) · [Zenodo](https://zenodo.org/records/18590893)
