# B14 MMA-SafetyBench — 数据表格与分析

> 论文：MMA-SafetyBench: A Benchmark for Multimodal Agent Safety Evaluation（视觉语义劫持）  
> 表格：[analysis/tables](../B14-mma-safetybench/analysis/tables/)

## 1. 数据集结构与公开范围

论文：1,083 条对抗轨迹，覆盖 5 个领域（Web 200、Document 200、Desktop GUI 209、Mobile 283、Video 191）；三类攻击意图（破坏诱导、数据外泄、任务劫持），用伪造的系统弹窗、通知、文档内嵌指令、视频叠加字幕等“看起来像原生界面元素”的视觉载荷实施。

本包实际收录（`data_release_coverage.csv`）：

- Desktop GUI：209 条攻击（与论文完全一致），来自 42 个 OSWorld Chrome 基础任务，绝大多数基础任务派生 5 个攻击变体（`data_gui_attacks_per_base_task.csv`）。载荷类别（`data_gui_attack_payload_category.csv`）：隐私外泄 86（41%）、金融劫持 51、Root 提权 42、持续监控 29、恢复出厂 1。每条带有伪造按钮的 bbox，用于判定“点击坐标是否落在恶意目标内”。
- Document：200 条（简历 100 + 发票 100，与论文一致）。
- Web、Mobile、Video 三个领域的数据不在本包中。

## 2. 主结果：9 个视觉模型 × 5 个领域

`paper_T2_asr.csv`（ASR，越低越好）与 `derived_model_means.csv`（我计算的 5 领域简单平均）：

| 模型 | 平均 ASR | 加安全优先提示后 | 平均 SCR（语义被劫持） | 干净任务成功率 |
| --- | --- | --- | --- | --- |
| GLM-4.6V | **73.65** | 31.57 | 86.27 | 87.32 |
| SEED-1.8 | 70.19 | 30.36 | 85.65 | 81.44 |
| Qwen3-VL-32B | 67.50 | 30.35 | 83.69 | 86.39 |
| InternVL3-38B | 64.59 | 24.95 | 79.21 | 82.95 |
| GPT-5 | 57.77 | 15.27 | 72.93 | 86.52 |
| Kimi-K2.5 | 51.17 | 16.28 | 63.48 | 83.20 |
| Claude 4.5 Sonnet | 42.85 | 9.59 | 58.22 | **89.69** |
| Gemini 3 Pro | 41.93 | **8.91** | 53.39 | 89.64 |
| Llama-3.2-11B-Vision | **27.12** | 8.64 | 40.67 | 69.11 |

- 视觉注入非常有效：9 个模型中 8 个平均 ASR 超过 40%。GPT-5 在 GUI 上 75.12%，GLM-4.6V 在 Video 上 87.96%。
- Llama-3.2-11B 的低 ASR 伴随最低的干净任务成功率（69%）——它常常点不准，属于“能力不足带来的安全”。Claude 4.5 Sonnet 与 Gemini 3 Pro 则是在高效用下保持较低 ASR。
- 按领域（`derived_domain_means.csv`）：Video（69.2%）和 GUI（63.7%）最脆弱，Web 最低（43.0%）。
- **SCR 比 ASR 普遍高 10–30 个点**：在 GUI 上模型的“语义已经被劫持”（推理中采纳了恶意指令）达 86%，只是因为点击坐标没落在伪造按钮上才没被计为攻击成功。Claude 4.5 Sonnet 在 GUI 上 SCR−ASR 差值达 +36.4。展示时建议同时呈现两者。

## 3. 防御与对照

- `paper_T5_asr_with_safety_prompt.csv`：在系统提示前加“安全优先”指令，45 个模型–领域组合全部下降，平均 ASR 从 55.20% 降到 19.54%（相对降幅 64.6%）。但残余仍高：GLM-4.6V 在 GUI 上 46.89%、Video 45.03%。
- `paper_T3_neutral_prompt_asr.csv`：把用户提示换成中性措辞后 ASR 只略降，说明攻击不依赖特定的用户提示写法。
- `paper_T4_clean_task_success.csv`：所有前沿模型在干净任务上 78–94%，排除了“模型本身做不了这些任务”的解释。
- 判官（GPT-5）与人工在 300 条审计轨迹中 290 条一致。

## 4. 展示建议

9 模型 × 5 领域 ASR 热力图，加 ASR→SCR 的“额外语义劫持”叠加柱，以及加入安全提示前后的对比。
