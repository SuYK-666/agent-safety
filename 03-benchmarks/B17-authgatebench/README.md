# B17　AuthGateBench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　700 条实例（JSONL 与 Parquet 两种格式）

论文称 1,400 例，公开发布 700 条。

**论文**　[AuthGateBench - Benchmarking LLMs as Authorization Gate](<paper/AuthGateBench - Benchmarking LLMs as Authorization Gate.pdf>) · 完整原件 21 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2610.16426) · [发布页 1](https://arxiv.org/abs/2610.16426) · [发布页 2](https://www.alphaxiv.org/abs/2610.16426)


## 测试集

**来源**　[GitHub Digital-Trust-Lab/AuthGateBench](https://github.com/Digital-Trust-Lab/AuthGateBench)

**位置**　[`data/upstream/`](data/upstream/) · 3 个文件 · 2.4 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/authgatebench.jsonl`](<data/upstream/data/authgatebench.jsonl>) | 700 | 1.9 MB |
| [`upstream/data/authgatebench.parquet`](<data/upstream/data/authgatebench.parquet>) | 700 | 417 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　1,400 个实例、5 类故障模式

**任务与判分设置**　固定策略下给出良性高风险动作与上下文；判断允许、拒绝及环境信号的贡献，面向审批组件

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
