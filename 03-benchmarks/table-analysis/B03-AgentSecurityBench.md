# B03 Agent Security Bench (ASB) — 数据表格与分析

> 论文：Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents（ICLR 2025）  
> 表格：[analysis/tables](../B03-agent-security-bench/analysis/tables/)

## 1. 数据集结构

`data_agents_summary.csv`：10 个场景智能体，每个 5 个用户任务（academic_search_agent 为 6 个，合计 51；论文 Table 3 写 50）、2 个正常工具、40 个攻击工具（20 激进 + 20 非激进）。

- 攻击工具共 400 个：`data_attack_type_by_aggressive.csv` 显示 Disruptive（破坏型）200 + Stealthy（隐蔽型）200，与激进/非激进各 100 完全正交平衡。
- 若按“用户任务 × 本智能体攻击工具”全组合，共 2,040 个攻击用例（论文实验常以 400 个攻击任务为单位报告百分比，结果粒度为 0.25%，即每格 400 次）。
- PoT 后门任务 16 条，分布在 5 个智能体上。
- 明细表：`data_attack_tools.csv`（400 条攻击指令与目标原文）、`data_normal_tools.csv`、`data_user_tasks.csv`。

论文 Table 3（`paper_T3_statistics.csv`）：10 场景、10 智能体、50 任务、20 正常工具、400 攻击工具/任务、13 种攻击方法（5 DPI + 5 IPI + 记忆投毒 + 混合 + PoT 后门）、11 种防御、7 项指标（ASR、RR、PNA、BP、FNR、FPR、NRP）。

## 2. 攻击主结果：13 个骨干模型 × 5 类攻击

`paper_T5_attack_results_by_backbone.csv`（Table 5）平均行：

| 攻击 | 平均 ASR | 平均拒绝率 |
| --- | --- | --- |
| DPI 直接注入 | 72.68% | 6.53% |
| IPI 间接注入 | 27.55% | 8.61% |
| 记忆投毒 | 7.92% | 4.63% |
| 混合攻击（DPI+IPI+MP） | **84.30%** | 3.22% |
| PoT 后门 | 42.12% | 5.42% |
| 总平均 | 46.91% | 5.68% |

- 混合攻击几乎对所有模型都 >85%（Gemma2-27B 达 100%），只有 LLaMA3-8B（40.75%）和 Mixtral（54.75%）这类能力弱的模型较低。
- GPT-4o 的平均 ASR 64.41%、GPT-4o-mini 67.55% 是最高的两个；GPT-4o 在 PoT 后门下 ASR 100%。
- GPT-4o 在 DPI 下拒绝率 20.05%（全表最高），对应 DPI ASR 仅 60.35%，而 GPT-3.5 Turbo 拒绝率 3% 时 DPI ASR 98.4%——拒绝机制能部分抵消“能力强更易被利用”的趋势（论文称为先升后降关系）。

## 3. 效用—安全综合：NRP

`paper_T6_NRP.csv`（Table 6，NRP = PNA × (1 − ASR)）：

| 模型 | PNA | 平均 ASR | NRP |
| --- | --- | --- | --- |
| Claude-3.5 Sonnet | 100.00 | 56.44 | **43.56** |
| LLaMA3-70B | 66.50 | 54.84 | 30.03 |
| GPT-4o | 79.00 | 64.41 | 28.12 |
| GPT-4o-mini | 50.00 | 67.55 | 16.23 |
| Gemma2-27B | 31.50 | 54.34 | 14.38 |
| … | | | |
| Mixtral-8x7B | 0.00 | 19.01 | 0.00 |
| 平均 | 29.46 | 46.91 | 15.64 |

- 13 个模型中有 7 个 PNA 不足 22%，即多数开源模型在 ASB 场景下连正常任务都做不好；它们的低 ASR 主要是“做不成”而不是“防得住”。NRP 是很适合展示系统的单一综合指标。

## 4. 防御效果

- `paper_T7_defenses_DPI.csv`：DPI 下平均 ASR 无防御 78.38% → Delimiter 79.08%（+0.69）、Paraphrase 56.87%（−21.52）、Instruction 76.77%（−1.62）、动态提示重写 DPR 44.45%（−33.93）。最好的 DPR 仍有 44% 的攻击成功。
- `paper_T8_defenses_IPI.csv`：IPI 下无防御 27.98% → Delimiter 24.96%、Instruction 26.31%、Sandwich 28.04%，基本无效。
- `paper_T19_defense_utility_no_attack.csv`：防御的效用代价——Delimiter 使平均 PNA 从 29.46% 降到 22.52%（−6.94），Sandwich 代价最小（−1.17）。
- `paper_T20_pot_defenses.csv`：对 PoT 后门，Shuffle 反而让平均 ASR 从 42.12% 升到 44.37%，Paraphrase 降到 29.06%。
- `paper_T21_memory_defense_llm_detector.csv`：LLM 检测记忆投毒的平均 FNR 0.660、FPR 0.200，即 66% 的投毒漏检；各模型差异极小（FNR 0.654–0.671）。`paper_F4_ppl_detection_curve_points.csv` 为困惑度检测在不同阈值下的 (FNR, FPR) 点，没有任何阈值能同时把两者压到 0.3 以下。

## 5. 附录细分

- `paper_T14_attack_combinations.csv`：两两组合 DPI+MP 平均 ASR 83.02%，已接近三者混合的 84.30%，IPI+MP 只有 23.75%。
- `paper_T15_pot_triggers.csv`：5 种后门触发词 ASR 99.75–100%，BP 平均 83.05% 与 PNA 79.00% 接近——后门隐蔽且不损效用。
- `paper_T16_pot_utility.csv`：13 个模型植入后门后的 BP vs PNA。
- `paper_T17_prompt_injection_types.csv`：5 种注入写法（Combined/Context Ignoring/Escape/Fake Completion/Naive）平均 ASR 34.75–38.01%，写法差异不大。
- `paper_T18_aggressive_vs_non.csv`：非激进任务 ASR 38.98% 高于激进任务 33.12%，激进任务拒绝率更高（8.31% vs 4.87%）。

## 6. 注意事项

- 论文正文与表格存在小的数字差异：附录 D.1.2 正文称混合攻击 84.03%，表中为 84.30%；Table 7 的“无防御 DPI 平均 ASR”为 78.38%（单独实验），与 Table 5 的 72.68% 不是同一批次。
- 展示时建议：主视图用 13 模型 × 5 攻击的热力图（Table 5），配合 PNA–ASR 散点与 NRP 排名。
