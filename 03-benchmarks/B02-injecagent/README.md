# B02　InjecAgent

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　1,054 条组合用例（dh 510+ds 544，base 与 enhanced 两档）、17 用户案例、62 攻击者案例、工具与模拟响应

测试集原文件存于 `data/upstream/`，与上游目录结构一致。

**论文**　[InjecAgent - Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents](<paper/InjecAgent - Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents.pdf>) · 完整原件 36 页（含附录） · [上游 PDF](https://aclanthology.org/2024.findings-acl.624.pdf) · [发布页 1](https://aclanthology.org/2024.findings-acl.624/)

**上游入口**　[项目或数据 1](https://github.com/uiuc-kang-lab/InjecAgent)


## 测试集

**来源**　[GitHub uiuc-kang-lab/InjecAgent](https://github.com/uiuc-kang-lab/InjecAgent)

**位置**　[`data/upstream/`](data/upstream/) · 10 个文件 · 4.7 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/attacker_cases_dh.jsonl`](<data/upstream/data/attacker_cases_dh.jsonl>) | 30 | 10 KB |
| [`upstream/data/attacker_cases_ds.jsonl`](<data/upstream/data/attacker_cases_ds.jsonl>) | 32 | 12 KB |
| [`upstream/data/attacker_simulated_responses.json`](<data/upstream/data/attacker_simulated_responses.json>) | — | 1.3 MB |
| [`upstream/data/test_cases_dh_base.json`](<data/upstream/data/test_cases_dh_base.json>) | 510 | 657 KB |
| [`upstream/data/test_cases_dh_enhanced.json`](<data/upstream/data/test_cases_dh_enhanced.json>) | 510 | 704 KB |
| [`upstream/data/test_cases_ds_base.json`](<data/upstream/data/test_cases_ds_base.json>) | 544 | 747 KB |
| [`upstream/data/test_cases_ds_enhanced.json`](<data/upstream/data/test_cases_ds_enhanced.json>) | 544 | 798 KB |
| [`upstream/data/tools.json`](<data/upstream/data/tools.json>) | 38 | 528 KB |
| [`upstream/data/user_cases.jsonl`](<data/upstream/data/user_cases.jsonl>) | 17 | 10 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　1,054 用例；17 种用户工具、62 种攻击者工具

**任务与判分设置**　真实风格的工具返回与间接指令，观察下一步工具选择与有害目标是否达成

## 本地文件

- [`metadata/user-case-index.json`](metadata/user-case-index.json) · 逐条结构化标签，无原始交互 · 17

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
