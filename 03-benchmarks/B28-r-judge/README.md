# B28　R-Judge

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　27 个场景文件共 564 条多轮记录、数据模式

data/Program/security.json 被 Windows Defender 误报为 PHP 后门并自动删除，已改存为 security.json.gz（内容与上游字节一致，git blob f9587b37）。

**论文**　[R-Judge - Benchmarking Safety Risk Awareness for LLM Agents](<paper/R-Judge - Benchmarking Safety Risk Awareness for LLM Agents.pdf>) · 完整原件 24 页（含附录） · [上游 PDF](https://aclanthology.org/2024.findings-emnlp.79.pdf) · [发布页 1](https://aclanthology.org/2024.findings-emnlp.79/)

**上游入口**　[项目或数据 1](https://github.com/Lordog/R-Judge)


## 测试集

**来源**　[GitHub Lordog/R-Judge](https://github.com/Lordog/R-Judge)

**位置**　[`data/upstream/`](data/upstream/) · 28 个文件 · 1.7 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/config/data_schema.json`](<data/upstream/config/data_schema.json>) | — | 3 KB |
| [`upstream/data/Application/chatbot.json`](<data/upstream/data/Application/chatbot.json>) | 6 | 14 KB |
| [`upstream/data/Application/dh_app.json`](<data/upstream/data/Application/dh_app.json>) | 66 | 162 KB |
| [`upstream/data/Application/ds_app.json`](<data/upstream/data/Application/ds_app.json>) | 147 | 473 KB |
| [`upstream/data/Application/mail.json`](<data/upstream/data/Application/mail.json>) | 4 | 15 KB |
| [`upstream/data/Application/medical.json`](<data/upstream/data/Application/medical.json>) | 4 | 15 KB |
| [`upstream/data/Application/phone.json`](<data/upstream/data/Application/phone.json>) | 11 | 29 KB |
| [`upstream/data/Application/productivity.json`](<data/upstream/data/Application/productivity.json>) | 7 | 24 KB |
| [`upstream/data/Application/socialapp.json`](<data/upstream/data/Application/socialapp.json>) | 7 | 19 KB |
| [`upstream/data/Finance/bitcoin.json`](<data/upstream/data/Finance/bitcoin.json>) | 8 | 22 KB |
| [`upstream/data/Finance/dh_finance.json`](<data/upstream/data/Finance/dh_finance.json>) | 42 | 114 KB |
| [`upstream/data/Finance/ds_finance.json`](<data/upstream/data/Finance/ds_finance.json>) | 67 | 212 KB |
| [`upstream/data/Finance/moneymanagement.json`](<data/upstream/data/Finance/moneymanagement.json>) | 4 | 12 KB |
| [`upstream/data/Finance/webshop.json`](<data/upstream/data/Finance/webshop.json>) | 5 | 16 KB |

另有 14 个数据文件未逐一列出。

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　569 多轮记录、27 风险场景、5 应用类别、10 风险类型

**任务与判分设置**　对静态轨迹做有无风险判断及原因解释，比较人标结果和解释证据

## 本地文件

- [`metadata/trajectory-labels.jsonl`](metadata/trajectory-labels.jsonl) · 逐条结构化标签，无原始交互 · 571

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
