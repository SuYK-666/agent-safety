# B37　BFCL

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　BFCL v4 全部 20 个题目分片、16 个标准答案分片、多轮函数文档与记忆前置对话

上游 unused_datasets（旧版废弃分片）未收。

**论文**　[The Berkeley Function Calling Leaderboard (BFCL) - From Tool Use to Agentic Evaluation of Large Language Models](<paper/The Berkeley Function Calling Leaderboard (BFCL) - From Tool Use to Agentic Evaluation of Large Language Models.pdf>) · 完整原件 22 页（含附录） · [上游 PDF](https://github.com/mlresearch/v267/blob/main/assets/patil25a/patil25a.pdf) · [发布页 1](https://proceedings.mlr.press/v267/patil25a.html) · [发布页 2](https://gorilla.cs.berkeley.edu/leaderboard.html) · [发布页 3](https://github.com/ShishirPatil/gorilla/blob/main/berkeley-function-call-leaderboard/bfcl_eval/data/BFCL_v4_multi_turn_base.json)

**上游入口**　[项目或数据 1](https://github.com/ShishirPatil/gorilla/tree/main/berkeley-function-call-leaderboard)


## 测试集

**来源**　[GitHub ShishirPatil/gorilla](https://github.com/ShishirPatil/gorilla)

**位置**　[`data/upstream/`](data/upstream/) · 54 个文件 · 10.4 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/BFCL_v4_format_sensitivity.json`](<data/upstream/data/BFCL_v4_format_sensitivity.json>) | 200 | 4 KB |
| [`upstream/data/BFCL_v4_irrelevance.json`](<data/upstream/data/BFCL_v4_irrelevance.json>) | 240 | 156 KB |
| [`upstream/data/BFCL_v4_live_irrelevance.json`](<data/upstream/data/BFCL_v4_live_irrelevance.json>) | 884 | 2.1 MB |
| [`upstream/data/BFCL_v4_live_multiple.json`](<data/upstream/data/BFCL_v4_live_multiple.json>) | 1,053 | 3.7 MB |
| [`upstream/data/BFCL_v4_live_parallel.json`](<data/upstream/data/BFCL_v4_live_parallel.json>) | 16 | 15 KB |
| [`upstream/data/BFCL_v4_live_parallel_multiple.json`](<data/upstream/data/BFCL_v4_live_parallel_multiple.json>) | 24 | 80 KB |
| [`upstream/data/BFCL_v4_live_relevance.json`](<data/upstream/data/BFCL_v4_live_relevance.json>) | 16 | 46 KB |
| [`upstream/data/BFCL_v4_live_simple.json`](<data/upstream/data/BFCL_v4_live_simple.json>) | 258 | 254 KB |
| [`upstream/data/BFCL_v4_memory.json`](<data/upstream/data/BFCL_v4_memory.json>) | 155 | 32 KB |
| [`upstream/data/BFCL_v4_multi_turn_base.json`](<data/upstream/data/BFCL_v4_multi_turn_base.json>) | 200 | 381 KB |
| [`upstream/data/BFCL_v4_multi_turn_long_context.json`](<data/upstream/data/BFCL_v4_multi_turn_long_context.json>) | 200 | 382 KB |
| [`upstream/data/BFCL_v4_multi_turn_miss_func.json`](<data/upstream/data/BFCL_v4_multi_turn_miss_func.json>) | 200 | 391 KB |
| [`upstream/data/BFCL_v4_multi_turn_miss_param.json`](<data/upstream/data/BFCL_v4_multi_turn_miss_param.json>) | 200 | 393 KB |
| [`upstream/data/BFCL_v4_multiple.json`](<data/upstream/data/BFCL_v4_multiple.json>) | 200 | 309 KB |

另有 39 个数据文件未逐一列出。

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　发布方旧版约 2,000 问题—函数—答案组；V4 以子集发布

**任务与判分设置**　单轮 AST 与执行、多轮、记忆和代理搜索指标不同；用作工具能力及过度拦截对照

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/`](data/) · 55 个文件（含 `data/upstream*/` 测试集），逐文件地址、计数与校验值见[文件清单](../file-manifest.csv)。

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
