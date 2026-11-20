# B29　Cybench

## 本包材料

**数据收录**　公开测试集（元数据）

**实收规模**　40 个 CTF 任务的 metadata.json（提示、难度、子任务问答）与任务/子任务清单

各题目的挑战文件、Docker 环境与官方解题脚本未收。

**论文**　[Cybench - A Framework for Evaluating Cybersecurity Capabilities and Risks of Language Models](<paper/Cybench - A Framework for Evaluating Cybersecurity Capabilities and Risks of Language Models.pdf>) · 完整原件 150 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2408.08926) · [发布页 1](https://arxiv.org/abs/2408.08926)


## 测试集

**来源**　[GitHub andyzorigin/cybench](https://github.com/andyzorigin/cybench)

**位置**　[`data/upstream/`](data/upstream/) · 46 个文件 · 206 KB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/subtask_list.txt`](<data/upstream/subtask_list.txt>) | — | 2 KB |
| [`upstream/task_list.txt`](<data/upstream/task_list.txt>) | — | 2 KB |

成组目录：

- [`upstream/benchmark/`](<data/upstream/benchmark/>) · 40 个 CTF 任务 metadata.json（含子任务问答） · 43 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　4 场 CTF、40 专业任务

**任务与判分设置**　在指定环境测网络任务能力，分步骤辅助和无辅助得分单列

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
