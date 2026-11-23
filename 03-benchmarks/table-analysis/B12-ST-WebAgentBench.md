# B12 ST-WebAgentBench — 数据表格与分析

> 论文：ST-WebAgentBench: A Benchmark for Evaluating Safety and Trustworthiness in Web Agents（ICLR 2026, IBM Research）  
> 表格：[analysis/tables](../B12-st-webagentbench/analysis/tables/)

## 1. 数据集结构

`data_overview.csv`：375 个任务、3,057 条策略实例（平均每任务 8.15 条）、11 种策略模板。按站点：GitLab 197、SuiteCRM 170（含 General/Easy/Medium/Hard 与视觉/DOM 对抗子集）、ShoppingAdmin 8。

`data_policy_category_x_site.csv`（我从 test.csv 统计）与论文 Table 2 的“Total # Policies”行**完全一致**：

| 策略维度 | GitLab | ShoppingAdmin | SuiteCRM | 合计 |
| --- | --- | --- | --- | --- |
| 边界与范围限制 | 694 | 17 | 409 | 1,120 |
| 严格执行 | 551 | 17 | 391 | 959 |
| 鲁棒性与安全 | 67 | 2 | 317 | 386 |
| 用户同意 | 120 | 23 | 179 | 322 |
| 层级遵循 | 63 | 0 | 89 | 152 |
| 错误处理 | 39 | 6 | 73 | 118 |
| 合计 | 1,534 | 65 | 1,458 | 3,057 |

- 策略来源（`data_policy_source.csv`）：组织层 2,300、用户层 700、任务层 57。“用户同意”和“错误处理”全部来自用户层，“层级遵循”全部来自组织层——这正是论文的“组织 > 用户 > 任务”三级策略层级设计。
- 策略负载（`data_policy_load_bins.csv`）：65.3% 的任务同时激活 >5 条策略，只有 19 个任务（5.1%）只有 1 条。

## 2. 主结果（Figure 2，pass@3）

| 智能体 | 完成率 CR | 策略合规完成率 CuP | 部分 CR | 部分 CuP | all-pass@3 |
| --- | --- | --- | --- | --- | --- |
| AWM | **33.8** | **20** | 46.9 | 23 | 5 |
| WorkArena Legacy | 26 | 15 | 37 | 18.7 | 3 |
| WebVoyager | 12.8 | 10.3 | 26.9 | 17.5 | 2 |

- 核心观点：**单看任务完成率会高估企业就绪度**。AWM 完成率最高，但 CuP 只有 20%，且有 37 次违反“用户同意”（风险比 0.44）——它的“经验学习”循环倾向于跳过询问用户这一步。
- 要求三次运行都成功且合规（all-pass@3）时只剩 2–5%，运行间稳定性很差。
- WebVoyager 的 CR 与 CuP 差距小，是因为它很少走到需要触发策略的步骤，而非更安全。
- 论文正文称 AWM “最高 PCR 为 46.9%”，对应图中 Partial CR。

## 3. 维度重要性与策略负载

- `paper_T3_dimension_ablation.csv`：全部维度下 CR 与 CuP 相关仅 0.48；去掉“严格执行”（+0.15）或“用户同意”（+0.13）后相关性提升最多，即这两个维度是“完成≠安全”的主要来源。
- 策略越多越难合规：CuP 从 1 条策略时的 18.2% 降到 >5 条时的 7.1%（Spearman ρ=−0.71），而原始完成率几乎不变（ρ=−0.14）；每多一个策略模板，风险比上升约 0.11。

## 4. 展示建议

CR vs CuP 分组柱 + 六维风险雷达（Figure 2 右图只有图形无数值）；数据集视图展示 6 维策略在三个站点的分布。
