# VirJenDB

**资源类型：** microbial knowledgebase / viral sequence platform　**优先级：** extended　**相关性：** supporting　**状态：** `active_verified`（官网标示 v1.1.3；本轮未调用 API）　**核查：** 2026-11-11

## 能提供什么

VirJenDB 官网搜索结果显示当前 release 为 v1.1.3；官方字段目录列出 sequence accession、BioSample、BioProject、SRA accession、collection date/location、host species、部分 host age/sex、病毒 taxonomy、序列来源与分析流程。mapping 文件可下载为 CSV/JSON/XLSX/TXT；官方文档说明有 REST/OpenAPI 搜索、下载和 metadata endpoints。此轮依据官网索引页与官方字段文档核实核心能力，未调用 API 或验证具体 accession。

## 适合什么任务

- 查询公共病毒序列 accession 与其 BioSample、BioProject、SRA 的交叉链接。
- 检索 viral host、采样时间/地点、宿主组织等字段，并追溯这些字段来自哪个上游库。
- 获取统一 metadata schema、字段定义及可供程序调用的查询接口。

## 边界与注意事项

- 资源对象是病毒序列记录，宿主字段的完整度和标准化程度依上游来源不同；页面明确标出部分字段尚未统一。
- 某个 virus sequence 记录的宿主信息不一定等同于用户输入微生物组 BioSample 的受试者信息。
- API/Swagger 页面无法由本轮浏览工具解析；官网可索引到当前 release 和搜索入口，但不将此视为已验证 API 响应或逐 accession 映射。

## 入口与来源

- [VirJenDB portal](https://virjendb.org/) · [documentation](https://doc.virjendb.org/) · [metadata schema](https://doc.virjendb.org/pages/metadata.html)
- [API Swagger](https://api.virjendb.org/swagger) · [原始论文](https://doi.org/10.1093/nar/gkaf1224)

相关目录行：[`resources.csv`](../../catalog/resources.csv) 中 `virjendb`；API 条目见 [`tools.csv`](../../catalog/tools.csv) 中 `virjendb_api`。
