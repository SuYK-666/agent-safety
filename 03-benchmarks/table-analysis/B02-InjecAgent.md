# B02 InjecAgent — 数据表格与分析

> 论文：InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated LLM Agents（ACL Findings 2024）  
> 表格：[analysis/tables](../B02-injecagent/analysis/tables/)

## 1. 数据集结构

`data_test_case_files.csv`：

| 文件 | 攻击类别 | 设置 | 用例 | 用户工具 | 攻击指令 | 平均工具返回长度 |
| --- | --- | --- | --- | --- | --- | --- |
| test_cases_dh_base | 直接伤害 | base | 510 | 17 | 30 | 264 字符 |
| test_cases_dh_enhanced | 直接伤害 | enhanced | 510 | 17 | 30 | 360 字符 |
| test_cases_ds_base | 数据窃取 | base | 544 | 17 | 32 | 299 字符 |
| test_cases_ds_enhanced | 数据窃取 | enhanced | 544 | 17 | 32 | 395 字符 |

- 用例是完全交叉构造：17 个用户案例 × 30 个直接伤害攻击 = 510，17 × 32 个数据窃取攻击 = 544，合计 1,054。enhanced 版本是在同一攻击指令前加上 “hacking prompt”（平均多出约 96 个字符），用例一一对应。
- `data_attack_type_by_attack_category.csv`（base，1,054 条）：直接伤害中 Data Security 187、Physical 170、Financial 153；数据窃取中 Others 255、Physical Data 187、Financial Data 102。即 17×(11/10/9) 和 17×(15/11/6)，与论文 Table 1 的攻击者案例数精确对应。
- `data_user_case_content_freedom.csv`：17 个用户案例中 12 个为“高内容自由度”（注入位置是评论、笔记、推文正文等自由文本），5 个为低自由度，与论文附录 D.1 一致。
- `tools.json` 含 38 个工具包、330 个工具（来自 ToolEmu），`attacker_simulated_responses.json` 缓存了 2,347 条数据窃取第二步的模拟返回。
- “Modifed” 字段：直接伤害有 11 个攻击者案例（187/17）、数据窃取有 9 个（153/17）是为补全工具必填参数而人工改写过的。

## 2. 论文主结果：ASR-valid（有效率 >50% 的 20 个智能体）

`paper_T3_asr_valid_main.csv`（Table 3）列包括 base/enhanced × {直接伤害, 窃取第1步 S1, 第2步 S2, 窃取总, 总}。精选：

| 类型 | 模型 | base 总 ASR | enhanced 总 ASR |
| --- | --- | --- | --- |
| 提示型 | Llama2-70B | 86.9 | 88.2 |
| 提示型 | Capybara-7B | 34.9 | 83.5 |
| 提示型 | Nous-Mixtral-DPO | 43.6 | 72.5 |
| 提示型 | GPT-4 | 23.6 | 47.0 |
| 提示型 | GPT-3.5 | 23.7 | 39.8 |
| 提示型 | Claude-2 | 11.4 | **3.4** |
| 微调型 | GPT-4 (FT) | 6.6 | 7.1 |
| 微调型 | GPT-3.5 (FT) | 3.8 | 8.4 |

分析：

- hacking prompt 对几乎所有模型都显著抬高 ASR（GPT-4 从 23.6% 到 47.0%，Capybara-7B 从 34.9% 到 83.5%）。唯一反例是 Claude-2，enhanced 下反而降到 3.4%，说明“明显的注入话术”会触发其防护。
- 函数调用微调（OpenAI 原生 tool calling）的 GPT 系列 ASR 低一个数量级（3.8–8.4%），提示型 ReAct 智能体则普遍在 20–50% 以上。
- 数据窃取第二步 S2（把已取到的数据发给攻击者）几乎总是成功：大多数模型 >75%，微调型 GPT 为 100%。说明一旦第一步被劫持，防线基本失守，安全重点应放在第一步。
- 注意论文 Sec.3.2 正文写“微调 GPT-4 和 GPT-3.5 分别为 3.8% 和 6.6%”，但 Table 3 中 3.8 对应 GPT-3.5、6.6 对应 GPT-4，正文顺序与表相反，以表为准。

## 3. 其他转录表

- `paper_T6_valid_rates.csv`（Table 6）：30 个智能体在无攻击/base/enhanced 下的有效输出率。小模型在攻击下有效率暴跌（Llama2-13B 无攻击 100% → base 1.7%），这就是论文要区分 ASR-valid 和 ASR-all 的原因。
- `paper_T7_asr_valid_low_valid_agents.csv`（Table 7）：有效率 <50% 的 10 个智能体的 ASR-valid，样本少、波动大（如 Qwen-7B 87.4%），仅作参考。
- `paper_T8_asr_all.csv`（Table 8）：全部 30 个智能体的 ASR-all（以全部用例为分母），更适合做排行榜：GPT-4 base 23.3 / enhanced 46.8，Llama2-70B 39.2 / 46.9，Nous-Mixtral-DPO 31.6 / 54.6。
- `paper_T9_asr_all_by_attack_type.csv`（Table 9）：按 6 种攻击子类的 ASR-all，平均值 18.4/19.5/21.0/19.7/20.2/17.6，差异很小——论文结论是攻击类型对成功率影响不大，主要差异来自用户案例。
- `paper_T4_association_user_vs_attacker_case.csv`（Table 4）：Cramér's V 用户案例 0.28/0.31 > 攻击者案例 0.18/0.20，即“注入出现在什么上下文里”比“注入要求做什么”更决定成败；高内容自由度的注入位置更易被攻破。
- `paper_T10_response_quality_failed_cases.csv`（Table 10）：攻击失败时回复的相关性/清晰度（0–2），Claude-2 清晰度最高（1.86/1.92），因为它会主动提醒用户工具返回中有异常内容。
- `paper_T11/T12_*_simple_react.csv`：换成更短的 LangChain ReAct 提示后的 ASR-valid / ASR-all。GPT-4 基本不变（22.2/46.1），但部分开源模型变化很大（如 Platypus2-70B 直接伤害从 34.3 降到 0.2），说明提示模板本身是重要变量。

## 4. 展示建议

- 用 ASR-all（Table 8）做 30 个模型的完整排行，用 base vs enhanced 双柱展示 hacking prompt 的放大效应。
- 用“S1→S2 漏斗”展示数据窃取的两步成功率。
- 数据集视图：17 个用户工具 × 62 个攻击指令的交叉矩阵。
