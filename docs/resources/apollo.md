# APOLLO

**类型：** 人体微生物组代谢模型专题资源　**目录层级：** Extended　**状态：** `active_verified`　**已核查：** 2026-11-10

## 它是什么

APOLLO 是一套人体微生物基因组尺度代谢重建资源。2025 年论文报告 247,092 个 microbial genome-scale reconstructions，并基于公共宏基因组构建了 14,451 个 sample-specific microbiome community models；模型覆盖多身体位点、年龄组、疾病状态和 34 个国家。APOLLO 模型可通过 Virtual Metabolic Human（VMH）资源入口浏览。

## 可提供什么

- 微生物基因组代谢模型和按菌株/分类单元比较的代谢能力；
- 来自特定宏基因组样本的群落模型，用于研究样本层的潜在代谢通路；
- 按身体位点、年龄和疾病分层的模型分析上下文。

## 适用场景与边界

适用于微生物代谢、宿主—菌群—饮食—疾病机制建模。它不是原始测序 archive，也不能替代 BioSample 或论文中的参与者表型表。虽然论文描述了 sample-specific community models，但在每个模型是否都提供可复用的原始 sample accession crosswalk 前，应把模型的分层/代谢信息视作 supporting evidence，不自动反推或补齐个人饮食、临床变量。

模型文件和关联数据库受 VMH 页面及各文件条款约束；本文献的开放许可不应直接推广为所有模型文件的再分发许可。

## 官方来源

- [VMH](https://www.vmh.life/)
- [APOLLO 论文](https://doi.org/10.1016/j.cels.2025.101196)
- [VMH reconstructions](https://www.digitalmetabolictwin.org/reconstructions)
