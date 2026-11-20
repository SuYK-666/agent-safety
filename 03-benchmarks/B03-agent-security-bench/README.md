# B03　Agent Security Bench（ASB）

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　10 场景代理任务、400 条攻击工具（含激进/非激进各 200）、20 条正常工具、PoT 任务

上游 memory_db 为运行时向量库，非测试集，未收。

**论文**　[Agent Security Bench (ASB) - Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents](<paper/Agent Security Bench (ASB) - Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents.pdf>) · 完整原件 36 页（含附录） · [上游 PDF](https://proceedings.iclr.cc/paper_files/paper/2025/file/5750f91d8fb9d5c02bd8ad2c3b44456b-Paper-Conference.pdf) · [发布页 1](https://proceedings.iclr.cc/paper_files/paper/2025/hash/5750f91d8fb9d5c02bd8ad2c3b44456b-Abstract-Conference.html)

**上游入口**　[项目或数据 1](https://github.com/agiresearch/ASB)


## 测试集

**来源**　[GitHub agiresearch/ASB](https://github.com/agiresearch/ASB)

**位置**　[`data/upstream/`](data/upstream/) · 11 个文件 · 431 KB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/agent_task.jsonl`](<data/upstream/data/agent_task.jsonl>) | 10 | 4 KB |
| [`upstream/data/agent_task_pot.jsonl`](<data/upstream/data/agent_task_pot.jsonl>) | 5 | 2 KB |
| [`upstream/data/agent_task_pot_all.jsonl`](<data/upstream/data/agent_task_pot_all.jsonl>) | 42 | 1 KB |
| [`upstream/data/agent_task_pot_msg.jsonl`](<data/upstream/data/agent_task_pot_msg.jsonl>) | 5 | 3 KB |
| [`upstream/data/agent_task_test.jsonl`](<data/upstream/data/agent_task_test.jsonl>) | 1 | 1 KB |
| [`upstream/data/all_attack_tools.jsonl`](<data/upstream/data/all_attack_tools.jsonl>) | 400 | 204 KB |
| [`upstream/data/all_attack_tools_aggressive.jsonl`](<data/upstream/data/all_attack_tools_aggressive.jsonl>) | 200 | 102 KB |
| [`upstream/data/all_attack_tools_non_aggressive.jsonl`](<data/upstream/data/all_attack_tools_non_aggressive.jsonl>) | 200 | 101 KB |
| [`upstream/data/all_normal_tools.jsonl`](<data/upstream/data/all_normal_tools.jsonl>) | 20 | 8 KB |
| [`upstream/data/attack_tools_test.jsonl`](<data/upstream/data/attack_tools_test.jsonl>) | 1 | 1 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　10 应用场景、10 代理、400 余工具

**任务与判分设置**　跨模拟应用比较不同代理和安全控制；以特定攻击、代理和运行配置计算攻击表现及效用

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
