# B16　AuthorizationBench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　286 个 vignette、286 个可执行任务目录（提示、夹具、记忆、配置）、种子、来源清单与分类法

固定提交 bfe1fc27。原 vignette-labels.jsonl 为提取视图，保留。

**论文**　[Act on Your Behalf, Beyond Your Authorization - Benchmarking LLM Agent Authorization Alignment](<paper/Act on Your Behalf, Beyond Your Authorization - Benchmarking LLM Agent Authorization Alignment.pdf>) · 完整原件 24 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2610.27548) · [发布页 1](https://arxiv.org/abs/2610.27548)

**上游入口**　[项目或数据 1](https://github.com/PEACH-Research-Lab/AuthorizationBench)


## 测试集

**来源**　[GitHub PEACH-Research-Lab/AuthorizationBench](https://github.com/PEACH-Research-Lab/AuthorizationBench)

**位置**　[`data/upstream/`](data/upstream/) · 6322 个文件 · 19.6 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/authorization_eva_sandbox/seeds/seed.json`](<data/upstream/authorization_eva_sandbox/seeds/seed.json>) | 44 | 56 KB |
| [`upstream/authorization_eva_sandbox/seeds/seed_template.json`](<data/upstream/authorization_eva_sandbox/seeds/seed_template.json>) | — | 1 KB |
| [`upstream/benchmark/lineage.csv`](<data/upstream/benchmark/lineage.csv>) | 286 | 10 KB |
| [`upstream/benchmark/manifest.json`](<data/upstream/benchmark/manifest.json>) | — | 6 KB |

成组目录：

- [`upstream/authorization_eva_sandbox/vignettes/`](<data/upstream/authorization_eva_sandbox/vignettes/>) · 286 个 vignette 定义 JSON · 286 个文件
- [`upstream/authorization_eva_sandbox/tasks/`](<data/upstream/authorization_eva_sandbox/tasks/>) · 286 个可执行任务目录（系统提示、夹具、先验记忆、任务配置） · 6029 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　286 任务、10 领域、14 类情境压力；6,864 条运行判决，4,981 条保留原轨迹

**任务与判分设置**　真实案例构造成授权约定；确定性模拟服务允许观察有无直接伤害两种情况下的越界与合法完成

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/vignette-labels.jsonl`](data/vignette-labels.jsonl) · 逐条结构化标签，无原始交互 · 286

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
