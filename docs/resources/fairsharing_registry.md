# FAIRsharing

**类型：** standards / databases / policies 策展注册库；二级发现入口　**层级：** Extended　**核查：** 2026-11-11

## 它是什么

FAIRsharing 由人工策展与社区维护，互相链接描述数据库（包括研究数据仓库和知识库）、数据/报告标准及数据政策的记录。其价值是帮助判断某个主题有哪些资源、标准和政策，以及这些对象之间如何关联；它本身不存储这些数据库所收录的样本或测序数据。

## 适合怎么用

- 搜索 `microbiome`、`metagenome`、疾病、生态或测序相关主题，筛选 databases / standards / policies 类型；
- 打开记录，检查 scope、支持的标识符、访问模式、许可、关联标准和外部链接；
- 将其作为候选发现来源，再逐条回到官网和原始论文核实服务状态与可检索粒度。

## 程序化访问与限制

官方文档说明有 JSON API，GraphQL schema 可浏览，记录保留关联与修改历史。本轮 API 文档入口在非交互抓取中只显示 JavaScript shell；没有执行认证查询、分页遍历或导出。因此目录记录 API 为可发现能力，不声明本项目已全量扫描。FAIRsharing 内容说明为 CC BY-SA 4.0；具体 API 权限、认证和批量复用条件在脚本接入前应按官方当前条款确认。

## 官方来源

- [FAIRsharing](https://fairsharing.org/)
- [Getting Started](https://fairsharing.gitbook.io/fairsharing)
- [API 文档入口](https://fairsharing.org/API_doc)
- [GraphQL schema](https://api.fairsharing.org/schema/)
