# B23 MCPSecBench — 数据表格与分析

> 论文：MCPSecBench: A Systematic Security Benchmark and Playground for Testing Model Context Protocols  
> 表格：[analysis/tables](../B23-mcpsecbench/analysis/tables/)

## 1. 数据与口径说明

MCPSecBench 本质是一个可运行的攻防靶场：17 类攻击 × 4 个攻击面（客户端、协议、服务端、宿主），在 3 个 MCP 平台（Claude Desktop、OpenAI、Cursor）上每格跑 15 次。本包只收录了用例定义（`data.json`，11 条攻击提示）和仓库里的 `experiments.csv`（每个平台 15 次运行 × 17 类攻击的成功/失败记录）。

**注意**：`experiments.csv` 统计出的结果（`data_experiments_asr_by_provider_attack.csv`）与论文 Table 1 的“无防御”列并不完全一致。例如 Claude Desktop 的 Tool Shadowing 在 CSV 中 15/15 成功，论文为 20%；Indirect Prompt Injection CSV 为 100%，论文为 33.3%。这个 CSV 应是早期版本的实验记录，展示系统应以论文 Table 1 为准，CSV 仅作为“原始运行记录格式”的参考。

## 2. 主结果（Table 1，ASR 与拒绝率 RR）

按攻击面平均（无防御）：

| 攻击面 | Claude Desktop ASR | OpenAI ASR | Cursor ASR |
| --- | --- | --- | --- |
| 客户端（ATT-1~4） | 33.3% | 66.7% | **80%** |
| 协议（ATT-5~6：重绑定、中间人） | 100% | 100% | 100% |
| 服务端（ATT-7~13） | 78.1% | 75.2% | 75.2% |
| 宿主（ATT-14~17） | 58.3% | 75% | **81.7%** |

- 协议层攻击（MCP 重绑定、中间人）和部分服务端攻击（工具投毒、包名抢注）对所有平台都 100% 成功——这些是结构性漏洞，模型本身无法拒绝。
- Claude Desktop 对直接提示注入（ATT-1）和“困惑代理”工具误用（ATT-2）完全拒绝，而 Cursor 对 ATT-1 100% 中招。论文结论：Cursor 攻击面最广、原生检测最弱，Claude Desktop 最稳健。
- 工具投毒（ATT-12）在三个平台、三种防御配置下几乎都是 100%。

## 3. 防御（MCIP、FAN）

- `paper_T2_defense_protection.csv`：MCIP 和 FAN 对间接注入防护最好（55.6% / 64.4%），对工具影子、包名抢注、Rug Pull、工具投毒基本无效（2–13%）。
- 防御效果依赖平台：MCIP 在 Claude Desktop 上把数据外泄 ASR 从 100% 降到 0%，在 Cursor 和 OpenAI 上几乎无效。
- 论文 Table 4（token 与成本）显示 MCIP 在 Cursor 上把 token 消耗放大约 10 倍（如 ATT-1 从 24.6k 到 271.1k）。

## 4. 展示建议

17 类攻击 × 3 平台 × 3 防御的 ASR 热力图（Table 1），按攻击面分组；突出“协议层 100%”这一结构性问题。
