# B24 MCP Security Bench (MSB) — 数据表格与分析

> 论文：MCP Security Bench (MSB): Benchmarking Attacks Against Model Context Protocol in LLM Agents（ICLR 2026）  
> 表格：[analysis/tables](../B24-mcp-security-bench/analysis/tables/)

## 1. 数据集结构

`data_overview.csv`：2,000 条攻击实例（case_manifest）、64 个不同用户任务（论文 65）、10 个场景智能体、33 个 MCP 工具规格文件。

`data_cases_attack_type.csv`（公开实例）：PI、FE、UI（simulated_user）以及 PI-UI、PI-FE 各 300 条；NC、PM、OP、TT、PM-OP、PM-UI 各 80 条；另有 search_term_deception 20 条（即 RI）。论文 Table 2：10 场景、65 任务、25 个 MCP 服务器、304 个良性工具、405 个攻击工具、6 个攻击任务、12 种攻击类型。

攻击类型按 MCP 流程阶段划分（`paper_T1_attack_types.csv`）：规划阶段（名称碰撞 NC、偏好操纵 PM、描述注入 PI）、调用阶段（越界参数 OP）、响应阶段（冒充用户 UI、伪造错误 FE、工具转移 TT、检索注入 RI），以及 7 种组合。

## 2. 主结果（Table 3，10 个模型 × 12 种攻击 ASR）

| 模型 | 平均 ASR | 最有效攻击 |
| --- | --- | --- |
| DeepSeek-V3.1 | **60.94%** | OP 92.50%、FE 85.25% |
| GPT-4o-mini | 58.56% | PI-UI / PI-FE 95.41% |
| Claude4 Sonnet | 52.51% | OP 93.75%、TT-OP 87.50% |
| Qwen3 8B | 47.23% | PM-OP 86.25% |
| Llama3.3 70B | 46.61% | OP 98.75% |
| GPT-5 | 37.17% | OP 98.75%、PM-OP 86.25% |
| Gemini 2.5 Flash | 30.26% | PI-FE 76.39% |
| Qwen3 30B | 27.14% | OP 62.50% |
| Llama3.1 70B | 23.37% | OP 58.75% |
| Llama3.1 8B | **19.74%** | OP 46.25% |
| 平均 | 40.35% | OP 76.50% |

- **越界参数攻击 OP 是最有效的单一攻击**（平均 76.5%）：恶意工具只需在参数里要求“LLM 模型名”之类的额外信息，模型几乎都会照填。它不含任何显式恶意指令，因此极难检测；且 OP 的 PUA 与 ASR 几乎相同，说明它不损害任务完成，非常隐蔽。
- 能力强的模型对描述注入 PI 和检索注入 RI 更脆弱：Claude4 Sonnet PI 66.89%、GPT-5 PI 48.85%，而 Llama3.1 只有 4.92%。
- GPT-5 对冒充用户和伪造错误几乎免疫（0.33%、1.31%），但对 OP 和 PM-OP 依然中招。

## 3. 效用与 NRP

`paper_T11/T12_*_full.csv` 给出每种攻击的 ASR、PUA（攻击下用户任务完成率）、NRP = PUA × (1 − ASR)。GPT-5 的平均 NRP 最高（52.99%），因为它在高完成率下保持中等抗攻击能力。UI/FE 类攻击下恶意工具没有正常功能，PUA 无意义，表中记为 “-”。

## 4. 防御 MCIP（Table 4）

平均 ASR 从 40.35% 降到 28.69%（−11.66），但 PUA 同时下降 7.59，NRP 仅 +1.18；GPT-5 的 NRP 甚至从 52.99% 降到 46.73%。检测拦截式防御会误拦正常调用（比如拦掉越界参数后导致参数缺失、调用失败）。

## 5. 其他

Qwen3 8B 开启思考模式后 ASR 反而升高 9.85 个点，PUA 升高 13.82 个点（Table 13）——推理让模型更会完成任务，也更会完成攻击者的任务。

## 6. 展示建议

10 模型 × 12 攻击热力图（Table 3），按 MCP 阶段（规划/调用/响应/组合）分组列。
