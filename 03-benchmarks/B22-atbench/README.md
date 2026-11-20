# B22　ATBench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　ATBench 1,000 条轨迹全集、ATBench500 500 条

HF 根目录 test.json 与 ATBench500/test.json 字节相同，未重复保存。原 test-labels/test-benign-trajectories 为提取视图，保留。

**论文**　[ATBench - A Diverse and Realistic Trajectory Benchmark for Long-Horizon Agent Safety](<paper/ATBench - A Diverse and Realistic Trajectory Benchmark for Long-Horizon Agent Safety.pdf>) · 完整原件 29 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2604.02022v1) · [发布页 1](https://arxiv.org/abs/2604.02022)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/AI45Research/ATBench/tree/main)


## 测试集

**来源**　[HF AI45Research/ATBench](https://huggingface.co/datasets/AI45Research/ATBench)

**位置**　[`data/upstream/`](data/upstream/) · 3 个文件 · 22.7 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/ATBench500/test.json`](<data/upstream/ATBench500/test.json>) | 500 | 5.2 MB |
| [`upstream/ATBench/test.json`](<data/upstream/ATBench/test.json>) | 1,000 | 17.5 MB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　新版本 1,000 轨迹；前版 ATBench500 为 500

**任务与判分设置**　长程工具交互，风险来源、失效、后果三轴，测试轨迹级检测，轨迹为离线材料

## 本地文件

- [`data/test-benign-trajectories.jsonl`](data/test-benign-trajectories.jsonl) · 保留对话结构的正常轨迹子集 · 248
- [`data/test-labels.jsonl`](data/test-labels.jsonl) · 逐条结构化标签，无原始交互 · 1000

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
