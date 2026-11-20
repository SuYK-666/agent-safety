# B24　MCP Security Bench（MSB）

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　2,000 条攻击实例清单、65 条代理任务、攻击任务与类型、各 MCP 工具规格

攻击工具服务器实现（.py）未收，仅收工具规格 JSON。

**论文**　[MCP Security Bench (MSB) - Benchmarking Attacks Against Model Context Protocol in LLM Agents](<paper/MCP Security Bench (MSB) - Benchmarking Attacks Against Model Context Protocol in LLM Agents.pdf>) · 完整原件 32 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2510.15994) · [发布页 1](https://arxiv.org/abs/2510.15994) · [发布页 2](https://arxiv.org/html/2510.15994)


## 测试集

**来源**　[HF dongsenzhang/MSB](https://huggingface.co/datasets/dongsenzhang/MSB)

**位置**　[`data/upstream/`](data/upstream/) · 38 个文件 · 495 KB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/case_manifest.jsonl`](<data/upstream/case_manifest.jsonl>) | 2,000 | 471 KB |
| [`upstream/data/agent_task.jsonl`](<data/upstream/data/agent_task.jsonl>) | 10 | 8 KB |
| [`upstream/data/attack_task.jsonl`](<data/upstream/data/attack_task.jsonl>) | 5 | 1 KB |
| [`upstream/data/attack_type.jsonl`](<data/upstream/data/attack_type.jsonl>) | 1 | 1 KB |

成组目录：

- [`upstream/data/tools/`](<data/upstream/data/tools/>) · MCP 工具规格 JSON（正常与攻击工具） · 33 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　12 类对抗；论文按配置报告运行

**任务与判分设置**　端到端比较规划、工具调用及响应处理；兼看正常完成、风险事件与 NRP 组合计分

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
