# B05　AgentDyn

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　60 条用户任务（日常/开发协作/购物各 20）、28 条注入任务、100 个工具、7 个环境数据库

原三个 *-normal-tasks.json 为静态提取视图，保留。

**论文**　[AgentDyn - Are Your Agent Security Defenses Deployable in Real-World Dynamic Environments](<paper/AgentDyn - Are Your Agent Security Defenses Deployable in Real-World Dynamic Environments.pdf>) · 完整原件 26 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2602.03117) · [发布页 1](https://arxiv.org/abs/2602.03117)

**上游入口**　[项目或数据 1](https://github.com/SaFo-Lab/AgentDyn)


## 测试集

**来源**　[HF agentdyn-dataset/agentdyn](https://huggingface.co/datasets/agentdyn-dataset/agentdyn)

**位置**　[`data/upstream/`](data/upstream/) · 11 个文件 · 271 KB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/env_bank_database/train-00000-of-00001.parquet`](<data/upstream/env_bank_database/train-00000-of-00001.parquet>) | 3 | 12 KB |
| [`upstream/env_calendar/train-00000-of-00001.parquet`](<data/upstream/env_calendar/train-00000-of-00001.parquet>) | 3 | 15 KB |
| [`upstream/env_email_database/train-00000-of-00001.parquet`](<data/upstream/env_email_database/train-00000-of-00001.parquet>) | 3 | 71 KB |
| [`upstream/env_filesystem/train-00000-of-00001.parquet`](<data/upstream/env_filesystem/train-00000-of-00001.parquet>) | 3 | 4 KB |
| [`upstream/env_github_platform/train-00000-of-00001.parquet`](<data/upstream/env_github_platform/train-00000-of-00001.parquet>) | 2 | 3 KB |
| [`upstream/env_shopping_platform/train-00000-of-00001.parquet`](<data/upstream/env_shopping_platform/train-00000-of-00001.parquet>) | 2 | 62 KB |
| [`upstream/env_web_database/train-00000-of-00001.parquet`](<data/upstream/env_web_database/train-00000-of-00001.parquet>) | 3 | 62 KB |
| [`upstream/injection_tasks/train-00000-of-00001.parquet`](<data/upstream/injection_tasks/train-00000-of-00001.parquet>) | 28 | 3 KB |
| [`upstream/user_tasks/train-00000-of-00001.parquet`](<data/upstream/user_tasks/train-00000-of-00001.parquet>) | 60 | 6 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　60 开放任务、560 注入用例

**任务与判分设置**　购物、开发协作和日常场景需要利用合法外部信息动态重规划；分别观察任务效用和边界偏移

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/dailylife-normal-tasks.json`](data/dailylife-normal-tasks.json) · 正常任务，静态提取 · 20
- [`data/github-normal-tasks.json`](data/github-normal-tasks.json) · 正常任务，静态提取 · 20
- [`data/shopping-normal-tasks.json`](data/shopping-normal-tasks.json) · 正常任务，静态提取 · 20

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
