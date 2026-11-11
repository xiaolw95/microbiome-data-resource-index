# 资源关系与证据链

本项目将资源视为互相链接、但功能不同的节点：原始归档保存序列和提交者 metadata；论文解释研究设计并链接 accession；supplement 可能提供 accession 到 subject/visit/body-site 的 crosswalk；整理型数据库对部分项目进行筛选、字段标准化或统一分析；受控 archive 保存隐私敏感的临床/问卷信息。

## 从研究问题发现数据

~~~mermaid
flowchart TD
    Q[研究问题<br/>母婴多位点 / CRC / 其他主题] --> R[专题资源与综述检索<br/>MAMI / Microbiome Repo / curated collections]
    R --> C[候选研究与论文]
    C --> P[项目 accession<br/>BioProject / ENA Study / DDBJ / GSA CRA]
    P --> A[原始归档对象<br/>BioSample / SAMC → Experiment → Run]
    C --> S[论文补充材料<br/>sample crosswalk / phenotype / visit]
    C --> H[受控数据入口<br/>EGA / dbGaP / DAC]
    A --> V[逐项目核验<br/>body site / assay / access / ID mapping]
    S --> V
    H --> V
    V --> O[本地轻量结果<br/>datasets.csv + 专题指南]
~~~

## 从样本或 accession 查询 metadata 的证据链

~~~mermaid
flowchart LR
    I[输入 accession] --> X[识别 accession 类型]
    X --> P[BioProject / Study]
    X --> B[BioSample]
    X --> E[Experiment / Library]
    X --> U[Run]
    P --> L[文章与数据可用性声明]
    B --> M[提交者样本字段]
    E --> T[文库策略 / 平台]
    U --> F[文件 / spots / bases]
    L --> D[补充表与 sample crosswalk]
    D --> G[样本 / subject / visit / phenotype evidence ledger]
    M --> G
    T --> G
    F --> G
    G --> Z[输出字段值、信息层级、来源链接、访问状态和不确定性]
~~~

这张图是后续自研工具的目标流程草图，不代表本仓库当前已有自动检索器。

## 不同资源补充的信息

| 信息来源 | 通常最强的信息 | 常见缺口/边界 |
|---|---|---|
| SRA / ENA / DDBJ / GSA | Study/Project（含 CRA/PRJCA）、BioSample/SAMC、Experiment、Run、library、sequencing platform、raw reads | 跨库整合时按原始 accession 去重；host/body-site/age 等由 submitter 提交；临床/生活方式字段不保证存在 |
| GSA-Human | 人类研究的 Study、Individual、Sample、Experiment、Run 及 DAC/申请路径 | 部分表型/临床信息受控；有 GSA-Human ID 不代表能自动映射到 INSDC BioSample 或取得受控字段 |
| BioSample | 样本属性和值 | 术语自由文本、缺失字段、同一 subject 多 samples/records |
| 论文正文 | 研究设计、纳入标准、队列层特征、变量定义、分析流程 | 文章表述可能只适用于队列，不一定可映射至所有样本 |
| Supplementary files | accession/sample ID crosswalk、个体/时间点/位点信息、原始样本表 | 文件格式复杂、变量版本不一致、可能缺少永久链接或受控 |
| Curated dataset | 标准化 disease/body_site metadata、taxonomic/functional profiles、筛选后的 cohorts | 覆盖限于某宿主/assay/部位；可能剔除样本或应用过滤 |
| Celeri Explorer | 从 ENA XML 派生的 AI-structured 人体肠道研究/样本字段 | AI 结构化不等于人工校验；目前未确认对论文 supplements 的补采，且同步和使用条款需复核 |
| Mica | 饮食/营养与肠道菌群研究的变量、队列与 harmonization protocol 目录 | 研究级信息发现不能替代个体数据访问申请或 BioSample/Run crosswalk |
| OmicsMLRepoR + cMD | cMD 人体 shotgun harmonized metadata 与 ontology-based query | 只覆盖其已发布的数据包，不能从任意 accession 自动找到论文/supplement |
| Microbiome Research Data Toolkit | 前瞻采集和 retrospective harmonization 的字段/表单设计 | 是规范与采集工具，不含公开样本记录或 accession 查询服务 |
| EGA / dbGaP | 受控 clinical/questionnaire/host genotype 与受控数据的申请路径 | 需获批；公开 API 只提供公开 metadata；不可绕过许可 |
| Ontologies/checklists | 可复用术语、报告字段、字段含义 | 不提供研究中的实际样本值，也不补齐缺失事实 |

## 信息来源优先级

1. 官方 archive/API 的 sample/experiment/run 记录；
2. 原始论文的 Methods、Results、Data Availability；
3. 论文 supplement 的具体表、sheet、列或样本 ID；
4. curated resource 的数据字典、记录页和 release；
5. 综述、注册库、第三方列表用于发现候选，不单独支撑样本级事实。

每一个未来的 metadata claim 都应携带 source URL、证据定位、信息层级（study/cohort/subject/visit/sample/library/run）、提取日期和状态说明。没有可靠 crosswalk 时，保留上游层级。
