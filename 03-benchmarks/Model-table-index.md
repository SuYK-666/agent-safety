# Benchmark 模型 × 数据表索引

> 数据范围：`C:\Users\18201\Desktop\agent-safety\03-benchmarks`，39 个有数据表的 benchmark（B01–B40，B15 无数据表），共 516 张 `analysis/tables/*.csv`。  
> 本文只索引**有明确模型结果的表**：模型作为行/列出现，或整张表只测一个具名模型。纯数据构成、攻击类型、判官一致性、成本汇总等没有具名模型结果的表不在此重复。  
> 同一个模型可能出现在多个 benchmark；同一 benchmark 的不同表也可能使用不同模型面板。本文保留原始论文拼写，并在系列内给出常见别名。  
> 读法示例：`B17 paper_T2/T3/T4/T5` 表示该模型出现在 `B17-authgatebench/analysis/tables/paper_T2_*.csv` 至 `paper_T5_*.csv` 这四张结果表中。

## 术语约定

- **B03 全部 9 张模型表**：`paper_T5_attack_results_by_backbone.csv`、`paper_T6_NRP.csv`、`paper_T7_defenses_DPI.csv`、`paper_T8_defenses_IPI.csv`、`paper_T14_attack_combinations.csv`、`paper_T16_pot_utility.csv`、`paper_T19_defense_utility_no_attack.csv`、`paper_T20_pot_defenses.csv`、`paper_T21_memory_defense_llm_detector.csv`。这 9 张表都使用同一组 13 个 LLM。
- **B05 全模型面板**：`paper_T9_T11_benign_utility.csv`、`paper_T12_T14_utility_under_attack.csv`、`paper_T15_T17_asr.csv`、`paper_T17_asr_system.csv`、`derived_full_matrix_overall.csv`。前四张中除 `paper_T17_asr_system` 的 12 模型子集外，主体均为 14 模型。
- **B02 T6/T8 30 模型面板**：包含原始 30 个模型；T8 额外含 GPT-3.5/GPT-4 微调版的分组结果，但主面板仍按 30 个基础模型读取。
- **B06 5 模型核心面板**：`paper_T3/T4/T27/T28/T38/T41/T42`；**B06 8 模型面板**：`paper_T22_T24/T29/T31/T32/T43`，其中 T31 仅 5 个模型、T32 仅 3 个模型。
- **B40 v1.0 / v1.1**：分别指 `data_v1_0_by_model.csv` + `data_v1_0_success_by_model_x_length.csv`，以及 `data_v1_1_by_model.csv` + `data_v1_1_success_by_model_x_length.csv`；`(Inspect)` 是运行标签。

## 0. 先看结论

- 覆盖模型最多的面板：B02 InjecAgent（30 个）、B37 BFCL v4（69 个模型配置）、B40 METR（v1.0 34 个、v1.1 21 个含 human）。
- 最常见的跨基准模型：GPT-4o、Claude 3.5 Sonnet、GPT-4、Llama 3.x、Qwen2.5/3.x、Mistral/Mixtral、Gemini 1.5/2.5。
- 2026 年新模型主要集中在 B06、B16、B17、B21、B27、B35、B40：GPT-5.x、Claude 4.x/5、Gemini 3.x、Qwen3.5/3.6/3.7、GLM-5.x、Kimi K2.x、DeepSeek V3.2/V4。
- B12、B30 的“模型”是智能体脚手架/攻击智能体，不是 LLM 型号，集中放在最后的“智能体与基线”一节。
- B23 MCPSecBench、B25 HCP、B36 SOCBench 没有具名 LLM 结果面板，故不进入型号清单。

## 1. 基准 → 有模型结果的数据表

| 基准 | 有模型结果的数据表 | 模型面板规模 |
| --- | --- | --- |
| B01 AgentDojo | `paper_T3_agents_important_message_attack.csv`；`paper_T2/T4/T5` 仅 GPT-4o | T3 10 个；T2/T4/T5 单模型 |
| B02 InjecAgent | `paper_T3`、`paper_T6`–`paper_T12` | 10–30 个 |
| B03 ASB | `paper_T5`–`T8`、`T14`、`T16`、`T19`–`T21` | 13 个 |
| B04 ART | `paper_F3`、`paper_F5_transfer_matrix`、`paper_F5_transfer_long`、`derived_F5_transfer_summary` | F3 18 个；迁移 14 个 |
| B05 AgentDyn | `paper_T3`、`paper_T8`、`paper_T9_T11`、`paper_T12_T14`、`paper_T15_T17`、`paper_T17_asr_system`、`derived_full_matrix_overall` | 3–14 个 |
| B06 SafeClawBench | `paper_T3/T4/T27/T28/T38/T41/T42`、`paper_T22_T24`、`paper_T29/T31/T32/T43` | 5 或 8 个 |
| B07 AgentHarm | `paper_T2/T3/T8/T9/T10`、`derived_T9_pivot_by_model` | 3–15 个 |
| B08 Agent-SafetyBench | `paper_T5`、`paper_T6` | 16 个 |
| B09 ToolEmu | `paper_T4_agent_evaluation.csv` | 5 个 |
| B10 WASP | `paper_T2`、`paper_T3`、`paper_T4` | 2–5 个 |
| B11 SafeArena | `paper_F3`、`paper_F5`、`paper_T3/T5/T11/T12`；`paper_T4` 2 个 | 2–5 个 |
| B12 ST-WebAgentBench | `paper_F2_agent_metrics.csv` | 3 个智能体框架 |
| B13 OS-Harm | `paper_T2`、`paper_F5`；`paper_T6` 3 个 | 3–5 个 |
| B14 MMA-SafetyBench | `paper_T2/T3/T4/T5/T6`、`derived_model_means` | 9 个 |
| B16 AuthorizationBench | `paper_T11`、`paper_T12` | 4 个 |
| B17 AuthGateBench | `paper_T2`–`T5`、`derived_policy_means` | 4 个 |
| B18 PrivacyLens | `paper_T2`、`paper_T3`、`paper_T5` | 9 个 |
| B19 CI-Work | `paper_T1`；`paper_T2` 仅 GPT-5 | 9 个 + 单模型 |
| B20 AgentLeak | `paper_F7`、`paper_T15`、`paper_T16`、`results_model_stats` | 5 个 |
| B21 MemSecBench | `paper_T2`、`derived_pooled_by_llm` | 3 个 LLM × 2 框架 × 4 后端 |
| B22 ATBench | `paper_T2_main_results.csv` | 17 个 |
| B24 MSB | `paper_T3`、`paper_T4`、`paper_T11`、`paper_T12` | 10 个 |
| B26 MADBench | `paper_T4b_M5_model.csv` | 3 个 |
| B27 DUMA-Bench | `paper_T4_model_asr.csv` | 14 个 |
| B28 R-Judge | `paper_T1/T2/T3/T7/T8` | 4–12 个 |
| B29 Cybench | `paper_T2`、`paper_T3`、`paper_T9`–`T12` | 2–8 个 |
| B30 CVE-Bench | `paper_F3`、`paper_F4` | 3 个攻击智能体（T-Agent 由 GPT-4o 驱动） |
| B31 CyberSecEval 2 | `paper_F1`–`F6`、`derived_figure_row_means` | 7–11 个 |
| B32 CyberSecEval 3 | `paper_F3/F4/F7/F9/F11`–`F15`、`paper_T5` | 4–7 个（另有护栏组合） |
| B33 SEC-bench | `paper_T4_agents_models.csv` | 3 个 LLM × 3 个脚手架 |
| B34 CyberSOCEval | `paper_F8/F9/F10/F12/F13/F14` | 6–7 个 |
| B35 Cyber Defense Benchmark | `paper_T5_leaderboard`、`data_reference_cost` | 11 个 |
| B37 BFCL v4 | `paper_T1`；`paper_T2`、`paper_T3` | T1 69 个配置；T2/T3 7 个 |
| B38 τ²-Bench | `paper_F3`、`paper_F4` | 4 个 / 2 个 |
| B39 OSWorld | `paper_T5`、`paper_T14` | 12 个 + human |
| B40 METR | `data_v1_0_*`、`data_v1_1_*`、`paper_T6/T7/T9`、`results_logistic_fits`、`results_model_horizon_summary` | v1.0 34 个、v1.1 21 个（含 human） |

## 2. OpenAI

### GPT-3.5 / ChatGPT-3.5

- **GPT-3.5 Turbo**：B01 `paper_T3`；B02 `paper_T3/T6/T8/T9/T10/T11/T12`；B03 `paper_T5–T8/T14/T16/T19–T21`；B07 `paper_T9/T10`、`derived_T9_pivot_by_model`；B31 `paper_F1–F6`、`derived_figure_row_means`；B40 v1.0（`gpt-3.5-turbo-instruct`）。
- **GPT-3.5 Turbo（Fine-tuned）**：B02 `paper_T6/T8`（论文同时报告原始与微调版）。
- **ChatGPT / ChatGPT-3.5 标签**：B09 `paper_T4`；B18 `paper_T2/T3/T5`；B28 `paper_T1/T2/T7/T8`。这些论文使用 ChatGPT-3.5 名称，未细分 Turbo 快照，故单列。

### GPT-4 系列

- **GPT-4**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`；B09 `paper_T4`；B18 `paper_T2/T3/T5`；B31 `paper_F1/F2/F3/F4/F6`、`derived_figure_row_means`（无 F5）；B39 `paper_T5/T14`。
- **GPT-4（Fine-tuned）**：B02 `paper_T6/T8`。
- **GPT-4 Turbo**：B01 `paper_T3`；B08 `paper_T5/T6`；B31 `paper_F5`、`derived_figure_row_means`；B32 `paper_F3/F4/F7/F9/F11–F15`、`paper_T5`；B40 v1.0 与 v1.1（Inspect）。
- **GPT-4 0314**：B40 v1.0；v1.1 的 `data_v1_1_by_model`、`paper_T6`；`results_logistic_fits`。
- **GPT-4 0125**：B40 v1.0；`paper_T6`。
- **GPT-4 1106**：B40 v1.0 与 v1.1（Inspect）；`paper_T6/T7/T9`；`results_logistic_fits`。
- **GPT-4.5**：B04 `paper_F3`、`paper_F5_transfer_matrix`、`paper_F5_transfer_long`、`derived_F5_transfer_summary`。

### GPT-4o 系列

- **GPT-4o**：B01 `paper_T2/T3/T4/T5`（T2/T4/T5 专测 GPT-4o）；B03 `paper_T5–T8/T14/T16/T19–T21`；B05 `paper_T3/T9_T11/T12_T14/T15_T17/T17_asr_system`、`derived_full_matrix_overall`；B06 `paper_T22_T24/T29/T31/T32/T43`；B07 `paper_T2/T3/T8/T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`；B10 `paper_T2/T3/T4`；B11 `paper_F3/F5/T3/T5/T11/T12`；B13 `paper_T2/F5`；B19 `paper_T1`；B20 `paper_F7/T15/T16`、`results_model_stats`；B26 `paper_T4b`；B27 `paper_T4`；B28 `paper_T1/T2/T7/T8`；B29 `paper_T2/T3/T9–T12`；B33 `paper_T4`；B34 `paper_F8/F9/F10/F12/F13/F14`；B37 `paper_T1`（`gpt-4o-2024-11-20` Prompt/FC）；B39 `paper_T5/T14`；B40 v1.0 与 v1.1（Inspect）。
- **GPT-4o（axtree+SOM / axtree 观察模式）**：B10 `paper_T3/T4`。这是同一 GPT-4o 的输入表示变体，不是新模型。
- **GPT-4o mini**：B03 全部 9 张模型表；B06 `paper_T22_T24/T29/T31/T32/T43`；B07 `paper_T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`；B10 `paper_T2/T3`；B11 `paper_F3/F5/T3/T5/T11/T12`；B20 `paper_F7/T15/T16`、`results_model_stats`；B24 `paper_T3/T4/T11/T12`；B27 `paper_T4`；B37 `paper_T1`（`GPT-4o-mini-2024-07-18` Prompt/FC）。
- **GPT-4o-Mini 大写写法**：B11 表中的 `GPT-4o-Mini` 与上条同一型号。

### GPT-5 系列

- **GPT-5**：B14 `paper_T2–T6`、`derived_model_means`；B19 `paper_T1/T2`；B22 `paper_T2`；B24 `paper_T3/T4/T11/T12`；B26 `paper_T4b`；B27 `paper_T4`；B35 `paper_T5_leaderboard`、`data_reference_cost`；B40 v1.0 与 v1.1（Inspect）。
- **GPT-5-mini**：B05 `paper_T8`、`paper_T9_T11`、`paper_T12_T14`、`paper_T15_T17`、`paper_T17_asr_system`、`derived_full_matrix_overall`；B27 `paper_T4`。
- **GPT-5-nano**：B27 `paper_T4`。
- **GPT-5.1**：B05 `paper_T8`、`paper_T9_T11`、`paper_T12_T14`、`paper_T15_T17`、`paper_T17_asr_system`、`derived_full_matrix_overall`。
- **GPT-5.1-Codex-Max**：B40 v1.0 与 v1.1（Inspect）；`results_logistic_fits`。
- **GPT-5.2**：B22 `paper_T2`；B40 v1.1；`results_logistic_fits`。
- **GPT-5.3-Codex**：B40 v1.1；`results_logistic_fits`。
- **GPT-5.4**：B06 `paper_T22_T24/T29/T31/T43`；B22 `paper_T2`；B40 `results_logistic_fits`。
- **GPT-5.5**：B06 `paper_T3/T4/T27/T28/T38/T41/T42`（5 模型核心面板）。
- **GPT-5.6 Sol**：B16 `paper_T11/T12`。
- **GPT-6 Astra**：B26 `paper_T4b`。

### o 系列与早期 OpenAI

- **o1**：B04 `paper_F3`、`paper_F5_transfer_matrix/long`、`derived_F5_transfer_summary`；B10 `paper_T2/T3`；B40 v1.0 与 v1.1（Inspect）；`paper_T6`；`results_logistic_fits`。
- **o1-preview**：B29 `paper_T2`、`paper_T10–T12`；B40 v1.0 与 v1.1；`paper_T6/T7`；`results_logistic_fits`。
- **o1-mini**：B37 `paper_T1`（`o1-mini-2024-09-12` Prompt）。
- **o1-2024-12-17**：B37 `paper_T1`（Prompt/FC）。
- **o3**：B04 `paper_F3`、`paper_F5_transfer_matrix/long`、`derived_F5_transfer_summary`；B19 `paper_T1`；B40 v1.0 与 v1.1（Inspect）；`paper_T6/T7`；`results_logistic_fits`。
- **o3-mini**：B33 `paper_T4`（SWE-agent/OpenHands/Aider 三个脚手架）。
- **o4-mini**：B13 `paper_T2/F5/T6`；B38 `paper_F3/F4`；B40 v1.0；`paper_T7`。
- **GPT-2**：B40 v1.0；`paper_T7`；`results_model_horizon_summary`（`gpt2`）。
- **davinci-002（GPT-3）**：B40 v1.0；`paper_T7`；`results_model_horizon_summary`（`davinci_002`）。
- **gpt-oss-120b**：B40 v1.0。

## 3. Anthropic Claude

- **Claude-2**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`；B09 `paper_T4`。
- **Claude 3 Haiku**：B07 `paper_T8/T9/T10`、`derived_T9_pivot_by_model`；B18 `paper_T2/T3/T5`。
- **Claude 3 Sonnet**：B01 `paper_T3`；B07 `paper_T9/T10`、`derived_T9_pivot_by_model`；B18 `paper_T2/T3/T5`。
- **Claude 3 Opus**：B01 `paper_T3`；B07 `paper_T8/T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`；B29 `paper_T2/T10–T12`；B39 `paper_T5/T14`；B40 v1.0 与 v1.1（Inspect）；`paper_T6/T7/T9`；`results_logistic_fits`。
- **Claude 3.5 Sonnet**：B01 `paper_T3`；B03 全部 9 张模型表；B04 `paper_F3`、F5 迁移矩阵/长表/汇总；B05 `paper_T3/T9_T11/T12_T14/T15_T17/T17_asr_system`、`derived_full_matrix_overall`；B07 `paper_T2/T3/T8/T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`；B10 `paper_T2/T3`；B11 全部 7 张模型表；B20 `paper_F7/T15/T16`、`results_model_stats`；B29 `paper_T2/T3/T9–T12`；B37 `paper_T1`（`Claude-3.5-Sonnet-20241022` Prompt/FC）；B40 v1.0（New/Old）与 v1.1（New/Old Inspect）；`paper_T6/T7/T9`；`results_logistic_fits`。
- **Claude 3.5 Haiku**：B08 `paper_T5/T6`；B37 `paper_T1`（`claude-3.5-haiku-20241022` Prompt/FC）。
- **Claude 3.7 Sonnet**：B04 `paper_F3`、F5 迁移矩阵/长表/汇总；B10 `paper_T2/T3/T4`；B13 `paper_T2/F5`；B33 `paper_T4`（三个脚手架）；B34 `paper_F8/F9/F10/F12/F13/F14`；B40 v1.0 与 v1.1（Inspect）；`paper_T6`；`results_logistic_fits`。
- **Claude 3.7 Sonnet:Thinking（扩展思考）**：B04 `paper_F3`、F5 矩阵/长表/汇总；B10 `paper_T2` 的 `Claude Sonnet 3.7 Ext. Thinking` 为同一配置。
- **Claude 4 Opus**：B40 v1.0 与 v1.1（Inspect）；`paper_T6`；`results_logistic_fits`。
- **Claude 4 Sonnet**：B40 v1.0。
- **Claude 4.1 Opus**：B40 v1.0 与 v1.1（Inspect）；`results_logistic_fits`。
- **Claude 4.5 Sonnet / Claude Sonnet 4.5**：B05 `paper_T8/T9_T11/T12_T14/T15_T17/T17_asr_system`、`derived_full_matrix_overall`；B14 `paper_T2–T6`、`derived_model_means`；B27 `paper_T4`；B40 v1.0。
- **Claude 4.5 Haiku / Claude Haiku 4.5**：B27 `paper_T4`。
- **Claude 4.5 Opus / Claude Opus 4.5**：B27 `paper_T4`；B40 v1.0 与 v1.1（Inspect）；`results_logistic_fits`。
- **Claude 4.6 Sonnet / Claude Sonnet 4.6**：B06 `paper_T22_T24/T43`；B35 `paper_T5_leaderboard`、`data_reference_cost`。
- **Claude 4.6 Opus / Claude Opus 4.6**：B06 `paper_T22_T24/T29/T43`；B35 `paper_T5_leaderboard`、`data_reference_cost`；B40 v1.1（Inspect）；`results_logistic_fits`。
- **Claude 4.7 Opus / Claude Opus 4.7**：B06 `paper_T3/T4/T27/T28/T38/T41/T42`；B35 `paper_T5_leaderboard`、`data_reference_cost`。
- **Claude Sonnet 5**：B16 `paper_T11/T12`。
- **Claude Mythos Preview（early）**：B40 `results_logistic_fits`、`results_model_horizon_summary`（`claude_mythos_preview_early_inspect`）。

## 4. Google Gemini

- **Gemini 1.0 Pro**：B07 `paper_T9/T10`、`derived_T9_pivot_by_model`。
- **Gemini 1.5 Flash**：B01 `paper_T3`；B07 `paper_T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`。
- **Gemini 1.5 Pro**：B01 `paper_T3`；B07 `paper_T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`；B29 `paper_T2/T10–T12`。
- **Gemini Pro**：B32 `paper_F11–F15`、`paper_F9`；B39 `paper_T5/T14`。
- **Gemini Pro 1.5**：B39 `paper_T5/T14`。
- **Gemini-ProV**：B39 `paper_T5/T14`（视觉版 Gemini Pro）。
- **Gemini 2.0 Flash Exp**：B37 `paper_T1`（Prompt/FC）。
- **Gemini 2.5 Flash**：B05 `paper_T9_T11/T12_T14/T15_T17/T17_asr_system`、`derived_full_matrix_overall`；B13 `paper_T2/F5/T6`；B24 `paper_T3/T4/T11/T12`；B34 `paper_F8/F9/F10/F12/F13/F14`。
- **Gemini 2.5 Pro**：B05 `paper_T3/T9_T11/T12_T14/T15_T17/T17_asr_system`、`derived_full_matrix_overall`；B13 `paper_T2/F5/T6`；B34 `paper_F8/F9/F10/F12/F13/F14`。
- **Gemini 2.5 Pro Preview**：B40 v1.0。
- **Gemini 3 Pro**：B14 `paper_T2–T6`、`derived_model_means`；B40 v1.1；`results_logistic_fits`。
- **Gemini 3 Flash**：B22 `paper_T2`（表中写作 `Gemini-3-Flash`）。
- **Gemini 3 Flash Preview**：B35 `paper_T5_leaderboard`、`data_reference_cost`。
- **Gemini 3.1 Pro**：B22 `paper_T2`。
- **Gemini 3.1 Pro Preview**：B35 `paper_T5_leaderboard`、`data_reference_cost`。
- **Gemini 3.8 Flash**：B16 `paper_T11/T12`。

## 5. Meta Llama

### Llama 2 / Llama 3

- **Llama 2 7B / 7b-chat**：B02 `paper_T6/T7/T8/T9/T10/T11/T12`；B28 `paper_T1/T3/T7/T8`（`Llama-2-7b-chat-hf`）；B37 `paper_T2/T3`（`Llama2-7B`）。
- **Llama 2 13B / 13b-chat**：B02 `paper_T6/T7/T8/T9/T11/T12`；B28 `paper_T1/T2/T7/T8`（`Llama-2-13b-chat-hf`）。
- **Llama 2 70B**：B02 `paper_T3/T6/T8/T9/T11/T12`。
- **Meta-Llama-3 8B Instruct**：B28 `paper_T1/T2/T3/T7/T8`（`Meta-Llama-3-8B-Instruct` / `Llama-3-8B-it`）；B37 `paper_T1`（Prompt）、`paper_T2/T3`。
- **Llama 3 8B Instruct**：B31 `paper_F1–F6`、`derived_figure_row_means`；B32 `paper_F11`。
- **Llama 3 70B Chat**：B01 `paper_T3`；B29 `paper_T2/T10–T12`；B31 `paper_F1–F6`、`derived_figure_row_means`；B32 `paper_F11–F15`、`paper_F9`；B39 `paper_T5/T14`。
- **Llama 3 405B**：B32 `paper_F7/F9/F11–F15`、`paper_T5`。

### Llama 3.1 / 3.2 / 3.3

- **Llama 3.1 8B Instruct**：B03 全部 9 张模型表；B07 `paper_T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`；B31 `paper_F1–F6`、`derived_figure_row_means`；B37 `paper_T1`（Prompt/FC）。
- **Llama 3.1 70B Instruct**：B03 全部 9 张模型表；B07 `paper_T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`；B29 `paper_T2/T10–T12`；B32 `paper_T5`（写作 `Llama 3.1 70b`）；B37 `paper_T1`（Prompt/FC）。
- **Llama 3.1 405B Instruct**：B04 `paper_F3`、F5 迁移矩阵/长表/汇总；B07 `paper_T9/T10`、`derived_T9_pivot_by_model`；B08 `paper_T5/T6`。
- **Llama 3.2 1B Instruct**：B37 `paper_T1`（Prompt）。
- **Llama 3.2 3B Instruct**：B37 `paper_T1`（Prompt）。
- **Llama 3.2 11B Vision**：B14 `paper_T2–T6`、`derived_model_means`。
- **Llama 3.2 90B**：B11 `paper_F3/F5/T3/T5/T11/T12`。
- **Llama 3.3 70B Instruct**：B04 `paper_F3`、F5 迁移矩阵/长表/汇总；B05 `paper_T3` 及 `paper_T9_T11/T12_T14/T15_T17/T17_asr_system`、`derived_full_matrix_overall`；B20 `paper_F7/T15/T16`、`results_model_stats`；B24 `paper_T3/T4/T11/T12`；B37 `paper_T1`（Prompt）。

## 6. DeepSeek

- **DeepSeek-V2.5**：B08 `paper_T5/T6`。
- **DeepSeek-V3**：B19 `paper_T1`；B40 v1.0。
- **DeepSeek-V3-0324**：B40 v1.0。
- **DeepSeek-V3.1**：B24 `paper_T3/T4/T11/T12`。
- **DeepSeek-V3.2**：B27 `paper_T4`；B35 `paper_T5_leaderboard`、`data_reference_cost`。
- **DeepSeek-R1**：B19 `paper_T1`；B34 `paper_F8/F12/F13/F14`（不含 F9/F10）；B40 v1.0。
- **DeepSeek-R1-0528**：B40 v1.0。
- **DeepSeek-V4-Flash**：B17 `paper_T2/T3/T4/T5`、`derived_policy_means`。
- **DeepSeek-V4-Pro**：B21 `paper_T2_lifecycle_24configs`、`derived_pooled_by_llm`。
- **deepseek_r1（B34 小写写法）**：B34 `paper_F8/F12/F13/F14`，别名同上。

## 7. 阿里 Qwen

### Qwen 1.x / Qwen2

- **Qwen-0.5B**：B02 `paper_T6/T7/T8/T9/T10/T11/T12`。
- **Qwen-1.8B**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **Qwen-4B**：B02 `paper_T6/T7/T8/T9/T11/T12`。
- **Qwen-7B**：B02 `paper_T6/T7/T8/T9/T11/T12`。
- **Qwen-14B**：B02 `paper_T6/T7/T8/T9/T10/T11/T12`。
- **Qwen-72B**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **Qwen2-7B**：B03 全部 9 张模型表。
- **Qwen2-72B**：B03 全部 9 张模型表。
- **Qwen2 72B Instruct**：B32 `paper_F4/F7/F11–F15`、`paper_T5`。
- **Qwen2-1.5B-Instruct**：B37 `paper_T1`（Prompt）。

### Qwen2.5

- **Qwen2.5-0.5B-Instruct**：B37 `paper_T1`（Prompt/FC）。
- **Qwen2.5-1.5B-Instruct**：B37 `paper_T1`（Prompt/FC）。
- **Qwen2.5-3B-Instruct**：B37 `paper_T1`（Prompt/FC）。
- **Qwen2.5-7B-Instruct**：B08 `paper_T5/T6`；B37 `paper_T1`（Prompt/FC）。
- **Qwen2.5-14B-Instruct**：B08 `paper_T5/T6`；B37 `paper_T1`（Prompt/FC）。
- **Qwen2.5-32B-Instruct**：B19 `paper_T1`（`Qwen-2.5 32B`）；B37 `paper_T1`（Prompt/FC）。
- **Qwen2.5-72B-Instruct**：B08 `paper_T5/T6`；B37 `paper_T1`（Prompt/FC）。

### Qwen3 / Qwen3.5+

- **Qwen3 8B**：B24 `paper_T3/T4/T11/T12`。
- **Qwen3 30B**：B24 `paper_T3/T4/T11/T12`。
- **Qwen3-4B**：B22 `paper_T2`。
- **Qwen3-4B-Instruct-2507**：B22 `paper_T2`。
- **Qwen3-235B-A22B**：B05 全模型面板；B06 `paper_T22_T24/T29/T32/T43`；B22 `paper_T2`（写作 `Qwen3-235B-A22B-Instruct-2507`）。
- **Qwen3-Coder**：B05 全模型面板。
- **Qwen3.5-4B**：B22 `paper_T2`。
- **Qwen3.5-397B-A17B**：B22 `paper_T2`。
- **Qwen3.5-Flash**：B27 `paper_T4`。
- **Qwen3.5-Plus**：B27 `paper_T4`。
- **Qwen3.6-Plus**：B06 `paper_T3/T4/T27/T28/T38/T41/T42`；B35 `paper_T5_leaderboard`、`data_reference_cost`。
- **Qwen3.7-Plus**：B17 `paper_T2/T3/T4/T5`、`derived_policy_means`。
- **Qwen3-VL-32B**：B14 `paper_T2–T6`、`derived_model_means`。
- **QwQ-32B**：B22 `paper_T2`。
- **Qwen-Max**：B39 `paper_T5/T14`。
- **Qwen-2-VL-72B**：B11 `paper_F3/F5/T3/T4/T5/T11/T12`。

## 8. Mistral / Mixtral

- **Mistral-7B**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`；B37 `paper_T2/T3`。
- **Mistral-7B-Instruct-v0.2**：B18 `paper_T2/T3/T5`；B28 `paper_T1/T7/T8`。
- **Mistral-7B-Instruct-v0.3**：B28 `paper_T1/T7/T8`。
- **Mistral Small 2**：B07 `paper_T9/T10`、`derived_T9_pivot_by_model`。
- **Mistral Large 2**：B07 `paper_T2/T3/T9/T10`、`derived_T9_pivot_by_model`。
- **Mistral Large**：B20 `paper_F7/T15/T16`、`results_model_stats`。
- **Mistral Small Latest**：B31 `paper_F1/F2/F5/F6`、`derived_figure_row_means`。
- **Mistral Medium Latest**：B31 `paper_F1/F2/F5/F6`、`derived_figure_row_means`。
- **Mistral Large Latest**：B31 `paper_F1/F2/F5/F6`、`derived_figure_row_means`。
- **Ministral-8B-Instruct-2410**：B37 `paper_T1`（FC）。
- **Mixtral-8x7B / Mixtral-8x7B-Instruct-v0.1**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`；B03 全部 9 张模型表；B18 `paper_T2/T3/T5`；B39 `paper_T5/T14`。
- **Mixtral 8x22B Instruct**：B29 `paper_T2/T10–T12`；B32 `paper_F11–F15`、`paper_F9`。
- **Pixtral Large**：B04 `paper_F3`（只有 F3，不进 14 模型迁移矩阵）。

## 9. Kimi（Moonshot）

- **Kimi-K2**：B19 `paper_T1`。
- **Kimi K2.5 / Kimi-K2.5**：B05 全模型面板；B06 `paper_T3/T4/T22_T24/T27/T28/T38/T41/T42/T43`；B14 `paper_T2–T6`、`derived_model_means`；B35 `paper_T5_leaderboard`、`data_reference_cost`。
- **Kimi K2.6**：B35 `paper_T5_leaderboard`、`data_reference_cost`。
- **Kimi-K2.7-Code**：B17 `paper_T2/T3/T4/T5`、`derived_policy_means`。
- **Kimi K2 Thinking**：B40 v1.0。

## 10. 智谱 GLM

- **GLM4-9B-Chat**：B08 `paper_T5/T6`。
- **GLM-4-9b-Chat**：B37 `paper_T1`（FC）。
- **GLM-4.6V**：B14 `paper_T2–T6`、`derived_model_means`。
- **GLM-4.7**：B27 `paper_T4`。
- **GLM-5**：B06 `paper_T22_T24/T29/T31/T43`。
- **GLM-5.1**：B06 `paper_T3/T4/T27/T28/T38/T41/T42`。
- **GLM-5.2**：B17 `paper_T2/T3/T4/T5`、`derived_policy_means`。
- **GLM 5.3**：B16 `paper_T11/T12`。

## 11. MiniMax

- **MiniMax-M3**：B21 `paper_T2_lifecycle_24configs`、`derived_pooled_by_llm`。
- **MiniMax M2.7**：B35 `paper_T5_leaderboard`、`data_reference_cost`。

## 12. Cohere、xAI、Amazon 与其他闭源模型

- **Command-R**：B04 `paper_F3`、F5 迁移矩阵/长表/汇总。
- **Command-R+**：B01 `paper_T3`。
- **Command-R-Plus**：B37 `paper_T1`（FC）；与 Command-R+ 同一系列的 BFCL 配置名。
- **Command R7B**：B37 `paper_T1`（FC）。
- **Grok 2**：B04 `paper_F3`、F5 迁移矩阵/长表/汇总。
- **Grok-3**：B19 `paper_T1`。
- **Grok 4**：B40 v1.0。
- **Amazon Nova Lite v1**：B04 `paper_F3`（只 F3）。
- **Amazon Nova Micro v1**：B04 `paper_F3`（只 F3）。
- **Amazon Nova Pro v1**：B04 `paper_F3`（只 F3）。
- **Amazon-Nova-Pro-v1:0**：B37 `paper_T1`（FC）。
- **Amazon-Nova-Lite-v1:0**：B37 `paper_T1`（FC）。
- **Amazon-Nova-Micro-v1:0**：B37 `paper_T1`（FC）。

## 13. 其他开源模型（B02 / B03 / B07 / B29 / B31–B37）

- **Gemma2-9B / Gemma2-27B**：B03 全部 9 张模型表。
- **Gemma-3-12b-it / Gemma-3-4b-it / Gemma-3-1b-it**：B37 `paper_T1`（均为 Prompt）。
- **Yi-34B / Nous-Yi-34B**：B02 `paper_T6/T7/T8/T9/T11/T12`（不含 T3/T10）。
- **OpenOrca-Mistral**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **OpenHermes-2.5-Mistral**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **OpenHermes-2-Mistral**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **Snorkel-Mistral**：B02 `paper_T6/T7/T8/T9/T10/T11/T12`。
- **Nous-Mixtral-DPO / Nous-Mixtral-SFT**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **MythoMax-13b**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **WizardLM-13B**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **Platypus2-70B**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **Capybara-7B**：B02 `paper_T3/T6/T8/T9/T11/T12`（不含 T7/T10）。
- **StripedHyena-7B**：B02 `paper_T6/T7/T8/T9/T10/T11/T12`。
- **Nous-Llama2-13b**：B02 `paper_T3/T6/T8/T9/T10/T11/T12`。
- **Vicuna-1.5-7B / 13B**：B09 `paper_T4`；B28 还有 `Vicuna-7b-v1.5`、`Vicuna-7b-v1.5-16k`、`Vicuna-13b-v1.5`、`Vicuna-13b-v1.5-16k`，均出现在 `paper_T1/T7/T8`。
- **Zephyr-7b-beta**：B18 `paper_T2/T3/T5`。
- **SEED-1.8**：B14 `paper_T2–T6`、`derived_model_means`。
- **InternVL3-38B**：B14 `paper_T2–T6`、`derived_model_means`。
- **CogAgent**：B39 `paper_T5/T14`。
- **CodeLlama-13B/34B/70B-Instruct**：B31 `paper_F1–F6`、`derived_figure_row_means`。
- **CodeLlama-7B**：B37 `paper_T2/T3`；不是 B31 的 CodeLlama-Instruct 面板。
- **Openfunctions-v2**：B37 `paper_T2/T3`。
- **Functionary-7B**：B37 `paper_T2/T3`。
- **Salesforce xLAM-7B**：B37 `paper_T2/T3`。
- **ToolACE-2-8B / ToolACE-8B**：B37 `paper_T1`（FC）。
- **Hammer2.1-0.5b/1.5b/3b/7b**：B37 `paper_T1`（FC）。
- **xLAM-1b-fc-r / 7b-fc-r / 7b-r / 8x7b-r**：B37 `paper_T1`（FC）。
- **Falcon3-1B/3B/7B/10B-Instruct**：B37 `paper_T1`（FC）。
- **MiniCPM3-4B**：B37 `paper_T1`（Prompt）；**MiniCPM3-4B-FC**：B37 `paper_T1`（FC）。
- **DBRX-Instruct**：B37 `paper_T1`（Prompt）。
- **Bielik-11B-v2.3-Instruct**：B37 `paper_T1`（Prompt）。
- **Granite-20b-FunctionCalling**：B37 `paper_T1`（FC）。
- **BitAgent-8B**：B37 `paper_T1`。
- **Haha-7B**：B37 `paper_T1`。
- **GoGoAgent**：B37 `paper_T1`。

## 14. 护栏 / 判官模型

- **LlamaGuard-7b**：B28 `paper_T3_llama_guard.csv`（与 Llama-2-7b-chat 对照）。
- **Meta-Llama-Guard-2-8B**：B28 `paper_T3_llama_guard.csv`。
- **LlamaGuard3-8B**：B22 `paper_T2`。
- **LlamaGuard4-12B**：B22 `paper_T2`。
- **Qwen3-Guard**：B22 `paper_T2`。
- **ShieldAgent**：B22 `paper_T2`。
- **AgentDoG-Qwen3-4B**：B22 `paper_T2`。
- **Llama 3 70B + LlamaGuard（output only / input+output）**：B32 `paper_F14/F15` 的护栏增强配置，不是独立基础模型。
- **Llama 3 405B + LlamaGuard（output only / input+output）**：B32 `paper_F14/F15` 的护栏增强配置。

## 15. B37 BFCL v4 的 69 个模型配置

B37 的 `paper_T1_leaderboard.csv` 原样列 69 个配置，按“基础模型（Prompt / FC 配置）”归并如下；每项都出现在 `paper_T1_leaderboard.csv`。

| 基础模型 | B37 配置 |
| --- | --- |
| gpt-4o-2024-11-20 | Prompt、FC |
| GPT-4-turbo-2024-04-09 | Prompt、FC |
| GPT-4o-mini-2024-07-18 | Prompt、FC |
| o1-2024-12-17 | Prompt、FC |
| o1-mini-2024-09-12 | Prompt |
| Qwen2.5-72B-Instruct | Prompt |
| Qwen2.5-32B-Instruct | Prompt、FC |
| Qwen2.5-14B-Instruct | Prompt、FC |
| Qwen2.5-7B-Instruct | Prompt、FC |
| Qwen2.5-3B-Instruct | Prompt、FC |
| Qwen2.5-1.5B-Instruct | Prompt、FC |
| Qwen2.5-0.5B-Instruct | Prompt、FC |
| Qwen2-1.5B-Instruct | Prompt |
| Gemini-2.0-Flash-Exp | Prompt、FC |
| ToolACE-2-8B | FC |
| ToolACE-8B | FC |
| Amazon-Nova-Pro-v1:0 | FC |
| Amazon-Nova-Lite-v1:0 | FC |
| Amazon-Nova-Micro-v1:0 | FC |
| Claude-3.5-Sonnet-20241022 | Prompt、FC |
| claude-3.5-haiku-20241022 | Prompt、FC |
| Llama-3.1-70B-Instruct | Prompt、FC |
| Llama-3.1-8B-Instruct | Prompt、FC |
| Llama-3.3-70B-Instruct | Prompt |
| Llama-3.2-3B-Instruct | Prompt |
| Llama-3.2-1B-Instruct | Prompt |
| Meta-Llama-3-8B-Instruct | Prompt |
| Hammer2.1-7b | FC |
| Hammer2.1-3b | FC |
| Hammer2.1-1.5b | FC |
| Hammer2.1-0.5b | FC |
| xLAM-8x7b-r | FC |
| xLAM-7b-r | FC |
| xLAM-7b-fc-r | FC |
| xLAM-1b-fc-r | FC |
| Falcon3-10B-Instruct | FC |
| Falcon3-7B-Instruct | FC |
| Falcon3-3B-Instruct | FC |
| Falcon3-1B-Instruct | FC |
| Gemma-3-12b-it | Prompt |
| Gemma-3-4b-it | Prompt |
| Gemma-3-1b-it | Prompt |
| MiniCPM3-4B | Prompt |
| MiniCPM3-4B-FC | FC |
| GLM-4-9b-Chat | FC |
| DBRX-Instruct | Prompt |
| Bielik-11B-v2.3-Instruct | Prompt |
| Command-R-Plus | FC |
| Command R7B | FC |
| Ministral-8B-Instruct-2410 | FC |
| Granite-20b-FunctionCalling | FC |
| BitAgent-8B | 单一配置 |
| Haha-7B | 单一配置 |
| GoGoAgent | 单一配置 |

另有 `paper_T2_perplexity.csv`、`paper_T3_char_nll.csv` 的 7 个模型：Llama2-7B、Openfunctions-v2、CodeLlama-7B、Meta-Llama-3 8B、Mistral-7B、Functionary-7B、Salesforce xLAM-7B。它们不出现在 `paper_T1` 的 69 配置面板中。

## 16. B40 METR：版本与快照

`B40` 的模型不是统一面板，而是两版人类基线对照：v1.0 与 v1.1。为避免把“Inspect 运行标签”误当成新模型，原文写法的版本如下。

### v1.0（`data_v1_0_by_model`、`data_v1_0_success_by_model_x_length`）

- **Claude Opus 4.5、GPT-5.1-Codex-Max、GPT-5、o3、Claude 4.1 Opus、Claude Sonnet 4.5、Claude 4 Opus、Claude 4 Sonnet、o4-mini、gpt-oss-120b**
- **Claude 3.7 Sonnet、Grok 4、Kimi K2 Thinking、o1、Gemini 2.5 Pro Preview**
- **DeepSeek-R1-0528、DeepSeek-R1、DeepSeek-V3-0324、DeepSeek-V3**
- **Claude 3.5 Sonnet (New)、Claude 3.5 Sonnet (Old)、o1-preview、Qwen2-72B、Qwen2.5-72B**
- **GPT-4o、GPT-4 1106、GPT-4 0314、GPT-4 0125、GPT-4 Turbo、Claude 3 Opus**
- **GPT-2、davinci-002（GPT-3）、gpt-3.5-turbo-instruct**

### v1.1（`data_v1_1_by_model`、`data_v1_1_success_by_model_x_length`）

- **Claude Opus 4.6 (Inspect)、Claude Opus 4.5 (Inspect)、GPT-5.2、Gemini 3 Pro、GPT-5.3-Codex**
- **GPT-5 (Inspect)、GPT-5.1-Codex-Max (Inspect)、o3 (Inspect)、Claude 4.1 Opus (Inspect)、Claude 4 Opus (Inspect)**
- **Claude 3.7 Sonnet (Inspect)、o1 (Inspect)、Claude 3.5 Sonnet (New) (Inspect)、Claude 3.5 Sonnet (Old) (Inspect)**
- **o1-preview、GPT-4o (Inspect)、Claude 3 Opus (Inspect)、GPT-4 1106 (Inspect)、GPT-4 0314、GPT-4 Turbo (Inspect)**

`results_logistic_fits.csv` 另包含 **Gemini 3.1 Pro、GPT-5.4、Claude Mythos Preview (early)**；`results_model_horizon_summary.csv` 用 26 个内部别名汇总时间跨度，不逐个重复。

## 17. 智能体与基线

- **B12 ST-WebAgentBench**：`AWM`、`WebVoyager`、`WorkArena Legacy`，见 `paper_F2_agent_metrics.csv`。
- **B30 CVE-Bench**：`Cy-Agent`、`AutoGPT`、`T-Agent`，见 `paper_F3`、`paper_F4`；其中 T-Agent 由 GPT-4o 驱动，不是独立 LLM。
- **B33 SEC-bench 脚手架**：`SWE-agent`、`OpenHands`、`Aider`，与 Claude 3.7 Sonnet / GPT-4o / o3-mini 交叉，见 `paper_T4_agents_models.csv`。
- **B09 NoAct**：`paper_T4_agent_evaluation.csv` 的无动作基线。
- **B28 Random**：`paper_T1_main_results.csv` 的随机基线；`AVG` 是汇总行，不是模型。
- **B40 human**：`data_v1_0_by_model.csv`、`data_v1_1_by_model.csv` 的人类基线，不是 LLM。

## 18. 使用提醒

1. B37 的 `Prompt` 和 `FC` 是同一基础模型的两种调用配置，不能合并成“两个模型”；但也不应把一个配置的成绩当成整个模型成绩。
2. B40 的 `(Inspect)` 是运行/评测框架标签，不是新版本号；同一模型可能在 v1.0 与 v1.1 更换了 scaffold。
3. B31 的 `paper_F3/F4` 只测 8 个模型中的 7 个（不含 Mistral Small/Medium/Large），而 `paper_F5` 不含 GPT-4；按本索引中的逐表标注读取。
4. B02 的 `paper_T7` 是低有效率子集，`paper_T10` 是失败案例质量子集，不能把它们当作完整 30 模型主榜。
5. 论文模型名大小写/连接符不统一（如 `Mixtral-8x7B` 与 `Mixtral 8x7B`、`Qwen-2.5` 与 `Qwen2.5`）时，本文已在同一条目内合并；没有证据时不擅自把不同参数规模的模型合并。
