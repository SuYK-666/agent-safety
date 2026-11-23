# B05 AgentDyn — 数据表格与分析

> 论文：AgentDyn: Are Your Agent Security Defenses Deployable in Real-World Dynamic Environments?  
> 表格：[analysis/tables](../B05-agentdyn/analysis/tables/)

## 1. 数据集结构

`data_suite_summary.csv`（由 HF parquet 统计）：

| 套件 | 用户任务 | 注入任务 | 安全用例 | 工具 | 平均用户指令长度 |
| --- | --- | --- | --- | --- | --- |
| Shopping | 20 | 9 | 180 | 39 | 126 字符 |
| GitHub | 20 | 9 | 180 | 34 | 122 字符 |
| Dailylife | 20 | 10 | 200 | 27 | 214 字符 |
| 合计 | 60 | 28 | **560** | 100 | |

与论文 Table 2 完全一致。7 个环境（银行、日历、邮件、文件系统、GitHub、购物、网页）在 `data_environments.csv`；`data_injection_goals.csv` 列出 28 个注入目标。公开任务文件中没有难度标注（difficulty 全为空）。

论文 Table 1（`paper_T1_benchmark_complexity.csv`）对比了每个用户任务的平均可见工具数/轨迹长度/涉及应用数：InjecAgent 2/1/1、ASB 3/1/1、AgentDojo 19.87/3.49/1.38、AgentDyn **33.33/7.10/3.17**。AgentDyn 的核心卖点是任务更长、更动态，并且执行路径中嵌有“有益的环境指令”（如去邮箱取 OTP），这正是很多防御会误杀的地方。

## 2. 完整结果矩阵：12 模型 × 11 种配置

附录 Table 9–17 已全部转录，分为三张长表（每张含 Overall/Shopping/GitHub/Dailylife 四列）：`paper_T9_T11_benign_utility.csv`、`paper_T12_T14_utility_under_attack.csv`、`paper_T15_T17_asr.csv` + `paper_T17_asr_system.csv`。合并后的 Overall 视图为 `derived_full_matrix_overall.csv`（122 行）。

按防御取 12 个模型均值（`derived_defense_means.csv`，我计算的）：

| 防御 | 类型 | 无攻击效用 | 受攻击效用 | ASR |
| --- | --- | --- | --- | --- |
| 无防御 | – | 46.95 | 41.69 | 18.75 |
| Prompt Sandwiching | 提示 | 44.58 | 41.58 | 14.93 |
| Spotlighting | 提示 | 41.67 | 40.04 | 14.94 |
| ProtectAI | 过滤 | **1.25** | 0.76 | 0.54 |
| PIGuard | 过滤 | 10.14 | 2.47 | 1.25 |
| PromptGuard2 | 过滤 | 43.05 | 20.28 | 13.09 |
| Meta-SecAlign（8B/70B 两个模型） | 对齐 | 30.00 | 30.29 | 7.12 |
| Tool Filter | 系统 | 2.50 | 2.16 | 1.36 |
| CaMeL | 系统 | **0.00** | 0.00 | 0.00 |
| Progent | 系统 | 13.33 | 10.38 | 3.56 |
| DRIFT | 系统 | 22.08 | 21.74 | 2.25 |

分析：

- 这是本基准最重要的结论：**在 AgentDojo 上表现很好的防御，在动态任务里几乎都靠“让智能体什么都做不成”来换取低 ASR**。CaMeL 效用为 0，ProtectAI 1.25%，Tool Filter 2.5%。原因是这些防御要么事先规划工具/数据流（无法适应运行中才出现的步骤），要么把执行路径上“有益的环境指令”当作注入拦截掉。
- 提示类防御几乎不损效用，但 ASR 只降 4 个点左右。
- DRIFT 是系统级防御里折中最好的（效用 22%，ASR 2.25%），但效用也只有无防御的一半。PromptGuard2 无攻击效用接近不设防，但受攻击时效用减半（检测到注入就终止）。
- 不设防时，新一代模型自身已经很稳健：GPT-5-mini ASR 0.37%、Claude-Sonnet-4.5 0.87%、GPT-5.1 4.96%，同时效用最高（65–72%）；GPT-4o-mini 50.0%、GPT-4o 37.8%、Gemini-2.5 Flash 37.61% 最脆弱。
- 分套件看，Dailylife 的 ASR 普遍最高（如 GPT-4o mini 80%、Gemini-2.5 Flash 74.5%），Shopping 最低。

## 3. 主文 Table 3 与附加攻击

- `paper_T3_main_defenses.csv`：正文中 4 个代表模型（GPT-4o、Gemini-2.5 Pro、Claude-Sonnet-3.5、Llama 3.3 70B）× 10 种防御的效用/ASR，数值与附录对应行一致。
- `paper_T8_other_attacks.csv`：对 GPT-5-mini、GPT-5.1、Claude-Sonnet-4.5 换用 Ignore、Completion 与人工自适应攻击，ASR 仍只有 0–5.6%。论文坦言“攻击发展落后于防御”，所以 AgentDyn 的主要价值是检验防御的效用代价，而非攻击强度。

## 4. 展示建议

用“防御 × 模型”双热力图（效用、ASR 各一）展示 `derived_full_matrix_overall.csv`；再用效用–ASR 散点按防御着色，直观看到“低 ASR 簇几乎全贴在效用 0 附近”。
