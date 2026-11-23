# B38 τ²-Bench — 数据表格与分析

> 论文：τ²-Bench: Evaluating Conversational Agents in a Dual-Control Environment（Sierra）  
> 表格：[analysis/tables](../B38-tau2-bench/analysis/tables/)  
> 定位：**能力/可靠性基准**，也是 B27 DUMA-Bench 的底座框架，在展示系统中可作为“双控交互下的任务可靠性”参照。

## 1. 数据集结构（固定提交 c06b07dd）

`data_task_files.csv` / `data_splits.csv`：

| 领域 | 任务 | 划分 | 平均参考动作数 |
| --- | --- | --- | --- |
| airline | 50 | train 30 / test 20 | 2.84 |
| retail | 114（论文 115） | train 74 / test 40 | 4.82 |
| telecom | base 114；full 2,285；small 20 | train 74 / test 40 | 5.78（full） |
| banking_knowledge | 97 | – | 9.85 |
| intake | 200 | – | – |

banking_knowledge、intake 是论文之后新增的领域；各领域另有 2 条语音版样例。

telecom 是论文新增的**双控**领域：用户也有自己的工具（模拟手机，15 写 + 15 读），智能体必须指导用户操作。full 集统计（`data_telecom_*.csv`）：MMS 问题 86.8%、移动数据 11.1%、服务问题 2.1%；三种用户画像（无/易/难）各约 1/3；参考动作中 **82.7% 需要由用户执行**，只有 17.3% 由智能体自己执行。

## 2. 主结果（Figure 3，pass^k = k 次都成功的概率）

| 模型 | Retail pass^1 → pass^4 | Airline | Telecom |
| --- | --- | --- | --- |
| claude-3.7-sonnet | **0.79 → 0.60** | 0.50 → 0.36 | 0.49 → 0.25 |
| gpt-4.1 | 0.74 → 0.53 | 0.56 → 0.40 | **0.34 → 0.19** |
| o4-mini | 0.71 → 0.46 | 0.59 → 0.38 | 0.42 → 0.26 |
| gpt-4.1-mini | 0.66 → 0.39 | 0.51 → 0.26 | 0.44 → 0.18 |

- 双控的 telecom 最难：gpt-4.1 从零售 74% 降到 34%。
- 可靠性随 k 迅速下降：要求连续 4 次都成功时，telecom 只剩 18–26%。对智能体安全展示有直接意义——**单次成功率高估了真实部署的稳定性**（同样的结论见 B16、B27 的 pass^k / Safe³）。

## 3. 双控消融（Figure 4，telecom）

| 模型 | 默认（与用户协作） | 无用户（智能体全权操作） | 给出标准操作计划 |
| --- | --- | --- | --- |
| gpt-4.1 | 0.34 | 0.52 | 0.73 |
| o4-mini | 0.42 | 0.67 | 0.96 |

从“无用户”到“需要指导用户”，pass^1 下降 18–25 个点；给出计划后大幅提升——瓶颈既有推理也有沟通。改用工作流式策略文档后默认模式提升到 0.52 / 0.59。

## 4. 用户模拟器质量（Table 2）

人工标注的模拟用户关键错误率：airline 13%、retail 12%、telecom 6%。评测结论有一定噪声。

## 5. 展示建议

模型 × 领域 pass^k 折线（k=1..4）+ 双控消融三柱图。
