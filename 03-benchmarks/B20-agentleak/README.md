# B20　AgentLeak

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　1,000/100/100 场景原文件、冒烟集、内部通道轨迹样例、隐私缓存

原 *-privacy-view.jsonl 为字段裁剪视图，保留。

**论文**　[AgentLeak - A Benchmark for Internal-Channel Privacy Leakage in Multi-Agent LLM Systems](<paper/AgentLeak - A Benchmark for Internal-Channel Privacy Leakage in Multi-Agent LLM Systems.pdf>) · 完整原件 19 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2602.11510) · [发布页 1](https://arxiv.org/abs/2602.11510) · [发布页 2](https://ieeexplore.ieee.org/document/11569042/)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/humain2/AgentLeak)


## 测试集

**来源**　[GitHub Privatris/AgentLeak](https://github.com/Privatris/AgentLeak)

**位置**　[`data/upstream/`](data/upstream/) · 8 个文件 · 3.4 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/agentleak_data/datasets/ai4privacy_cache.json`](<data/upstream/agentleak_data/datasets/ai4privacy_cache.json>) | 20 | 11 KB |
| [`upstream/agentleak_data/datasets/clinical_cache.json`](<data/upstream/agentleak_data/datasets/clinical_cache.json>) | 20 | 7 KB |
| [`upstream/agentleak_data/datasets/scenarios_base_100.jsonl`](<data/upstream/agentleak_data/datasets/scenarios_base_100.jsonl>) | 100 | 305 KB |
| [`upstream/agentleak_data/datasets/scenarios_difficult_100.jsonl`](<data/upstream/agentleak_data/datasets/scenarios_difficult_100.jsonl>) | 100 | 286 KB |
| [`upstream/agentleak_data/datasets/scenarios_full_1000.jsonl`](<data/upstream/agentleak_data/datasets/scenarios_full_1000.jsonl>) | 1,000 | 2.7 MB |
| [`upstream/agentleak_data/datasets/smoke_test.jsonl`](<data/upstream/agentleak_data/datasets/smoke_test.jsonl>) | 2 | 5 KB |
| [`upstream/agentleak_data/datasets/traces_internal_channels.jsonl`](<data/upstream/agentleak_data/datasets/traces_internal_channels.jsonl>) | 3 | 1 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　1,000 场景、7 通道；论文重点实测其中 3 条

**任务与判分设置**　多代理终答、代理消息、共享记忆等内部流；依据场景敏感性及渠道权限判定泄露

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/scenarios_base_100-privacy-view.jsonl`](data/scenarios_base_100-privacy-view.jsonl) · 场景任务视图及风险标签 · 100
- [`data/scenarios_difficult_100-privacy-view.jsonl`](data/scenarios_difficult_100-privacy-view.jsonl) · 场景任务视图及风险标签 · 100
- [`data/scenarios_full_1000-privacy-view.jsonl`](data/scenarios_full_1000-privacy-view.jsonl) · 场景任务视图及风险标签 · 1000
- [`results/model_stats.json`](results/model_stats.json) · 上游原文件 · 聚合结果
- [`results/paper_stats.json`](results/paper_stats.json) · 上游原文件 · 聚合结果

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
