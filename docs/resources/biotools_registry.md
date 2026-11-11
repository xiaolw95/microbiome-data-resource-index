# bio.tools

**类型：** 生命科学软件与服务注册目录；二级发现入口　**层级：** Extended　**核查：** 2026-11-11

## 它是什么

bio.tools 是 ELIXIR 生命科学工具平台中的社区维护注册库，记录软件、web services、数据库和工作流的名称、功能、EDAM 主题/操作、输入输出、格式、版本、许可和文档。它描述工具本身，并不代替工具执行，也不托管工具处理的研究数据。

## 如何搜索

- 在网页输入 accession 类型、metadata、microbiome、metagenome、SRA/ENA 等用途词；
- 有明确计算操作或文件类型时，使用 EDAM topic/operation/data/format 做概念筛选；
- 看工具记录中的官方文档、源代码、版本、license、引用和输入输出，再决定是否收入本项目的工具清单。

## API 与限制

公开 REST API 支持分页列出工具（默认 50 项/页）、全文查询、字段过滤、排序、单条详情与统计；只读查询不要求认证，写入和修改需 token。词语默认可能是 fuzzy search，精确过滤需要按 API 文档加引号。注册信息由开发者/社区维护，字段完整度与更新时间不完全一致。2026 年 NAR 更新论文报告注册库接近 33,000 条工具记录；其中只有经过本项目范围筛选且官方信息核验的工具才进入 `tools.csv`。

## 官方来源

- [bio.tools](https://bio.tools/)
- [API Quickstart](https://biotools.readthedocs.io/en/latest/api_quickstart.html)
- [API Reference](https://biotools.readthedocs.io/en/latest/api_reference.html)
- [2026 更新论文](https://doi.org/10.1093/nar/gkag420)
