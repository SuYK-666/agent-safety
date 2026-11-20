# B38　τ²-Bench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　航空 50、零售 114、电信 2,285（含 full/small/voice）、银行知识 97、intake 等全部领域任务、数据库、策略与文档

固定提交 c06b07dd。mock 测试域未收。

**论文**　[τ²-Bench - Evaluating Conversational Agents in a Dual-Control Environment](<paper/τ²-Bench - Evaluating Conversational Agents in a Dual-Control Environment.pdf>) · 完整原件 47 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2506.07982) · [发布页 1](https://arxiv.org/abs/2506.07982) · [发布页 2](https://github.com/sierra-research/tau2-bench/blob/main/data/tau2/domains/airline/split_tasks.json) · [发布页 3](https://github.com/sierra-research/tau2-bench/blob/main/data/tau2/domains/airline/tasks.json)

**上游入口**　[项目或数据 1](https://github.com/sierra-research/tau2-bench)


## 测试集

**来源**　[GitHub sierra-research/tau2-bench](https://github.com/sierra-research/tau2-bench)

**位置**　[`data/upstream/`](data/upstream/) · 879 个文件 · 137.9 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/domains/airline/audio_difficulty.json`](<data/upstream/domains/airline/audio_difficulty.json>) | — | 1.2 MB |
| [`upstream/domains/airline/db.json`](<data/upstream/domains/airline/db.json>) | — | 6.7 MB |
| [`upstream/domains/airline/split_tasks.json`](<data/upstream/domains/airline/split_tasks.json>) | 100 | 1 KB |
| [`upstream/domains/airline/tasks.json`](<data/upstream/domains/airline/tasks.json>) | 50 | 151 KB |
| [`upstream/domains/airline/tasks_voice.json`](<data/upstream/domains/airline/tasks_voice.json>) | — | 1.3 MB |
| [`upstream/domains/banking_knowledge/db.json`](<data/upstream/domains/banking_knowledge/db.json>) | — | 264 KB |
| [`upstream/domains/banking_knowledge/tasks.json`](<data/upstream/domains/banking_knowledge/tasks.json>) | 97 | 1.1 MB |
| [`upstream/domains/banking_knowledge/tasks_voice.json`](<data/upstream/domains/banking_knowledge/tasks_voice.json>) | — | 2.5 MB |
| [`upstream/domains/intake/split_tasks.json`](<data/upstream/domains/intake/split_tasks.json>) | 200 | 5 KB |
| [`upstream/domains/intake/tasks.json`](<data/upstream/domains/intake/tasks.json>) | 200 | 1014 KB |
| [`upstream/domains/intake/tasks.manifest.json`](<data/upstream/domains/intake/tasks.manifest.json>) | 200 | 106 KB |
| [`upstream/domains/retail/audio_difficulty.json`](<data/upstream/domains/retail/audio_difficulty.json>) | — | 2.0 MB |
| [`upstream/domains/retail/db.json`](<data/upstream/domains/retail/db.json>) | — | 2.7 MB |
| [`upstream/domains/retail/split_tasks.json`](<data/upstream/domains/retail/split_tasks.json>) | 228 | 3 KB |

另有 8 个数据文件未逐一列出。

成组目录：

- [`upstream/domains/banking_knowledge/`](<data/upstream/domains/banking_knowledge/>) · 银行知识域：任务、文档库与提示 · 815 个文件
- [`upstream/domains/retail/task_issues/`](<data/upstream/domains/retail/task_issues/>) · 零售任务问题记录 · 3 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　原论文航空 50、零售 115、电信 114，共 279 任务

**任务与判分设置**　航空与零售继承单边工具交互，电信为用户与代理双边工具；按最终状态核对任务，后续版本有子集与修订

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/`](data/) · 879 个文件（含 `data/upstream*/` 测试集），逐文件地址、计数与校验值见[文件清单](../file-manifest.csv)。

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
