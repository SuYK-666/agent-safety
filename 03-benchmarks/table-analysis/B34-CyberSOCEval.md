# B34 CyberSOCEval — 数据表格与分析

> 论文：CyberSOCEval: Benchmarking LLMs Capabilities for Malware Analysis and Threat Intelligence Reasoning（Meta × CrowdStrike）  
> 表格：[analysis/tables](../B34-cybersoceval/analysis/tables/)  
> Figure 8/9/13/14 的格子印有数值（已逐格转录）；Figure 10、12 为折线/柱图，标注为近似。

## 1. 数据集结构（`data_overview.csv`）

这是一个**防守方能力**基准（SOC 分析员任务），全部是多选题，必须选中全部且仅选中正确答案才算对。

- 恶意软件分析：609 题，基于 175 份 Hybrid Analysis 沙箱运行报告（包内有 178 份报告 JSON，不含可执行样本）。5 个恶意软件家族（`data_malware_attack_x_difficulty.csv`）：信息窃取 167、勒索 127、Remcos 远控 114、用户态脱钩 112、杀软终结者 89；难度 easy 451 / medium 136 / hard 22。8 个题目主题，行为分析 100 题最多。
- 选项与答案（`data_malware_options_answers.csv`）：每题 3–10 个选项，正确答案 1–9 个，多数为 1–3 个。随机猜中概率约 0.63%。
- 威胁情报推理：588 题，基于 45 份报告（CrowdStrike、NSA、IC3、CISA）；以图片形式输入每页报告。公开版中这部分的 topic/difficulty 字段为空。

## 2. 恶意软件分析结果（Figure 8）

| 模型 | 简单 | 中等 | 困难 | 总体 |
| --- | --- | --- | --- | --- |
| claude-3-7-sonnet | 37% | 23% | 24% | **33.51%** |
| deepseek_r1 | 33% | 26% | 14% | 30.81% |
| gpt-o3 | 31% | 26% | 14% | 29.44% |
| llama4-maverick | 31% | 21% | 18% | 28.57% |
| gemini-2.5-pro | 29% | 24% | 5% | 27.42% |
| gpt-4o | 28% | 16% | 5% | 24.63% |
| llama4-scout | 26% | 16% | **0%** | 22.99% |

- 总体只有 23–34%，远高于随机但离实用很远。按家族看（Figure 13），信息窃取类最容易（Claude 42%），勒索和杀软终结者类普遍 20–30%。按主题看（Figure 14），行为分析、ATT&CK 映射较好（40–50%），**规避技术**最差（GPT-4o 仅 8%）。
- 推理模型（o3、R1）没有带来明显的“跃升”，作者认为安全领域需要专门的训练数据。

## 3. 威胁情报推理结果（Figure 9）

总体 43–53%：gpt-o3 52.87%、llama4-maverick 50.42%、claude-3-7-sonnet 49.25%、gpt-4o 43.09%。NSA 报告的题最容易（62–73%），CISA 报告最难（30–50%）。

Figure 10：所有模型用文字输入都比用图片输入好约 5–10 个百分点，说明多模态模型“读图里的文字”仍是短板。

## 4. 展示建议

两个子基准各一张“模型 × 分类”热力图；Figure 10 的“图片 vs 文字”对比可做哑铃图。该基准与攻击类基准（B29–B32）结合，可展示“同一模型的攻防能力”。
