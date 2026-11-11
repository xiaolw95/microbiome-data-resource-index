# iMicrobe

**类型：** 微生物组数据发现与计算平台　**目录层级：** Legacy　**状态：** legacy

## 它是什么

iMicrobe 曾将项目、样本 metadata、分析产品和远程文件存储连接到一个微生物组搜索与计算平台。它被描述为 data broker/search platform，而非把所有序列统一托管在单一 archive 中。

## 历史上可提供什么

- 按项目、样本和多个 metadata 字段发现微生物组数据；旧版文档称样本搜索覆盖 250 多个字段；
- 查看项目、样本、reads、gene calls、contigs、assemblies 等对象，并链接到 CyVerse Data Store 或外部归档；
- 连接 CAMERA 等环境微生物组数据和可在平台运行的分析应用。

## 当前使用边界

本轮检查时官方主站返回 HTTP 502；文档页仍可访问，但内容最后更新约为 2019 年。`grabseqs` 1.0.0 在 2025 年明确移除了 iMicrobe 支持。因此本项目将它保留为历史发现入口，任何 ID、外链或远程数据路径在使用前都必须重新核实。iMicrobe 历史上可搜索的字段不能被当作当前可访问的记录。

旧版官方文档曾将数据路径指向 CyVerse Data Commons 的 `/iplant/home/shared/imicrobe` 以及 iMicrobe FTP。当前 Data Commons URL 能加载目录应用外壳，但本轮未确认该路径下具体数据清单或文件可读；这些仅作为可复核的历史镜像线索，不视为已验证的替代数据服务。

## 官方来源

- [iMicrobe 官方站点](https://www.imicrobe.us/)
- [iMicrobe 搜索说明](https://hurwitzlab.gitbook.io/imicrobe/getting-started-1/searching-for-datasets)
- [旧版文档记录的 CyVerse Data Commons 路径](https://datacommons.cyverse.org/browse/iplant/home/shared/imicrobe)
- [CyVerse Data Commons 说明](https://docs.cyverse.org/platform/data-commons/)
- [iMicrobe 平台说明](https://hurwitzlab.gitbook.io/imicrobe/general/untitled)
- [2019 GigaScience 论文](https://doi.org/10.1093/gigascience/giz083)
- [grabseqs 现行文档（记录其 iMicrobe 支持已移除）](https://github.com/louiejtaylor/grabseqs)
