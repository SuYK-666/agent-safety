# B29 Cybench — 数据表格与分析

> 论文：Cybench: A Framework for Evaluating Cybersecurity Capabilities and Risks of Language Models（ICLR 2025）  
> 表格：[analysis/tables](../B29-cybench/analysis/tables/)

## 1. 数据集结构

40 道专业级 CTF 题，来自 4 场比赛（论文 Table 8）：HackTheBox 2024 17 道、SekaiCTF 12 道、Glacier 9 道、HKCert 2 道。我按论文 Table 10 统计了全部 40 题的类别（`derived_40tasks_category_x_competition.csv`）：密码学 16、Web 8、逆向 6、取证 4、杂项 4、Pwn 2。

本包只收录元数据（不含题目文件和 Docker 环境），且 Glacier 9 题的 metadata 不在包内（`data_overview.csv`）：包内 31 道官方题有元数据，共 129 个子任务，每题 2–7 个子任务（多为 3–4 个）；18 道需要连接目标服务。另有 3 个不在官方 40 题内的额外元数据。

难度以“首解时间”（FST，人类队伍最快解出时间）衡量：从 2 分钟到 24 小时 54 分钟。

## 2. 主结果（Table 2，结构化 bash 智能体，单次尝试）

| 模型 | 无指导解出率 | 有子任务指导解出率 | 子任务得分 | 最难解出题 FST |
| --- | --- | --- | --- | --- |
| Claude 3.5 Sonnet | **17.5%** | 15.0% | 43.9% | 11 min |
| GPT-4o | 12.5% | **17.5%** | 28.7% | **52 min**（指导下） |
| Claude 3 Opus | 10.0% | 12.5% | 36.8% | 11 min |
| OpenAI o1-preview | 10.0% | 10.0% | **46.8%** | 11 min |
| Llama 3.1 405B | 7.5% | 15.0% | 20.5% | 11 min |
| Mixtral 8x22B | 7.5% | 5.0% | 15.2% | 7 min |
| Gemini 1.5 Pro | 7.5% | 5.0% | 11.7% | 6 min |
| Llama 3 70B | 5.0% | 7.5% | 8.2% | 11 min |

- 最强模型无指导也只能解 17.5%（7/40 题），且**只能解人类 11 分钟内能解的题**。
- `derived_fst_bins.csv`（我根据 Table 10 计算）：FST ≤11 分钟的 11 题中有 8 题至少一个模型解出；FST >11 分钟的 29 题在无指导下**没有任何模型解出**。FST 是非常强的难度预测指标。
- 子任务得分能提供更细的区分度（论文称 58.8% 的格子非零），o1-preview 子任务得分最高但整题解出率并不高。

## 3. 脚手架与多次尝试（Table 3）

3 次尝试取最好：Claude 3.5 Sonnet 在伪终端脚手架下无指导 20%、指导下 27.5%，并在指导下解出 FST 2 小时 3 分钟的题；GPT-4o 在结构化 bash 下指导 22.5%。脚手架的影响对不同模型方向不同（GPT-4o 用伪终端反而下降）。

## 4. 逐题矩阵

`paper_T10/T11/T12_*_per_task.csv` 为 40 题 × 8 模型的完整结果；`derived_task_solve_counts.csv` 统计每题被几个模型解出。Dynastic（8/8）、Packed Away（7/8）、Loot Stash（6/8）最容易；Urgent（FST 4 分钟）无指导与指导下都没有模型解出。

论文附录还有 Table 13–71（每题 token、时间、迭代次数等资源消耗），本次未逐表转录。

## 5. 展示建议

按 FST 排序的 40 题 × 模型“解出热力图”是 Cybench 最直观的视图，能清楚看到能力边界停在约 11 分钟人类难度。
