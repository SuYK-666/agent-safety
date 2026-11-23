# B37 BFCL（Berkeley Function Calling Leaderboard）— 数据表格与分析

> 论文：The Berkeley Function Calling Leaderboard (BFCL): From Tool Use to Agentic Evaluation of LLMs（ICML 2025）  
> 表格：[analysis/tables](../B37-bfcl-v4/analysis/tables/)  
> 定位：**能力基准**，在安全展示系统中作为“工具调用能力”与“过度拒绝/幻觉”的对照。

## 1. 数据集结构（v4，`data_category_sizes.csv`）

20 个分片共 4,697 条（文件为逐行 JSON）：

| 组 | 条数 | 包含 |
| --- | --- | --- |
| 众包真实请求（Live） | 1,351 | simple 258、multiple 1,053、parallel 16、parallel_multiple 24 |
| 非 Live 单轮 | 1,150 | Python 400、Java 100、JS 50、multiple/parallel/parallel_multiple 各 200 |
| 幻觉测量 | 1,140 | irrelevance 240、live_irrelevance 884、live_relevance 16 |
| 多轮 | 800 | base / 缺函数 / 缺参数 / 长上下文 各 200，平均 3.7–4.7 轮 |
| 智能体 | 255 | 记忆 155、网页搜索 100 |

- 幻觉类（irrelevance）测的是“给的函数都不相关时模型是否会乱调”，与安全中的“过度执行”最相关；没有标准答案文件，因为正确行为是不调用。
- 多轮任务基于 11 套模拟 API（文件系统、交易机器人、车辆控制、消息、订票等，`data_multi_turn_apis.csv`）。
- live_multiple 平均提供 3.97 个候选函数，考查函数选择。

## 2. 主结果（Table 1，71 个模型配置）

完整 23 列见 `paper_T1_leaderboard.csv`。前几名：

| 模型 | 总体 | 多轮 base | 缺参数 | 长上下文 | 网页搜索 | 记忆 | 不相关检测 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| gpt-4o-2024-11-20 (Prompt) | **66.4** | 59.0 | 35.5 | 55.0 | 64.0 | 6.0 | 83.8 |
| gpt-4o-2024-11-20 (FC) | 65.8 | 62.5 | 37.5 | 58.0 | 82.0 | 0.0 | 83.1 |
| GPT-4-turbo (FC) | 60.9 | 54.0 | 35.5 | 49.5 | 66.0 | 4.0 | 83.8 |
| o1-2024-12-17 (Prompt) | 59.1 | 50.5 | 48.5 | 44.5 | 5.0 | 12.0 | 87.8 |
| Qwen2.5-72B (Prompt) | 57.0 | 24.5 | 15.5 | 12.0 | 54.0 | 8.0 | 72.8 |

- 单轮调用已接近饱和（简单/多函数 AST 普遍 90%+），**差距主要在多轮与智能体任务**：多轮缺参数、长上下文普遍 <50%，记忆任务几乎所有模型 <12%。
- 原生函数调用（FC）与提示式（Prompt）差异大且方向不一：Claude-3.5-Sonnet FC 模式下并行调用只有 3.5%（新版本取消了并行调用），Prompt 模式为 70.5%。
- 不相关检测（是否在不该调用时拒绝调用）从 4.9%（Llama-3.1-8B FC）到 91.5%（Gemini-2.0-Flash FC）不等——对智能体安全意味着部分模型很容易“乱用工具”。
- 多轮错误分析（Figure 5）：最常见的失败是“误解环境状态”（幻觉出不存在的目录、过早终止）。

## 3. 数据污染检测（Table 2/3）

多数模型在众包数据上的困惑度低于单轮静态集（如 Llama2-7B 3.47 → 2.56），说明并未背过测试集；xLAM-7B 例外（3.67 → 5.09），提示可能针对静态集过拟合。

## 4. 展示建议

按“单轮 / 众包 / 幻觉 / 多轮 / 智能体”五组做雷达图对比模型；突出 Irrelevance 列作为“过度调用风险”指标。
