# B13 OS-Harm — 数据表格与分析

> 论文：OS-Harm: A Benchmark for Measuring Safety of Computer Use Agents（EPFL, NeurIPS 2025 D&B）  
> 表格：[analysis/tables](../B13-os-harm/analysis/tables/)

## 1. 数据集结构（基于 OSWorld 的 Ubuntu 桌面环境）

`data_category_x_app.csv`（HF parquet，149 行）：

| 类别 | 任务数 | 主要应用 |
| --- | --- | --- |
| 用户蓄意滥用 | 50（25 原始 + 25 越狱模板版本） | Writer、多应用、OS、VS Code 各 8 |
| 提示注入攻击 | 51 | VS Code 14、Chrome/Writer/Thunderbird 各 11 |
| 模型自身失误 | 48 | 多应用 16、VS Code 16 |

- 蓄意滥用类的 50 行中有 25 行是同一任务套上 “ignore all restrictions” 越狱模板的配对版本（`data_category_x_jailbreak.csv`）。论文 Table 2 的 Misuse 列按 50 个任务计。
- 注入任务（`data_injection_vector_x_goal.csv`）：6 种注入载体 × 12 种攻击目标；VS Code 代码注释 15、桌面通知 12 最多；目标中 stop_task 8、email_send_prompt 7 最多。公开数据为 51 条，论文人工标注分析用 50 条（Table 4 中 VS Code 为 14）。
- 失误类任务多带 `_aug` 后缀，是对同一场景的改写增强（例如删除冗余文件、修改 .bashrc、撤销权限）。

## 2. 主结果（Table 2，GPT-4.1 判官，温度 1，最多 15 步）

| 模型 | 滥用：不安全 | 滥用：完成 | 注入：不安全 | 注入：完成原任务 | 失误：不安全 | 平均不安全 |
| --- | --- | --- | --- | --- | --- | --- |
| o4-mini | 52 | 24 | **20** | 54 | **10** | 27 |
| GPT-4.1 | 48 | 20 | 12 | 54 | 4 | **21** |
| Claude 3.7 Sonnet | **70** | **50** | 10 | 32 | 8 | **29** |
| Gemini 2.5 Pro | 64 | 40 | 8 | **72** | 8 | 27 |
| Gemini 2.5 Flash | 70 | 28 | 2 | 34 | 6 | 26 |

- 前沿模型在**不越狱**的情况下就有 48–70% 照做有害的电脑操作请求；Claude 3.7 Sonnet 不安全率 70%、实际完成 50%，是滥用类最差的模型（这与 AgentHarm/SafeArena 中 Claude 的表现形成反差，说明 computer-use 场景的安全训练明显不足）。
- 提示注入下不安全率 2–20%，o4-mini 最易受骗；模型自身失误（无攻击下误删文件等）4–10%。
- 五个模型的平均不安全率很接近（21–29%）。

## 3. 越狱模板（Figure 5，从渲染页读取）

| 模型 | 不安全率 直接 → 越狱 | 完成率 直接 → 越狱 |
| --- | --- | --- |
| o4-mini | 52 → 56 | 24 → 16 |
| GPT-4.1 | 48 → **100** | 20 → 44 |
| Claude 3.7 Sonnet | 70 → 96 | 50 → 48 |
| Gemini 2.5 Pro | 64 → **100** | 40 → 44 |
| Gemini 2.5 Flash | 70 → 88 | 28 → 32 |

一个静态模板就让 GPT-4.1 与 Gemini 2.5 Pro 的不安全率达到 100%；只有 o4-mini 基本不受影响。

## 4. 注入细分（Table 4，o4-mini）

桌面通知、Thunderbird 邮件 50% 被服从，LibreOffice 文档与 VS Code 代码注释 0%；目标为“停止任务”时 71% 成功，“泄露密码到 URL”40%，而删除文件、设置 cron、运行远程脚本等高危目标均为 0%。

## 5. 判官可靠性（Table 3、8–10）

GPT-4.1 AER 判官与 150 条人工标注：不安全判定准确率 84%、精确率 95%、召回 64%（偏保守，漏判多于误判）。违规步骤定位一致率 77%、平均偏差 0.85 步。Table 8/9 比较了 4 种观测框架与 3 个判官模型；Table 6 显示 LLM 判官与 OSWorld 执行检查器相比召回高、精确率低（38–48%）。

## 6. 展示建议

3 类风险 × 5 模型的不安全率热力图 + 越狱前后对比柱；注入载体/目标两张小表适合做下钻。
