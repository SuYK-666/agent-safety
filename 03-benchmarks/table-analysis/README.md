# Benchmark 数据表格与分析 · 总索引

整理日期：2026-11-23。覆盖 39 个 benchmark（B15 信通院无公开数据与论文，按要求跳过），共生成 **516 张 CSV 表**。

## 目录约定

每个 benchmark 目录下新增 `analysis/tables/`，只保留最终表格：

| 文件 | 说明 |
| --- | --- |
| `analysis/tables/data_*.csv` | 由上游数据集**计算**得到的统计表 |
| `analysis/tables/paper_*.csv` | 从论文**逐格转录**的结果表；带 `F` 前缀的来自图（热力图格子有印刷数值的为精确值，柱/折线图标 `approx`） |
| `analysis/tables/derived_*.csv` | 由论文表二次计算（均值、分组汇总等） |
| `analysis/tables/results_*.csv` | 作者随仓库发布的结果文件（B20、B40） |

每张 paper/derived 表对应的论文表号、页码与口径说明见各分析文档。

## 逐项分析文档

| 编号 | 分析文档 | 数据表 | 论文表 | 数据集情况 |
| --- | --- | --- | --- | --- |
| B01 | [AgentDojo](B01-AgentDojo.md) | 5 | 6 | 完整 |
| B02 | [InjecAgent](B02-InjecAgent.md) | 9 | 11 | 完整 |
| B03 | [Agent Security Bench](B03-AgentSecurityBench.md) | 6 | 14 | 完整 |
| B04 | [Agent Red Teaming](B04-AgentRedTeaming.md) | 0 | 6 | 无公开数据 |
| B05 | [AgentDyn](B05-AgentDyn.md) | 5 | 10 | 完整 |
| B06 | [SafeClawBench](B06-SafeClawBench.md) | 10 | 28 | 完整 |
| B07 | [AgentHarm](B07-AgentHarm.md) | 5 | 8 | 部分公开（8/11 类） |
| B08 | [Agent-SafetyBench](B08-AgentSafetyBench.md) | 7 | 4 | 完整 |
| B09 | [ToolEmu](B09-ToolEmu.md) | 6 | 11 | 完整 |
| B10 | [WASP](B10-WASP.md) | 4 | 4 | 完整 |
| B11 | [SafeArena](B11-SafeArena.md) | 0 | 8 | Gated 未下载 |
| B12 | [ST-WebAgentBench](B12-ST-WebAgentBench.md) | 7 | 4 | 完整 |
| B13 | [OS-Harm](B13-OS-Harm.md) | 5 | 11 | 完整 |
| B14 | [MMA-SafetyBench](B14-MMA-SafetyBench.md) | 8 | 7 | GUI+文档 2/5 领域 |
| B16 | [AuthorizationBench](B16-AuthorizationBench.md) | 8 | 11 | 完整 |
| B17 | [AuthGateBench](B17-AuthGateBench.md) | 5 | 7 | 完整 |
| B18 | [PrivacyLens](B18-PrivacyLens.md) | 6 | 4 | 完整 |
| B19 | [CI-Work](B19-CI-Work.md) | 5 | 5 | 完整 |
| B20 | [AgentLeak](B20-AgentLeak.md) | 11 | 18 | 完整 + 作者结果 |
| B21 | [MemSecBench](B21-MemSecBench.md) | 0 | 9 | 无公开数据 |
| B22 | [ATBench](B22-ATBench.md) | 7 | 3 | 完整 |
| B23 | [MCPSecBench](B23-MCPSecBench.md) | 3 | 2 | 用例 + 早期运行记录 |
| B24 | [MCP Security Bench](B24-MCP-Security-Bench.md) | 5 | 7 | 完整 |
| B25 | [MCP 运行时不变量 HCP](B25-MCP-Runtime-Invariants-HCP.md) | 0 | 9 | 无公开数据 |
| B26 | [MADBench](B26-MADBench.md) | 0 | 7 | 无公开数据 |
| B27 | [DUMA-Bench](B27-DUMA-Bench.md) | 3 | 6 | 完整 |
| B28 | [R-Judge](B28-R-Judge.md) | 4 | 7 | 完整 |
| B29 | [Cybench](B29-Cybench.md) | 6 | 10 | 元数据（31/40 题） |
| B30 | [CVE-Bench](B30-CVE-Bench.md) | 3 | 9 | 元数据 |
| B31 | [CyberSecEval 2](B31-CyberSecEval-2.md) | 12 | 7 | 完整 |
| B32 | [CyberSecEval 3](B32-CyberSecEval-3.md) | 8 | 13 | 完整 |
| B33 | [SEC-bench](B33-SEC-bench.md) | 6 | 6 | 完整 |
| B34 | [CyberSOCEval](B34-CyberSOCEval.md) | 10 | 6 | 完整 |
| B35 | [Cyber Defense Benchmark](B35-Cyber-Defense-Benchmark.md) | 5 | 5 | 1 个样例活动 |
| B36 | [SOCBench Detection](B36-SOCBench-Detection.md) | 7 | 0 | 完整（无论文） |
| B37 | [BFCL v4](B37-BFCL-v4.md) | 3 | 3 | 完整 |
| B38 | [τ²-Bench](B38-tau2-Bench.md) | 5 | 7 | 完整 |
| B39 | [OSWorld](B39-OSWorld.md) | 5 | 4 | 完整 |
| B40 | [METR Time Horizons](B40-METR-Time-Horizons.md) | 8 | 7 | 运行记录 + 官方结果 |

（论文表一列含 derived/results 表。）

## 校验结论与需要注意的口径差异

数据集统计与论文数字逐项对上的例子：AgentDojo 97/27/629、InjecAgent 1,054、AgentDyn 560、ST-WebAgentBench 六维策略 3,057、AuthorizationBench 领域与伤害分布、SafeClawBench 8 类 oracle 计数、CyberSecEval 2 各子集规模等。

发现的不一致（已在对应 md 中说明）：

- AgentHarm 公开版只有 176 条有害行为、8 个类别（论文 264 条、11 类）。
- MCPSecBench 仓库的 experiments.csv 与论文 Table 1 数值不同，应以论文为准。
- Cyber Defense Benchmark 仓库 cost.json 中 Opus 4.7 成本与论文不一致。
- AgentDojo 论文 Table 1 工具数合计 74 而非正文的 70；InjecAgent 正文对微调 GPT 的数字顺序与表相反；ASB 混合攻击正文 84.03% vs 表 84.30%。
- OSWorld、τ²-Bench、R-Judge、Cybench 等上游数据版本与论文有个别任务数差异（修订或下线）。

## 展示系统使用建议

- 排行榜类：优先用 `paper_*` 中“模型 × 指标”的主表（如 B03 T5、B05 全矩阵、B08 T5、B14 T2、B20 T15、B24 T3、B37 T1）。
- 注意区分**安全基准**（B01–B28）、**网络安全攻防能力**（B29–B35）和**通用能力/可靠性参照**（B36–B40），不要混在同一个排名里。
- 大部分安全基准都显示“低 ASR 可能源于能力不足”，建议所有安全指标与对应的效用/完成率并列展示。
