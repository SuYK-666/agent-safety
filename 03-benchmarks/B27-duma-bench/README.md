# B27　DUMA-Bench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　8 个域 35 条任务、各域数据库、策略与用户提示

测试集原文件存于 `data/upstream/`，与上游目录结构一致。

**论文**　[DUMA-Bench - A Dual-Control Multi-Agent Benchmark for Evaluating LLM Agent Security](<paper/DUMA-Bench - A Dual-Control Multi-Agent Benchmark for Evaluating LLM Agent Security.pdf>) · 完整原件 14 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2609.24662) · [发布页 1](https://arxiv.org/abs/2609.24662) · [发布页 2](https://thelatestinai.com/papers/2609.24662)


## 测试集

**来源**　[GitHub ai-security-lab-itmo/duma-benchmark](https://github.com/ai-security-lab-itmo/duma-benchmark)

**位置**　[`data/upstream/`](data/upstream/) · 31 个文件 · 142 KB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/duma/domains/auth_spoof_support/db.json`](<data/upstream/data/duma/domains/auth_spoof_support/db.json>) | — | 1 KB |
| [`upstream/data/duma/domains/auth_spoof_support/tasks.json`](<data/upstream/data/duma/domains/auth_spoof_support/tasks.json>) | 3 | 10 KB |
| [`upstream/data/duma/domains/collab/db.json`](<data/upstream/data/duma/domains/collab/db.json>) | — | 1 KB |
| [`upstream/data/duma/domains/collab/tasks.json`](<data/upstream/data/duma/domains/collab/tasks.json>) | 6 | 17 KB |
| [`upstream/data/duma/domains/crm_leak/db.json`](<data/upstream/data/duma/domains/crm_leak/db.json>) | — | 1 KB |
| [`upstream/data/duma/domains/crm_leak/tasks.json`](<data/upstream/data/duma/domains/crm_leak/tasks.json>) | 4 | 15 KB |
| [`upstream/data/duma/domains/infra_loadshed/db.json`](<data/upstream/data/duma/domains/infra_loadshed/db.json>) | — | 1 KB |
| [`upstream/data/duma/domains/infra_loadshed/tasks.json`](<data/upstream/data/duma/domains/infra_loadshed/tasks.json>) | 6 | 14 KB |
| [`upstream/data/duma/domains/mail_rag_phishing/db.json`](<data/upstream/data/duma/domains/mail_rag_phishing/db.json>) | — | 12 KB |
| [`upstream/data/duma/domains/mail_rag_phishing/tasks.json`](<data/upstream/data/duma/domains/mail_rag_phishing/tasks.json>) | 7 | 15 KB |
| [`upstream/data/duma/domains/mktg_phishing/db.json`](<data/upstream/data/duma/domains/mktg_phishing/db.json>) | — | 1 KB |
| [`upstream/data/duma/domains/mktg_phishing/tasks.json`](<data/upstream/data/duma/domains/mktg_phishing/tasks.json>) | 3 | 9 KB |
| [`upstream/data/duma/domains/output_handling/db.json`](<data/upstream/data/duma/domains/output_handling/db.json>) | — | 1 KB |
| [`upstream/data/duma/domains/output_handling/tasks.json`](<data/upstream/data/duma/domains/output_handling/tasks.json>) | 3 | 7 KB |

另有 2 个数据文件未逐一列出。

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　35 个可执行任务，8 个领域／风险类别；9 项另含通信断言

**任务与判分设置**　扩展双控制环境，对比被动、协作或其他用户行为条件；以环境断言和必要的通信证据判分

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
