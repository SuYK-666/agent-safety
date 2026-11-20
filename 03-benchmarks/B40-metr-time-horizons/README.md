# B40　METR Time Horizons

## 本包材料

**数据收录**　公开结果数据

**实收规模**　Time Horizon 1.0（41,629 条）与 1.1（24,008 条）原始运行记录

METR 任务本体大多私有，公开的是逐次运行结果。

**论文**　[Measuring AI Ability to Complete Long Software Tasks](<paper/Measuring AI Ability to Complete Long Software Tasks.pdf>) · 完整原件 45 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2503.14499) · [发布页 1](https://metr.org/time-horizons/) · [发布页 2](https://metr.org/assets/task_results_1_1.yaml) · [发布页 3](https://metr.org/assets/benchmark_results_1_1.yaml)

**上游入口**　[项目或数据 1](https://metr.org/time-horizons/)


## 测试集

**来源**　[GitHub METR/eval-analysis-public](https://github.com/METR/eval-analysis-public)

**位置**　[`data/upstream/`](data/upstream/) · 2 个文件 · 37.2 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/reports/time-horizon-1-0/data/raw/runs.jsonl`](<data/upstream/reports/time-horizon-1-0/data/raw/runs.jsonl>) | 41,629 | 22.9 MB |
| [`upstream/reports/time-horizon-1-1/data/raw/runs.jsonl`](<data/upstream/reports/time-horizon-1-1/data/raw/runs.jsonl>) | 24,008 | 14.3 MB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　滚动任务集，公开主页面称逾 100 个多样化软件任务；滚动更新

**任务与判分设置**　按人类耗时与成功概率拟合任务跨度，区分 T50、T80 与任务版本；用作时长分层参考

## 本地文件

- [`results/model-horizon-summary.json`](results/model-horizon-summary.json) · 由官方 YAML 提取事实结果 · 26
- [`results/task-level-metrics.json`](results/task-level-metrics.json) · 由官方 YAML 提取事实结果 · 23

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
