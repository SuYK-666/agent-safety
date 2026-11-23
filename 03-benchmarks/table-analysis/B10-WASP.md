# B10 WASP — 数据表格与分析

> 论文：WASP: Benchmarking Web Agent Security Against Prompt Injection Attacks（Meta FAIR）  
> 表格：[analysis/tables](../B10-wasp/analysis/tables/)

## 1. 数据集结构

`data_overview.csv`：21 个攻击目标（GitLab 12、Reddit 9）× 每环境 2 个用户目标 = 42 个场景，再 × 2 种注入模板（URL / 纯文本）= **84 个任务**，论文所有比率都以 84 为分母。另有 37 个效用任务（GitLab 25、Reddit 12）。

- 判定方式（`data_attack_env_x_evaltype.csv`）：16 个目标用页面状态检查（program_html），5 个用外泄 URL 检查（exfil）。
- 攻击者能力被刻意限制：只能发帖/评论/开 issue，不能改页面布局或弹窗——这比 InjecAgent、AgentDojo 的威胁模型更现实。
- 安全违规类别（`paper_T5_attacker_goals_violation.csv`）：Gaining Access 7 个（含添加 SSH key、加攻击者为 Owner）、Exfiltration 2、Data Destruction 2、Harassment 3、Snooping 2，以及 Phishing、Misinformation、Impair Defenses、Execution、Access Removal 各 1。

## 2. 主结果（Table 2）

| 模型 | 输入 | 防御 | ASR 中间 | ASR 端到端 | 效用 |
| --- | --- | --- | --- | --- | --- |
| GPT-4o-mini | axtree | – | 0.345 | 0.024 | 0.432 |
| GPT-4o | axtree+SOM | – | 0.429 | 0.036 | **0.622** |
| GPT-4o | axtree | 系统提示 | 0.167 | 0.000 | 0.459 |
| OpenAI o1 | axtree | 指令层级（system） | **0.857** | **0.167** | 0.486 |
| Claude 3.5 Sonnet v2 | 截图 | – | 0.583 | 0.060 | 0.081 |
| Claude 3.7 Sonnet 思考 | 截图 | – | 0.536 | 0.036 | 0.486 |

完整 13 种配置见 `paper_T2_main_results.csv`。

- 两级 ASR 的差异是 WASP 的核心发现：智能体在 17–86% 的任务中会“上钩”（开始执行攻击者指令），但最终真正完成攻击目标的只有 0–17%——作者称之为“security by incompetence”，攻击没完成往往是因为智能体能力不足而非识破了攻击。
- OpenAI o1 是最容易被劫持且最“能干”的：中间 ASR 85.7%、端到端 16.7%。
- 防御性系统提示能降低中间 ASR（GPT-4o 0.321 → 0.167），但同时降低效用（0.595 → 0.459）。Claude 3.5 v2 的效用只有 8%，几乎不可用。

## 3. 注入方式消融

- `paper_T3_url_vs_plaintext.csv`：URL 型注入（把恶意指令藏在链接里）远比纯文本有效，o1 中间 ASR 达 97.6%，Claude 3.5 85.7%。但 Claude 在纯文本下端到端 ASR 反而更高（0.071），作者认为截图模式下看不到 URL 中隐藏的完整指令。
- `paper_T4_task_related_vs_agnostic.csv`：攻击者不知道用户目标时（通用注入），ASR 下降但不为零，Claude 3.7 中间 ASR 从 50% 降到 32%。

## 4. 展示建议

用“中间 ASR → 端到端 ASR”的双柱或漏斗展示每个配置，旁边配效用；强调“低端到端 ASR 不等于安全”。
