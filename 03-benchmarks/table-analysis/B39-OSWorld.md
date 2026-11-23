# B39 OSWorld — 数据表格与分析

> 论文：OSWorld: Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments（NeurIPS 2024 D&B）  
> 表格：[analysis/tables](../B39-osworld/analysis/tables/)  
> 定位：**能力基准**；B13 OS-Harm 基于它的环境构造安全任务，展示时可作为“电脑操作智能体能力基线”。

## 1. 数据集结构（固定提交 5123bfdb）

`data_ubuntu_app_summary.csv`（由任务配置统计）：

| 应用 | 任务 | 不可完成任务 | 平均指令词数 |
| --- | --- | --- | --- |
| 多应用工作流 | 101 | 1 | 43.2 |
| LibreOffice Calc | 47 | 1 | 35.0 |
| LibreOffice Impress | 47 | 0 | 23.5 |
| Chrome | 45 | 3 | 19.9 |
| GIMP | 26 | 9 | 15.0 |
| OS 终端/设置 | 24 | 5 | 18.5 |
| Writer / VS Code | 23 / 23 | 1 / 4 | 27.9 / 16.7 |
| VLC / Thunderbird | 17 / 15 | 2 / 0 | 29.0 / 28.3 |
| 合计 | **368** | 26 | |

- 论文为 369 个任务（Chrome 46）、30 个不可完成任务；当前上游索引 368 个，说明后续有修订/下线（另有 retired 目录）。
- 不可完成任务（如要求软件做不到的功能）用来考查智能体是否会如实说“做不到”，GIMP 最多（9 个）。
- Windows 分析集：论文 43 个，当前仓库 49 个（多应用 22、Excel 11、Word 9、PPT 7）。
- 每个任务带有初始化配置和自动评估函数；评估函数多达 120+ 种（`data_eval_functions_top.csv`），这是 OSWorld 能做可执行评测的关键。
- test_small 为 39 个任务的快速子集。

## 2. 主结果（Table 5，成功率）

| 输入 | 最佳模型 | 总体 | 人类 |
| --- | --- | --- | --- |
| 可访问性树 | GPT-4 | 12.24% | 72.36% |
| 截图 | Gemini-ProV | 5.80% | |
| 截图 + 可访问性树 | GPT-4V | 12.17% | |
| Set-of-Mark | GPT-4V | 11.77% | |

- 2024 年的最好模型只有约 12% 成功率，人类 72%。按类别看，多应用工作流最难（≤7.56%），OS 类较易（GPT-4o + 截图+树达 41.67%）。
- 纯截图输入明显差于带可访问性树的输入，主要瓶颈是界面元素定位（grounding）。
- `paper_T14_success_by_app.csv` 给出 10 个应用的细分；Thunderbird、VS Code 等应用上部分模型可达 30% 以上，Calc 几乎所有模型 <9%。

## 3. 与安全测评的联系

OSWorld 只测能否完成任务，不测安全。B13 OS-Harm 在同一环境上构造了滥用、注入、误操作三类任务；两者结合可以展示“能力提升 → 风险暴露”的关系。

## 4. 展示建议

输入模态 × 模型的成功率分组柱（Table 5）+ 人类基线横线；数据集按应用的任务数与不可完成任务数。
