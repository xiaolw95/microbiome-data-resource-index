# HLRMDB — Human Long-Read Metagenomics Database

**资源类型：** curated dataset　**优先级：** core　**相关性：** direct　**状态：** `active_verified`　**核查：** 2026-11-10

## 能提供什么

HLRMDB 面向人类相关长读长和 hybrid shotgun metagenomics。官网报告整理了 1,672 个数据集、38 项研究，涵盖 stool、oral cavity、airway 等采样情境以及健康/疾病状态；提供 sample-centric 与 genome-bin-centric 搜索、平台/化学版本筛选、taxonomy/function/ARG 结果和下载入口。样本记录可以继续关联到组装 MAG 与 gene/pathway 结果。

## 适合什么任务

- 找到公开的人体长读长或长短读混合宏基因组数据。
- 按采样上下文、健康状态、测序平台或 genome-bin 信息筛候选。
- 将 sample record 与组装质量、分类、功能和耐药特征联查。

## 边界与注意事项

- 这是固定范围的 curated collection，不是对任意 SRA/ENA accession 的通用实时解析服务。
- 官网声明学术使用免费，商业使用需联系项目方；下载或复用前核对条款。
- 页面摘要中的 health-state/context 是该资源整理的样本属性，不应推断为论文中所有受试者变量均可用。
- paired long-read / short-read accession 字段可能一行包含多个 Run；下游仍需保留 Run 与 biological sample 的关系。

## 入口与来源

- [HLRMDB 搜索主页](https://www.inbirg.com/hlrmdb/home) · [Downloads](https://www.inbirg.com/hlrmdb/downloads/)
- [原始论文](https://doi.org/10.1093/nar/gkaf1152) · [2026 correction](https://doi.org/10.1093/nar/gkag014)

相关目录行：[`resources.csv`](../../catalog/resources.csv) 中 `hlrmdb`。
