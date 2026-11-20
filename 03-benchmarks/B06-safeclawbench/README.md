# B06　SafeClawBench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　600 条主测试集、600/150/60 可执行夹具、72 条早期版本、Croissant 数据卡

测试集原文件存于 `data/upstream/`，与上游目录结构一致。

**论文**　[SafeClawBench - Separating Semantic, Audit-Evidence, and Sandbox Harm in Tool-Using LLM Agents](<paper/SafeClawBench - Separating Semantic, Audit-Evidence, and Sandbox Harm in Tool-Using LLM Agents.pdf>) · 完整原件 32 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2606.18356) · [发布页 1](https://arxiv.org/abs/2606.18356)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/sairights/safeclawbench)


## 测试集

**来源**　[HF sairights/safeclawbench](https://huggingface.co/datasets/sairights/safeclawbench)

**位置**　[`data/upstream/`](data/upstream/) · 10 个文件 · 2.6 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/benchmark_v5_600.json`](<data/upstream/benchmark_v5_600.json>) | 600 | 417 KB |
| [`upstream/croissant.json`](<data/upstream/croissant.json>) | — | 16 KB |
| [`upstream/executable/fixtures/exec_full_600.json`](<data/upstream/executable/fixtures/exec_full_600.json>) | 600 | 1.5 MB |
| [`upstream/executable/fixtures/exec_subset_150.json`](<data/upstream/executable/fixtures/exec_subset_150.json>) | 150 | 393 KB |
| [`upstream/executable/fixtures/exec_subset_60.json`](<data/upstream/executable/fixtures/exec_subset_60.json>) | 60 | 156 KB |
| [`upstream/executable/fixtures/tiny_subset.json`](<data/upstream/executable/fixtures/tiny_subset.json>) | 3 | 5 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　600 个任务；执行环境与语义集按题对应

**任务与判分设置**　语义反应、审计证据与受控环境内实际影响分别给分，预先定义状态断言

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
