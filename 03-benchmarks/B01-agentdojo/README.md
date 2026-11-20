# B01　AgentDojo

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　4 套件（banking、slack、travel、workspace）全部环境 YAML、注入向量与 v1–v1.2.2 各版本 user/injection 任务定义

AgentDojo 任务以 Python 类定义，环境与注入点为 YAML；上游无独立 JSON 题库，故收录任务定义原文件。原 user-tasks-static.json 为静态提取视图，保留。

**论文**　[AgentDojo - A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents](<paper/AgentDojo - A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents.pdf>) · 完整原件 26 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2406.13352) · [发布页 1](https://papers.nips.cc/paper_files/paper/2024/hash/97091a5177d8dc64b1da8bf3e1f6fb54-Abstract-Datasets_and_Benchmarks_Track.html)

**上游入口**　[项目或数据 1](https://github.com/ethz-spylab/agentdojo)


## 测试集

**来源**　[GitHub ethz-spylab/agentdojo](https://github.com/ethz-spylab/agentdojo)

**位置**　[`data/upstream/`](data/upstream/) · 38 个文件 · 481 KB

成组目录：

- [`upstream/default_suites/`](<data/upstream/default_suites/>) · v1–v1.2.2 各版本 user/injection 任务定义 · 26 个文件
- [`upstream/data/suites/`](<data/upstream/data/suites/>) · 4 套件环境与注入向量 YAML · 11 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　97 正常任务；629 安全任务配对（论文）

**任务与判分设置**　工作区、出行、银行、Slack；同任务分别观测常态成功、受扰时效用和状态化安全结果，版本更新可改变配对数

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/banking/user-tasks-static.json`](data/banking/user-tasks-static.json) · 静态提取，保留评测字段 · 16
- [`data/slack/user-tasks-static.json`](data/slack/user-tasks-static.json) · 静态提取，保留评测字段 · 17
- [`data/travel/user-tasks-static.json`](data/travel/user-tasks-static.json) · 静态提取，保留评测字段 · 20
- [`data/workspace/user-tasks-static.json`](data/workspace/user-tasks-static.json) · 静态提取，保留评测字段 · 33

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
