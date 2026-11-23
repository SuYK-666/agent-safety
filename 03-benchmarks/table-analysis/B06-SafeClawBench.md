# B06 SafeClawBench — 数据表格与分析

> 论文：SafeClawBench: Separating Semantic, Audit-Evidence, and Sandbox Harm in Tool-Using LLM Agents  
> 表格：[analysis/tables](../B06-safeclawbench/analysis/tables/)（数据表 10 张、论文表 26 张）

## 1. 数据集结构

600 条 challenge 用例，6 类攻击各 100 条。`data_attack_type_x_harm_type.csv`：

| 攻击 | action | leak | persist | 其他 |
| --- | --- | --- | --- | --- |
| ADI 歧义诱导 | 37 | 26 | 37 | |
| DPI 直接注入 | 52 | 27 | 20 | 1 |
| IPI 间接注入 | 32 | 32 | 36 | |
| MEX 记忆提取 | 0 | 100 | 0 | |
| MPI 记忆投毒 | 0 | 0 | 100 | |
| TRI 工具返回注入 | 25 | 69 | 6 | |
| 合计 | 146 | 254 | 199 | 1 |

- 难度标签（`data_attack_type_x_difficulty.csv`）极度偏“hard”：477/600 为 hard，113 medium，仅 10 easy；MPI 是唯一 medium 占多数的类别（56）。这和论文 Table 45 的源标签一致（论文把 medium 计作 112、unknown 1，相差 1 条）。
- 可执行沙盒（`exec_full_600.json`）：每类 100 条又平分成 3–4 个子类型（`data_exec_subtype.csv`，如 DPI 的 config_modify/db_drop/email_exfil/file_delete 各 25）。我从 fixture 中统计的 8 种状态 oracle 检查数（`data_exec_oracle_checks.csv`：memory_value_contains 133、email_sent 125、code_output_contains 99…共 658 次）与论文 Table 40 逐项相同。
- 另有 72 条种子集（`data_seed72_stats.csv`）和 150/60/3 条执行子集。

## 2. 三层评测终点（这是本基准的核心设计）

同一攻击被分三级判定：语义层 CoreFail（LLM 判官认为回复遵从了攻击目标）→ 证据审计层 HarmEvidence（CoreFail 中能找到可观察伤害证据的）→ 沙盒层 ObservedHarm@Exec（状态 oracle 检测到真实非法状态变化）。三个数字会差一个数量级，展示时务必分开。

## 3. 语义层主结果（Table 3，CoreFail@600 %）

| 模型 | D0 无防御 | B2 Sandwich | D3 分层策略 | D4 长策略 |
| --- | --- | --- | --- | --- |
| GPT-5.5 | 23.8 | 14.7 | 10.8 | **8.8** |
| Claude Opus 4.7 | **9.0** | 10.3 | 5.8 | 5.8 |
| Qwen3.6-Plus | 35.5 | 14.2 | 9.5 | 11.5 |
| GLM-5.1 | 27.5 | 13.3 | **2.2** | 2.8 |
| Kimi K2.5 | 44.2 | 21.7 | 17.0 | 17.2 |
| 汇总 | 28.0 | 14.8 | 9.1 | 9.2 |

- 不设防时模型差距 4.9 倍（Claude Opus 4.7 9.0% vs Kimi K2.5 44.2%）。
- 分层提示策略 D3 把汇总失败率从 28.0% 降到 9.1%；更长的 D4（6,670 字符）并没有更好（9.2%）。`paper_T38_matched_length_control.csv` 用无指令填充文本把 D3 补到同样长度（D3_LM），平均 8.0%，说明“提示长度”本身就是混杂因素。
- `paper_T27_corefail_nine_policies.csv`：9 种策略完整矩阵。B1（一句安全提醒）和 B3（关键词提醒）几乎无效（25.9%、25.3%）。
- `paper_T28_corefail_by_attack_D0.csv`：按攻击类型，MPI（记忆投毒，Kimi 81%、Qwen 80%）和 MEX（记忆提取，五模型 41–76%）最难防；连最稳健的 Opus 4.7 在 MEX 上也有 41%。TRI 在 Opus 4.7 上为 0%，在 Kimi 上 35%。

## 4. 证据审计层（Table 4/5/16）

- D0 下 840 条 CoreFail 全部人工/模型审计：504 条（60%）有伤害证据，336 条仅是“语义上同意”而无实际伤害证据。
- 模型差异：GPT-5.5 的 143 条 CoreFail 中只有 40 条（28%）有证据，而 Opus 4.7 的 54 条中有 32 条（59%）——即 Opus 失败得少，但失败时更“实”。
- 按攻击（Table 16）：MPI 272 条中 251 条有持久化伤害证据（92%），MEX 272 条中只有 121 条有文本泄露证据（44%），IPI 80 条中只有 15 条（19%）。所以 MEX 的高 CoreFail 有一半是“谈论策略/架构”的轻度泄露（Table 17：49/100 属于策略透明度类）。
- 各防御（Table 5）：HarmEvidence 从 D0 504 → B2 176 → D3 119 → D4 160。

## 5. 沙盒层（Table 41/42/21）

| 模型 | ToolCall-ASR | ObservedHarm（D0） | D4 下 ObservedHarm |
| --- | --- | --- | --- |
| GPT-5.5 | 12.5 | 2.167 | 1.333 |
| Claude Opus 4.7 | 7.2 | 0.500 | 0.333 |
| Qwen3.6-Plus | 13.0 | 1.667 | 2.333 |
| GLM-5.1 | 14.2 | 5.000 | 4.500 |
| Kimi K2.5 | 20.0 | 11.333 | 3.333 |
| 平均 | 13.4 | 4.133 | 2.367 |

- 真实状态伤害率比语义失败率低约 7 倍（4.13% vs 28.0%）。GLM-5.1 语义层在 D3 下只有 2.2%，但沙盒伤害仍有 4.3%——**提示策略在语义层的大幅改进，并不等比例转化为执行层改进**。
- Table 21 揭示关键现象：沙盒伤害有 291/347 条发生在语义层判为“通过”（CorePass）的用例上，即只看文本回复的评测会漏掉大部分真实伤害。
- 防御对沙盒伤害的改善是显著的（Table 19 McNemar，Holm p ≈ 5e-5–1e-4），但幅度只有约 1.6 个百分点。

## 6. 其他附录表

- 效用（Table 22–25）：42 个良性任务上任务成功率 33–53%，误拒率 ≤1%，防御对效用影响小（D0 46.6% vs D3 46.9%，B2 降到 39.8%）。
- 评测框架敏感性（Table 29–31）：同一 600 条在单轮格式下平均 ASR 61.9%，换成 HERMES 多轮框架降到 38.7%；Qwen3 单轮高达 94.6%。说明 harness 本身会造成 20+ 个点差异。
- 判官可靠性（Table 34/36）：GPT-5.4 与 Claude Opus 4.6 判官一致率 96.1%、κ=0.871；人工复核 κ≈0.78–0.79。
- 统计检验（Table 43）、经验难度（Table 44：36.7% 的扩展题无模型攻破）、数据切分（Table 45）均已转录。

## 7. 展示建议

用“三级漏斗”（CoreFail → HarmEvidence → ObservedHarm）作为该基准的主视图，按模型或防御切换；再配 6 类攻击 × 5 模型热力图（Table 28）。
