# B08　Agent-SafetyBench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　2,000 条测试用例（8 类风险，含环境、提示与标签）

原 released-case-labels.jsonl 与 ordinary-task-prompts.jsonl 为提取视图，保留。

**论文**　[Agent-SafetyBench - Evaluating the Safety of LLM Agents](<paper/Agent-SafetyBench - Evaluating the Safety of LLM Agents.pdf>) · 完整原件 26 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2412.14470) · [发布页 1](https://arxiv.org/abs/2412.14470)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/thu-coai/Agent-SafetyBench/tree/main)


## 测试集

**来源**　[HF thu-coai/Agent-SafetyBench](https://huggingface.co/datasets/thu-coai/Agent-SafetyBench)

**位置**　[`data/upstream/`](data/upstream/) · 2 个文件 · 2.7 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/released_data.json`](<data/upstream/released_data.json>) | 2,000 | 2.7 MB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　2,000 用例、349 交互环境、8 类风险、10 类故障模式

**任务与判分设置**　动态工具环境，覆盖恶意输入及代理自身误行为；以交互轨迹和安全分类器判定

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/ordinary-task-prompts.jsonl`](data/ordinary-task-prompts.jsonl) · 经筛选的正常任务提示词 · 34
- [`data/released-case-labels.jsonl`](data/released-case-labels.jsonl) · 逐条结构化标签，无原始交互 · 2000

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
