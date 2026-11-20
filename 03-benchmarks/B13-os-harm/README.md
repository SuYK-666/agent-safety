# B13　OS-Harm

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　GitHub 版索引（滥用 50、注入 10、误行为 50）与 OSWorld 369 条索引；HF 版 83 个任务配置、149 行 Parquet、任务资产

assets/ 中含任务环境用的示例文件与小脚本，属测试夹具。原 misbehavior-user-task-view.json 为提取视图，保留。

**论文**　[OS-Harm - A Benchmark for Measuring Safety of Computer Use Agents](<paper/OS-Harm - A Benchmark for Measuring Safety of Computer Use Agents.pdf>) · 完整原件 32 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2506.14866) · [发布页 1](https://papers.neurips.cc/paper_files/paper/2025/hash/4009bff0cd87ba2203c8e3a2f082aaec-Abstract-Datasets_and_Benchmarks_Track.html)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/thomas-kuntz/os-harm)


## 测试集

**来源**　[HF thomas-kuntz/os-harm](https://huggingface.co/datasets/thomas-kuntz/os-harm) · [GitHub tml-epfl/os-harm](https://github.com/tml-epfl/os-harm)

**位置**　[`data/upstream/`](data/upstream/) · 145 个文件 · 8.9 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/test-00000-of-00001.parquet`](<data/upstream/data/test-00000-of-00001.parquet>) | 149 | 17 KB |
| [`upstream/evaluation_examples/test_injection.json`](<data/upstream/evaluation_examples/test_injection.json>) | 10 | 1 KB |
| [`upstream/evaluation_examples/test_misbehavior.json`](<data/upstream/evaluation_examples/test_misbehavior.json>) | 50 | 1 KB |
| [`upstream/evaluation_examples/test_misuse.json`](<data/upstream/evaluation_examples/test_misuse.json>) | 50 | 1 KB |
| [`upstream/evaluation_examples/test_osworld_all.json`](<data/upstream/evaluation_examples/test_osworld_all.json>) | 369 | 16 KB |
| [`upstream/evaluation_examples/test_osworld_small.json`](<data/upstream/evaluation_examples/test_osworld_small.json>) | 39 | 1 KB |
| [`upstream/test_injection.json`](<data/upstream/test_injection.json>) | 10 | 1 KB |
| [`upstream/test_misbehavior.json`](<data/upstream/test_misbehavior.json>) | 50 | 1 KB |
| [`upstream/test_misuse.json`](<data/upstream/test_misuse.json>) | 25 | 1 KB |

成组目录：

- [`upstream/tasks/`](<data/upstream/tasks/>) · 83 个任务配置 JSON（HF 版，按应用分目录） · 83 个文件
- [`upstream/assets/`](<data/upstream/assets/>) · 任务资产（文档、截图、邮件与示例仓库） · 52 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　150 桌面任务；3 类风险

**任务与判分设置**　OSWorld 环境中测用户故意滥用、间接输入干扰、代理误行为；依据动作与桌面观察评分

## 本地文件

- [`LICENSE-UPSTREAM-GITHUB.txt`](LICENSE-UPSTREAM-GITHUB.txt) · 许可
- [`data/misbehavior-user-task-view.json`](data/misbehavior-user-task-view.json) · 正常桌面任务提示词 · 50

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
