# 智能体安全测评资料包

**2026-11-19**

| 目录                                         | 内容                                                                                                                                                       |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [01-report](01-report/agent-safety-research.md) | Markdown 报告，三张图在同目录 `figures/`                                                                                                                 |
| [02-frameworks](02-frameworks/README.md)        | OWASP、全国网安标委、AIIA、NIST 四份原文及对应发布入口                                                                                                     |
| [03-benchmarks](03-benchmarks/README.md)        | 按 `B编号-基准短名` 排列。每项有 README。论文全文存于 `paper/`，上游测试集原文件存于 `data/upstream*/`，其余提取视图与结果在 `data/`、`results/` |
| [04-indexes](04-indexes/benchmark-catalog.csv)  | 42 项标准资料、40 项基准状态、逐文件来源、许可与校验值                                                                                                     |

## 数据覆盖

- 测试集：29 项收录上游公开测试集全集，5 项收录作者公开的部分、元数据或结果（B07、B29、B30、B35、B40），B11 SafeArena 为需作者授权的 gated 数据集，B04、B15、B21、B25、B26 无公开测试集。上游原文件共 10,300 个、约 1.7 GB，逐项口径见各基准 README 与 [03-benchmarks/file-manifest.csv](03-benchmarks/file-manifest.csv)。
- 40 项基准中 38 项附论文全文 PDF（标题、摘要、正文至附录完整），文件以论文标题命名；B15 信通院 AI Safety Benchmark 与 B36 SOCBench 经核查无对应论文。论文文件的页数、来源与校验值见 [03-benchmarks/file-manifest.csv](03-benchmarks/file-manifest.csv)。
- 原文 PDF 由提交的资料包原字节移入。数据文档保留上游 license 或相应说明。对保留字段或统计事实重新排版的文件，清单标注衍生方式。
- 上游项目的任务分片和数据环境可能更新。诸如任务索引、挑选子集、论文结果、完整题集等覆盖状况在各基准目录分开说明。
- 归档校验可核对 [SHA256SUMS.txt](04-indexes/SHA256SUMS.txt)。按原路径解压后，报告中的本地链接和图片可离线查看。

可从 [逐项基准总表](03-benchmarks/README.md) 跳转，也可以按 [逐文件清单](04-indexes/file-manifest.csv) 中的编号、文件性质和来源筛选。
