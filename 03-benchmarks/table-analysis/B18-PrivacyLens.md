# B18 PrivacyLens — 数据表格与分析

> 论文：PrivacyLens: Evaluating Privacy Norm Awareness of Language Models in Action（NeurIPS 2024 D&B, Stanford）  
> 表格：[analysis/tables](../B18-privacylens/analysis/tables/)

## 1. 数据集结构

493 条“种子 → 情境故事 → 智能体轨迹”三级数据（`data_overview.csv`）。种子按情境完整性（CI）框架描述一次信息流：数据类型、数据主体、发送者、接收者、传输原则。

- 来源（`data_seed_source.csv`）：众包 337（68%）、隐私文献 87、法规 69。464 种不同的数据类型、286 种接收者描述，几乎每条都独特。
- 智能体最后一步动作（`data_final_action.csv`）：Messenger 发消息 243、Gmail 发邮件 174、Slack 43、Facebook 发帖 33——都是“对外发送”类动作，泄露即在这一步发生。
- 轨迹中涉及的工具包（`data_toolkits.csv`）：Notion 68%、Messenger 54%、Gmail 37%；平均每条轨迹执行 1.88 个前置动作、约 2,555 字符。
- 每条轨迹标注的敏感信息项数（`data_sensitive_items_per_case.csv`）：1–16 项，中位数 2 项。
- 扩展子集：ConfAIde 32 条、CultureBank 24 条（跨文化隐私规范）。

## 2. 主结果（Table 2）：“知道”和“做到”之间的差距

| 模型 | 轨迹级问答准确率 | 实际泄露率 LR | 加隐私提示后 LR | 有用性 |
| --- | --- | --- | --- | --- |
| Claude-3-Sonnet | **99.80** | 38.34 | 37.32 | 2.71 |
| Claude-3-Haiku | 98.99 | **38.95** | 38.95 | 2.75 |
| GPT-4 | 97.57 | 26.37 | 24.54 | 2.60 |
| Llama-3-70B | 94.32 | 36.51 | 39.15 | 2.53 |
| ChatGPT-3.5 | 64.10 | 36.31 | 30.43 | 2.63 |
| Llama-3-8B | 31.44 | **21.30** | 20.49 | 2.47 |
| zephyr-7b-beta | 60.45 | 24.14 | 19.27 | 1.85 |

- 核心发现：Claude-3-Sonnet 几乎所有“这样分享合适吗？”的问题都答对（99.8%），但真正执行任务时仍在 38% 的情况下泄露敏感信息。**问答式隐私评测会严重高估智能体的隐私保护能力**。
- 加入“隐私增强提示”效果有限：GPT-4 只从 26.37% 降到 24.54%，Llama-3-70B 反而升高。
- 泄露率最低的 Llama-3-8B 与 zephyr 同时有用性最低（zephyr 1.85/3），是“做不好任务所以没泄露”。LRh（只统计有用的动作）为此做了校正：zephyr 的 LRh 33.44% 明显高于 LR 24.14%。
- 弱模型从种子到轨迹的问答准确率大幅下降（Llama-3-8B 88.84% → 31.44%），说明长上下文中识别隐私规范本身也是难点。

## 3. 扩展实验

- `paper_T3_extended_seeds.csv`：10 个法规种子各扩展为 5 种情境（互惠披露、正当理由、亲密关系等），泄露率 10–30%，Mixtral 最高（30%）。
- `paper_T5_confaide_culturebank.csv`：ConfAIde 子集上 GPT-4 泄露 9.38%、Claude-3-Sonnet 21.88%；跨文化 CultureBank 子集上普遍更高（Mixtral 37.5%、Claude-3-Sonnet 33.33%），说明模型对非美国文化的隐私规范更不敏感。

## 4. 展示建议

“问答准确率 vs 实际泄露率”散点图最能说明问题；数据集视图展示 CI 五元组和对外发送动作的分布。
