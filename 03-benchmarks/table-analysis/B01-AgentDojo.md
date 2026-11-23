# B01 AgentDojo — 数据表格与分析

> 论文：AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents（NeurIPS 2024 D&B）  
> 表格目录：[analysis/tables](../B01-agentdojo/analysis/tables/)  
> 文件命名：`data_*.csv` 由上游数据集计算得出；`paper_*.csv` 由论文原文逐格转录，表号与页码在下文各节注明。

## 1. 数据集结构（由上游任务定义统计）

表 `data_suite_summary_v1.csv`（v1 基线版本）：

| 套件 | 用户任务 | 注入任务 | 安全用例（用户×注入） | 注入点向量 | 难度 EASY/MEDIUM/HARD* |
| --- | --- | --- | --- | --- | --- |
| workspace | 40 | 6 | 240 | 16 | 11/16/6 |
| slack | 21 | 5 | 105 | 6 | 3/8/6 |
| travel | 20 | 7 | 140 | 13 | 2/4/1 |
| banking | 16 | 9 | 144 | 4 | 0/0/0 |
| **合计** | **97** | **27** | **629** | **39** | 16/28/13 |

\* 难度只对用类定义的任务标注；workspace 有 7 个、slack 有 4 个由 `TaskCombinator` 拼接的组合任务不带难度，banking 未标难度。

要点：

- 从代码计算出的 97 个用户任务、27 个注入任务、629 个安全用例，与论文 Table 1 和正文的 97/27/629 完全一致，说明 629 就是四个套件“用户任务数 × 注入任务数”之和。
- workspace 占安全用例的 38%（240/629），是最大的套件；banking 注入任务最多（9 个），但用户任务最少。
- `data_task_files_by_version.csv` 列出 v1→v1.2.2 每个版本对哪些任务做了覆盖修订（例如 v1.2 重写了 workspace 9 个注入任务、banking 8 个注入任务）。做展示时如果用最新版本跑分，配对数仍是 629，但个别任务的判定逻辑已变化，不宜与论文分数直接横比。
- `data_injection_goals_v1.csv` 列出全部 27 个攻击目标原文（转账、外发安全码、发钓鱼链接、订最贵酒店等），`data_user_task_prompts.csv` 列出 86 个类定义的用户任务原文。

论文 Table 1（`paper_T1_environments.csv`）给出工具数：workspace 24、slack 11、travel 28、banking 11。注意论文称总计 70 个工具，但四项相加为 74，这是论文自身的口径差异，转录时原样保留并加了备注。

## 2. 论文主结果：10 个模型（“Important message” 攻击）

表 `paper_T3_agents_important_message_attack.csv`（附录 Table 3，括号为 95% CI）：

| 模型 | 无攻击效用 | 受攻击效用 | 定向 ASR |
| --- | --- | --- | --- |
| Claude 3.5 Sonnet | 78.22 | 51.19 | 33.86 |
| GPT-4o | 69.00 | 50.08 | **47.69** |
| Claude 3 Opus | 66.61 | 52.46 | 11.29 |
| GPT-4 Turbo | 63.43 | 54.05 | 28.62 |
| Claude 3 Sonnet | 53.10 | 33.23 | 26.71 |
| Gemini 1.5 Pro | 45.63 | 28.93 | 25.60 |
| Gemini 1.5 Flash | 36.09 | 34.18 | 12.24 |
| Llama 3 70b | 34.50 | 18.28 | 20.03 |
| GPT-3.5 Turbo | 33.86 | 34.66 | 8.43 |
| Command-R+ | 25.44 | 25.12 | 0.95 |

分析：

- “能力越强越容易被定向攻击”的反向缩放：GPT-4o 效用第二高，ASR 最高（47.69%）；Command-R+ 效用最低，ASR 几乎为 0。原因是弱模型连攻击者的任务都完成不了，低 ASR 不等于“安全”。展示时建议把效用和 ASR 画在同一张散点图上，而不是单独排名 ASR。
- Claude 3 Opus 是明显的离群点：效用 66.61% 却只有 11.29% ASR，在效用—安全帕累托前沿上。
- 受攻击后效用普遍下降 10–25 个百分点（Claude 3.5 Sonnet 下降最多，−27.0）；GPT-3.5 Turbo 和 Command-R+ 几乎不降，同样因为它们基础效用低。
- CI 半宽约 ±2–4 个百分点，相差 5 个点以内的模型不宜断言优劣。

## 3. 攻击方式消融（GPT-4o）

`paper_T4_attack_prompts_gpt4o.csv`：TODO 3.66%、Ignore previous 5.41%、InjecAgent 5.72%、Important message 57.7%、自适应 Max 57.55%（定向）；非定向 ASR 分别为 32.75/33.23/31.48/49.9/68.36%。

- 措辞差异带来一个数量级的差别：“Important message”比经典 “Ignore previous instructions” 高 10 倍以上。展示系统应强调“测评结论依赖攻击模板”。
- 注意 Table 4 的 Important message 定向 ASR 为 57.7%，而 Table 3 的 GPT-4o 为 47.69%、Table 2 基线为 45.8%，三处数字来自不同实验批次/提示变体，不要混用。

`paper_T2_attacker_knowledge_gpt4o.csv`：知道用户名和模型名只把 ASR 从 45.8% 提到 47.7%（+1.9），但猜错名字会砍掉约一半（猜错用户 23.2%，猜错模型 23.7%）。

## 4. 防御对比（GPT-4o）

`paper_T5_defenses_gpt4o.csv`：

| 防御 | 无攻击效用 | 受攻击效用 | 定向 ASR |
| --- | --- | --- | --- |
| 无防御 | 69.0 | 50.01 | 57.69 |
| Delimiting（分隔符） | 72.66 | 55.64 | 41.65 |
| PI detector（BERT 检测器） | 41.49 | 21.14 | 7.95 |
| Repeat prompt（三明治） | 85.53 | 67.25 | 27.82 |
| Tool filter（工具过滤） | 73.13 | 56.28 | **6.84** |

- Tool filter 同时提高效用并把 ASR 降到 6.84%，是性价比最高的防御；但论文指出 17% 的测试用例中用户任务所需工具本身就足以完成攻击，这部分无法用工具过滤防住。
- PI detector 的 ASR 也很低（7.95%），代价是效用掉了 27.5 个点（误报过多）。
- Repeat prompt 的效用最高（85.53%），但论文提醒它对自适应攻击很可能不鲁棒。
- 正文写 Tool filter ASR 为 7.5%，附录表为 6.84%，以附录表为准（已在 `paper_text_key_numbers.csv` 记录差异）。

## 5. 其他关键数字

`paper_text_key_numbers.csv`：Slack 套件 ASR 92%（攻击者控制的工具输出占比高）；travel 注入任务 6 的 ASR 为 0%（需要完成两个无关恶意动作）；注入放在工具输出末尾时 ASR 可达约 70%；在 GPT-4o 上跑完整 629 个安全用例约 35 美元，97 个效用用例约 4 美元。

## 6. 展示建议

- 主视图：效用 vs 定向 ASR 散点（10 个模型）+ 防御前后对比柱图。
- 数据集视图：四个套件的用户任务、注入任务、安全用例堆叠柱。
- 论文的 Figure 7（按注入任务的 ASR）、Figure 20/21 只有图没有数值表，未转录。
