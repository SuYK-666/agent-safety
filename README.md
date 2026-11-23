# 智能体安全测评资料包

> 当前快照：**2026-11-23**  
> 资料范围：4 份治理/评测框架、1 份研究报告、40 项 benchmark、38 篇论文全文、39 项基准的 516 张结构化数据表，以及 OWASP ASI 风险映射和模型—数据表索引。  
> 适用场景：智能体安全研究、评测选型、风险归类、论文复现准备、模型横向对比和数据集审阅。

## 1. 这个资料包回答什么问题

这个目录不是简单的论文合集，而是一套围绕“**智能体委托、动作、提交与后果**”组织的证据包。它主要回答五类问题：

1. **风险是什么**：用 OWASP Agentic Top 10（ASI01–ASI10）定位目标劫持、工具滥用、权限滥用、供应链、代码执行、记忆投毒、智能体间通信、级联故障、信任利用和失控。
2. **监管和治理如何落位**：用全国网安标委治理框架 3.0、工信部 AIIA 评测框架和 NIST SP 2400 草案，把技术风险对应到生命周期、责任主体和评测流程。
3. **现有 benchmark 测什么**：40 项基准覆盖工具调用、Web/OS 操作、多智能体、MCP、隐私、权限、网络安全和长任务自主性。
4. **每张表实际在说什么**：516 张 `analysis/tables/*.csv` 统一了数据统计、论文结果转录和二次计算；表名和数据口径在各基准分析文档中说明。
5. **某个模型出现在哪里**：`Model-table-index.md` 按模型系列和具体型号整理其出现的结果表；`OWASP-ASI-01-10-table-map.md` 则按 ASI 类别反查基准和数据表。

## 2. 最新状态（2026-11-23）

| 资产 | 当前数量/状态 | 入口 |
| --- | --- | --- |
| 研究报告 | 1 份，含 3 张图 | [报告](01-report/agent-safety-research.md) · [图目录](01-report/figures/) |
| 治理/评测框架原文 | 4 份 PDF | [框架说明](02-frameworks/README.md) |
| benchmark | 40 项（B01–B40） | [逐项总表](03-benchmarks/README.md) |
| 论文全文 | 38 篇；B15、B36 无对应论文 | 各基准 `paper/` |
| 结构化数据表 | 39 项基准共 516 张；B15 无数据表 | [表格总索引](03-benchmarks/table-analysis/README.md) |
| 逐基准表分析 | 39 份 Markdown | [table-analysis](03-benchmarks/table-analysis/README.md) |
| ASI 风险映射 | ASI01–ASI10 全量映射 | [OWASP ASI 表映射](03-benchmarks/OWASP-ASI-01-10-table-map.md) |
| 模型索引 | 按模型系列/型号反查结果表 | [Model-table-index](03-benchmarks/Model-table-index.md) |
| 上游原文件 | 约 10,300 个文件、约 1.7 GB | 各基准 `data/upstream*/` |
| 索引/校验 | 基准目录、逐文件清单、SHA-256 | [03-benchmarks/file-manifest.csv](03-benchmarks/file-manifest.csv) · [04-indexes/SHA256SUMS.txt](04-indexes/SHA256SUMS.txt) |

### 2.1 本次新增的重点

- 39 项可分析基准已经整理出 **516 张 CSV 表**，分为数据统计表、论文表和二次计算表。
- 每项基准都有独立的表分析文档，记录论文表号、页数、样本口径和已知差异。
- `OWASP-ASI-01-10-table-map.md` 逐表归入 ASI01–ASI10；同一张表允许有多个标签。
- `Model-table-index.md` 按 OpenAI、Anthropic、Google、Meta、DeepSeek、Qwen、Mistral、Kimi、GLM、MiniMax 等系列整理型号，并单独展开 B37 的 69 个配置和 B40 的 v1.0/v1.1。

## 3. 快速入口

| 我想…… | 先看 |
| --- | --- |
| 快速了解智能体安全的整体风险 | [研究报告](01-report/agent-safety-research.md) |
| 找某个基准的论文、数据和任务设置 | [03-benchmarks/README.md](03-benchmarks/README.md) |
| 查某张表的列名、来源和口径 | [table-analysis/README.md](03-benchmarks/table-analysis/README.md) |
| 按 OWASP ASI 风险查表 | [OWASP-ASI-01-10-table-map.md](03-benchmarks/OWASP-ASI-01-10-table-map.md) |
| 查某个模型出现在哪些表 | [Model-table-index.md](03-benchmarks/Model-table-index.md) |
| 找治理框架的原文和发布入口 | [02-frameworks/README.md](02-frameworks/README.md) |
| 核对文件来源、许可和哈希 | [03-benchmarks/file-manifest.csv](03-benchmarks/file-manifest.csv) · [04-indexes/file-manifest.csv](04-indexes/file-manifest.csv) |
| 看标准清单和监管资料 | [04-indexes/standards-catalog.csv](04-indexes/standards-catalog.csv) |

## 4. 目录结构

```text
agent-safety/
├─ README.md
├─ 01-report/
│  ├─ agent-safety-research.md          # 主研究报告
│  └─ figures/                          # 3 张报告插图
├─ 02-frameworks/
│  ├─ README.md
│  ├─ 01-owasp-agentic-top-10-2026.pdf
│  ├─ 02-tc260-ai-safety-governance-framework-3.0.pdf
│  ├─ 03-aiia-industry-ai-safety-evaluation-framework-2026.pdf
│  └─ 04-nist-sp-2400-102e2026-initial-public-draft.pdf
├─ 03-benchmarks/
│  ├─ README.md                         # 40 项基准总表（最新归档口径）
│  ├─ archive-index.csv                 # 每项基准的收录范围、来源、入口
│  ├─ file-manifest.csv                 # 逐文件来源、许可、页数、哈希
│  ├─ table-analysis/                   # 39 份表分析 + 总索引
│  │  ├─ README.md
│  │  ├─ B01-AgentDojo.md
│  │  └─ ... B40
│  ├─ OWASP-ASI-01-10-table-map.md      # 表 → ASI 风险映射
│  ├─ Model-table-index.md              # 模型 → 数据表索引
│  └─ B01-agentdojo ... B40-metr-time-horizons/
│     ├─ README.md
│     ├─ paper/                         # 论文 PDF（若有）
│     ├─ data/                          # 提取视图/上游原文件
│     ├─ results/                       # 作者结果或整理结果（若有）
│     └─ analysis/tables/               # 516 张 CSV 表
└─ 04-indexes/
   ├─ benchmark-catalog.csv             # 旧版 benchmark 综合目录
   ├─ standards-catalog.csv             # 标准与监管资料索引
   ├─ coverage-summary.json             # 旧版覆盖摘要
   ├─ risk-evidence-rows.csv            # 风险—证据映射行
   ├─ file-manifest.csv                 # 旧版逐文件清单
   └─ SHA256SUMS.txt                    # 归档校验
```

> 重要：`03-benchmarks/README.md`、`03-benchmarks/archive-index.csv` 和 `03-benchmarks/file-manifest.csv` 反映本次基准补档后的最新口径。`04-indexes/` 是 2026-11-19 版静态索引，部分“归档状态”和“文件计数”早于最新补档；两者不要直接相加，冲突时以 `03-benchmarks/` 内的最新文件为准。

## 5. 40 项 benchmark 总目录

“表数”是 `analysis/tables/*.csv` 的实际数量；论文、上游原始数据和外部工具是不同层，不能用表数代替样本量。

### 5.1 工具调用、注入与运行时安全（B01–B06）

| 编号 | 基准 | 主要测什么 | 表数 | 资料状态 |
| --- | --- | --- | ---: | --- |
| B01 | [AgentDojo](03-benchmarks/B01-agentdojo/README.md) | 工作区、Slack、出行、银行场景中的间接提示注入与防御；同时看正常效用、受攻击效用和定向 ASR | 11 | 公开测试集完整 |
| B02 | [InjecAgent](03-benchmarks/B02-injecagent/README.md) | 工具集成智能体的间接提示注入；区分数据窃取与直接伤害，含 17 种用户工具、62 种攻击者工具 | 20 | 公开测试集完整 |
| B03 | [Agent Security Bench (ASB)](03-benchmarks/B03-agent-security-bench/README.md) | 10 个应用场景、10 个智能体、400 余工具；DPI、IPI、记忆投毒、PoT、混合攻击及防御 | 20 | 公开测试集完整 |
| B04 | [Agent Red Teaming (ART)](03-benchmarks/B04-agent-red-teaming/README.md) | 大规模公开红队竞赛；22 个模型、约 180 万次提交、跨模型攻击迁移 | 6 | 无公开测试集；有论文和结果表 |
| B05 | [AgentDyn](03-benchmarks/B05-agentdyn/README.md) | 动态长任务环境中的注入与防御可用性；购物、GitHub、日常任务 | 15 | 公开测试集完整 |
| B06 | [SafeClawBench](03-benchmarks/B06-safeclawbench/README.md) | 语义 CoreFail、审计证据 HarmEvidence、沙盒 ObservedHarm 三层终点；6 类 600 条攻击 | 38 | 公开测试集完整 |

### 5.2 行为安全、隐私、权限与长轨迹（B07–B22）

| 编号 | 基准 | 主要测什么 | 表数 | 资料状态 |
| --- | --- | --- | ---: | --- |
| B07 | [AgentHarm](03-benchmarks/B07-agentharm/README.md) | 工具型智能体执行有害任务；拒绝、部分完成、完成与良性对照 | 13 | 作者部分发布（公开版 8 类/176 条） |
| B08 | [Agent-SafetyBench](03-benchmarks/B08-agent-safetybench/README.md) | 8 类风险、10 类失效模式；2,000 用例、349 个交互环境 | 11 | 公开测试集完整 |
| B09 | [ToolEmu](03-benchmarks/B09-toolemu/README.md) | LM 模拟工具沙盒；识别工具风险、任务质量与 NoAct 基线 | 17 | 公开测试集完整 |
| B10 | [WASP](03-benchmarks/B10-wasp/README.md) | Web 智能体提示注入；中间 ASR 与端到端任务完成 | 8 | 公开测试集完整 |
| B11 | [SafeArena](03-benchmarks/B11-safearena/README.md) | Web 智能体有害任务完成、拒绝和正常任务过度拒绝 | 8 | 上游 gated，未下载原始任务 |
| B12 | [ST-WebAgentBench](03-benchmarks/B12-st-webagentbench/README.md) | 企业 Web 智能体的策略合规、用户同意、权限和鲁棒性 | 11 | 公开测试集完整 |
| B13 | [OS-Harm](03-benchmarks/B13-os-harm/README.md) | 电脑使用智能体：用户滥用、提示注入、模型失误、越狱 | 16 | 公开测试集完整 |
| B14 | [MMA-SafetyBench](03-benchmarks/B14-mma-safetybench/README.md) | 多模态 GUI/文档视觉语义劫持、伪造界面和跨域覆盖 | 15 | 本地整理 GUI+文档两域 |
| B15 | [CAICT AI Safety Benchmark 2026 Q1](03-benchmarks/B15-caict-ai-safety-benchmark-2026q1/README.md) | 信通院季度安全基准；本包只保留说明性材料 | 0 | 无数据表、无论文 |
| B16 | [AuthorizationBench](03-benchmarks/B16-authorizationbench/README.md) | 委托授权边界、越权完成（OAR）、良性压力和恶意注入 | 19 | 公开测试集完整 |
| B17 | [AuthGateBench](03-benchmarks/B17-authgatebench/README.md) | 把 LLM 当审批门时的误拦/漏放、策略显隐式和动作锚定 | 12 | 公开测试集完整 |
| B18 | [PrivacyLens](03-benchmarks/B18-privacylens/README.md) | 隐私规范“知道但做不到”；问答准确率与实际泄露率差距 | 10 | 公开测试集完整 |
| B19 | [CI-Work](03-benchmarks/B19-ci-work/README.md) | 企业上下文完整性；上行/下行/平级/对外信息流与用户施压 | 10 | 公开测试集完整 |
| B20 | [AgentLeak](03-benchmarks/B20-agentleak/README.md) | 多智能体内部通道泄露；C1 输出、C2 智能体间、C5 共享记忆等 | 29 | 公开测试集完整 + 作者结果 |
| B21 | [MemSecBench](03-benchmarks/B21-memsecbench/README.md) | 记忆安全全生命周期；2 框架 × 4 记忆后端 × 3 LLM | 9 | 无公开测试集；有论文表 |
| B22 | [ATBench](03-benchmarks/B22-atbench/README.md) | 1,000 条长轨迹安全风险；来源、伤害、失效模式与判官 | 10 | 公开测试集完整 |

### 5.3 MCP、多智能体与通信边界（B23–B28）

| 编号 | 基准 | 主要测什么 | 表数 | 资料状态 |
| --- | --- | --- | ---: | --- |
| B23 | [MCPSecBench](03-benchmarks/B23-mcpsecbench/README.md) | MCP 客户端、协议、服务端、宿主四攻击面；17 类攻击 | 5 | 用例 + 早期运行记录 |
| B24 | [MCP Security Bench (MSB)](03-benchmarks/B24-mcp-security-bench/README.md) | MCP 规划、调用、响应阶段攻击；单攻击与混合攻击 | 12 | 公开测试集完整 |
| B25 | [MCP 运行时不变量 (HCP)](03-benchmarks/B25-mcp-runtime-invariants-hcp/README.md) | 连接控制、授权匹配、句柄归属、审计、密封发布等运行时不变量 | 9 | 无公开测试集；有论文表 |
| B26 | [MADBench](03-benchmarks/B26-madbench/README.md) | 多智能体辩论的安全放大；成员、编排者、轮数与成本 | 7 | 无公开测试集；有论文表 |
| B27 | [DUMA-Bench](03-benchmarks/B27-duma-bench/README.md) | 双控多智能体；用户施压、协作者投毒、身份冒充、工具影子 | 9 | 公开测试集完整 |
| B28 | [R-Judge](03-benchmarks/B28-r-judge/README.md) | 轨迹级安全风险判官；风险识别、类别 F1 与人工一致性 | 11 | 公开测试集完整 |

### 5.4 网络安全攻防能力（B29–B35）

| 编号 | 基准 | 主要测什么 | 表数 | 资料状态 |
| --- | --- | --- | ---: | --- |
| B29 | [Cybench](03-benchmarks/B29-cybench/README.md) | CTF 任务；密码、Web、逆向、取证、Pwn 与子任务得分 | 16 | 公开元数据（31/40 题可核） |
| B30 | [CVE-Bench](03-benchmarks/B30-cve-bench/README.md) | 真实 Web CVE 的自主利用；zero-day/one-day、攻击类型与成本 | 12 | 公开元数据 |
| B31 | [CyberSecEval 2](03-benchmarks/B31-cyberseceval-2/README.md) | 不安全代码、提示注入、解释器滥用、ATT&CK 服从、漏洞利用、误拒 | 19 | 公开测试集完整 |
| B32 | [CyberSecEval 3](03-benchmarks/B32-cyberseceval-3/README.md) | 自动修补、鱼叉钓鱼、解释器滥用、自主渗透、护栏增强 | 21 | 公开测试集完整 |
| B33 | [SEC-bench](03-benchmarks/B33-sec-bench/README.md) | 真实 C/C++ 项目的漏洞修复与 PoC；SWE-agent/OpenHands/Aider | 12 | 公开测试集完整 |
| B34 | [CyberSOCEval](03-benchmarks/B34-cybersoceval/README.md) | 恶意软件分析与威胁情报推理；按家族、主题、难度和来源 | 16 | 公开测试集完整 |
| B35 | [Cyber Defense Benchmark](03-benchmarks/B35-cyber-defense-benchmark/README.md) | 威胁狩猎智能体；活动覆盖分、ATT&CK 战术召回与成本 | 10 | 公开样例集 |

### 5.5 通用能力、可靠性与长任务自主性（B36–B40）

| 编号 | 基准 | 主要测什么 | 表数 | 资料状态 |
| --- | --- | --- | ---: | --- |
| B36 | [SOCBench (Detection)](03-benchmarks/B36-socbench-detection/README.md) | 网络流检测数据集；攻击类型、协议、端口与采样 | 7 | 公开测试集完整；无对应论文 |
| B37 | [BFCL v4](03-benchmarks/B37-bfcl-v4/README.md) | 函数调用、多轮、无关函数拒调、长上下文、Web Search、Memory、SQL | 6 | 公开测试集完整；T1 含 69 个配置 |
| B38 | [τ²-Bench](03-benchmarks/B38-tau2-bench/README.md) | 双控对话智能体；用户协作、pass^k、telecom 模式 | 12 | 公开测试集完整 |
| B39 | [OSWorld](03-benchmarks/B39-osworld/README.md) | 真实桌面环境开放任务；12 模型、应用/类别成功率与人类基线 | 9 | 公开测试集完整 |
| B40 | [METR Time Horizons](03-benchmarks/B40-metr-time-horizons/README.md) | 长软件任务的时间跨度、成功率随任务时长衰减、v1.0/v1.1 | 15 | 公开结果数据 |

### 5.6 表数核对

516 = 11 + 20 + 20 + 6 + 15 + 38 + 13 + 11 + 17 + 8 + 8 + 11 + 16 + 15 + 0 + 19 + 12 + 10 + 10 + 29 + 9 + 10 + 5 + 12 + 9 + 7 + 9 + 11 + 16 + 12 + 19 + 21 + 12 + 16 + 10 + 7 + 6 + 12 + 9 + 15。

## 6. 516 张数据表怎么组织

每项基准的 `analysis/tables/` 只放最终 CSV，不把上游原始目录和临时脚本混在一起。表名前缀表示证据来源：

| 前缀 | 含义 | 使用注意 |
| --- | --- | --- |
| `data_*` | 由上游数据集计算得到的统计表 | 用于看任务构成、攻击类型、场景分布和标签规模，不等于模型成绩 |
| `paper_*` | 从论文表格/图逐格转录的结果表 | `T` 通常代表论文 Table，`F` 代表 Figure；图中无印刷数值时可能标 `approx` |
| `derived_*` | 对论文表二次计算的均值、分组、汇总 | 便于做排行榜，但必须回到母表核对分母和模型面板 |
| `results_*` | 作者随仓库发布的结果文件 | B20、B40 等；字段命名可能与 `paper_*` 不同 |

每张表在 `table-analysis/Bxx-*.md` 中有：

- 对应论文表号、页码或图号；
- 列/行含义；
- 样本量、模型数或攻击类型数；
- 与正文数字的差异；
- 是否只是论文图的近似读取；
- 适合用于展示还是只适合做数据审计。

## 7. 两份跨基准索引

### 7.1 ASI 风险映射

[`OWASP-ASI-01-10-table-map.md`](03-benchmarks/OWASP-ASI-01-10-table-map.md) 的结构：

- 先给每个基准的“主要 ASI”总览；
- ASI01–ASI10 各自按基准列出相关数据表；
- 每张表附一句风险机制说明；
- 同一张表可重复出现在多个 ASI 下；
- 末尾附覆盖说明和表数口径。

归类原则不是看论文标题，而是看“这张表实际测什么/记录什么”。例如，同一张 MCP 工具调用表可能同时属于工具滥用、权限边界和供应链；同一张多智能体记忆表可能同时属于 ASI06 与 ASI07。

### 7.2 模型—表索引

[`Model-table-index.md`](03-benchmarks/Model-table-index.md) 的结构：

- 先列每个 benchmark 中有模型结果的数据表；
- 按 OpenAI、Anthropic、Google、Meta、DeepSeek、Qwen、Mistral、Kimi、GLM、MiniMax、其他开源模型分系列；
- 每个型号列出其出现的 benchmark 和具体表名；
- 单独展开 B37 的 69 个 Prompt/FC 配置；
- 单独展开 B40 的 v1.0/v1.1 运行标签；
- 末尾收录智能体框架、护栏模型、NoAct/Random/Human 等基线。

该索引只覆盖“有明确模型结果”的表，不从 `data_*` 纯数据表反推模型；同一模型的不同论文拼写会合并，但没有证据时不会把不同参数规模硬合并。

## 8. 证据层次与数据覆盖

### 8.1 四层证据

| 层级 | 内容 | 用途 |
| --- | --- | --- |
| 标准/治理层 | 四份框架 PDF | 说明风险类别、生命周期、责任和评测流程 |
| 论文层 | 38 篇全文 PDF | 核对方法、表格、附录、样本和作者结论 |
| 数据层 | `data/upstream*/` 和 `data/` | 查看上游原始字节、任务文件和提取视图 |
| 分析层 | `analysis/tables/*.csv` 与 `table-analysis/*.md` | 做检索、比较、制图和复现准备 |

### 8.2 当前测试集覆盖

- **29 项**：上游公开测试集完整收录。
- **5 项**：部分、元数据或公开结果——B07 AgentHarm、B29 Cybench、B30 CVE-Bench、B35 Cyber Defense Benchmark、B40 METR。
- **1 项**：上游访问受限——B11 SafeArena（gated）。
- **5 项**：本包未取得公开测试集——B04、B15、B21、B25、B26。

### 8.3 论文覆盖

- 40 项中 **38 项**有论文全文 PDF。
- **B15** 信通院 AI Safety Benchmark 2026 Q1：本包只有说明性材料，无论文、无数据表。
- **B36** SOCBench (Detection)：有公开数据，但经核查无对应论文。

### 8.4 上游文件与旧索引口径

- `03-benchmarks/README.md` 记录本次补档后的上游原文件约 **10,300 个、1.7 GB**，位于各基准 `data/upstream*/`，并尽量保持上游目录结构和原始字节。
- `04-indexes/coverage-summary.json` 记录的是旧版整理视图：**12 项有数据、443 个 data/metadata 文件**。这不是当前上游总文件数，也不应与 10,300 直接相加。
- 需要当前逐文件来源时，优先使用 [`03-benchmarks/file-manifest.csv`](03-benchmarks/file-manifest.csv)；需要旧版概览时再用 `04-indexes/`。

## 9. 推荐阅读顺序

1. **先读报告摘要和风险图谱**：`01-report/agent-safety-research.md` 第 1–3 节，理解“尝试、拒绝、提交、后果、恢复”的区别。
2. **再选一个风险问题**：例如目标劫持看 B01/B02/B05/B10；权限看 B16/B17；隐私看 B18/B19/B20；MCP 看 B23/B24/B25；多智能体看 B20/B26/B27。
3. **打开对应基准 README**：先看任务、样本、模型和限制，再看论文。
4. **用 `analysis/tables/` 做筛选**：论文表用于正式引用，`derived_*` 只用于辅助比较。
5. **用 ASI 映射和模型索引做横向检索**：确认同一张表是否跨类别，以及某个模型是否真的在同一模型面板中。

## 10. 使用和比较时的注意事项

- **不要跨基准直接排名**：不同基准的任务、模型面板、分母和判定方式不同；同一模型在 B01 与 B40 的分数不可直接相减。
- **安全分数要和效用一起看**：低 ASR 可能来自模型能力不足、过度拒绝或工具不可用；应同时报告良性任务成功率、误拒率和完成率。
- **区分“文本上同意”与“实际提交”**：B06 的 CoreFail、HarmEvidence、ObservedHarm 是三层不同终点；B16 的 OAR 也不是普通完成率。
- **区分“尝试”与“后果”**：越权调用尝试、后端拒绝、实际写入、可回滚后果应分别记录。
- **区分模型与脚手架**：B12 的 AWM/WebVoyager/WorkArena 是智能体框架；B30 的 Cy-Agent/AutoGPT/T-Agent 是攻击智能体；B33 的 SWE-agent/OpenHands/Aider 是代码智能体脚手架。
- **注意版本漂移**：上游任务会增删，论文数字与当前仓库可能不同；B01、B06、B23、B35 等已在对应分析文档中标注差异。
- **注意评测器差异**：LLM 判官、人工审计、状态 oracle 的结论可能不同；B06、B13、B22、B28 等有专门的判官/人工一致性表。
- **注意许可证**：论文、上游数据、系统镜像和攻击材料可能使用不同许可；再分发或用于生产前应逐项核对各基准 README 与原始许可证。

## 11. 已知缺口

| 缺口 | 影响 |
| --- | --- |
| B15 无公开数据/论文 | 不能纳入 516 张表和 39 项分析；本包只保留说明 |
| B36 无论文 | 只能依据公开数据表和仓库说明，不能引用论文方法学 |
| B11 gated | 本地没有原始任务，只能整理论文表 |
| B04/B21/B25/B26 无公开测试集 | 只能使用论文结果和已转录表，不能复跑完整题集 |
| B07/B29/B30/B35/B40 部分公开 | 任务数量、模型面板和论文分母可能不同 |
| B14 本地 GUI/文档两域 | 不能据此推断 Web/移动/视频域表现 |
| 部分攻击材料未归档 | 出于安全、许可或 gated 原因，只保留论文、入口和许可说明 |
| 04-indexes 旧版状态 | 部分“未取得数据”标签早于本次补档，不能直接作为当前状态 |

## 12. 索引与校验

| 文件 | 用途 |
| --- | --- |
| [`03-benchmarks/README.md`](03-benchmarks/README.md) | 40 项基准的最新逐项入口、测试集位置和论文链接 |
| [`03-benchmarks/archive-index.csv`](03-benchmarks/archive-index.csv) | 每项基准的收录范围、来源、公开研究口径和项目/论文入口 |
| [`03-benchmarks/file-manifest.csv`](03-benchmarks/file-manifest.csv) | 上游文件逐项来源、许可、计数和 SHA-256 |
| [`04-indexes/benchmark-catalog.csv`](04-indexes/benchmark-catalog.csv) | 旧版 benchmark 综合目录，适合快速看历史口径 |
| [`04-indexes/standards-catalog.csv`](04-indexes/standards-catalog.csv) | 42 项标准、监管和协议资料 |
| [`04-indexes/risk-evidence-rows.csv`](04-indexes/risk-evidence-rows.csv) | 风险类别与证据行的映射 |
| [`04-indexes/SHA256SUMS.txt`](04-indexes/SHA256SUMS.txt) | 归档文件校验 |
| [`03-benchmarks/table-analysis/README.md`](03-benchmarks/table-analysis/README.md) | 39 份表分析的导航、展示建议和已知口径差异 |

校验时建议：

1. 先核对 `03-benchmarks/file-manifest.csv` 的路径和 SHA-256；
2. 再用 `04-indexes/SHA256SUMS.txt` 核对旧版归档层；
3. 论文页数、表号以各基准 `paper/` PDF 和 `table-analysis/Bxx-*.md` 为准；
4. 数据集行数、任务数和模型面板以 `analysis/tables/*.csv` 的实际列为准，不只看 README 摘要。

## 13. 维护约定

后续更新时建议保持以下顺序：

1. 新增/替换上游文件，保留原始字节和上游目录结构；
2. 更新该基准 `README.md` 和 `archive-index.csv`；
3. 重新生成 `file-manifest.csv`、`analysis/tables/*.csv` 和对应 `table-analysis/Bxx-*.md`；
4. 若新增或修改表，更新 `OWASP-ASI-01-10-table-map.md` 与 `Model-table-index.md`；
5. 更新本 README 的日期、基准数、论文数、表数和覆盖状态；
6. 重新校验 SHA-256，并保留“论文数字 / 上游数据 / 本地实收”三种口径的差异说明。

## 14. 引用与许可

- 四份治理/评测框架请引用各自发布方和正式版本，不以本 README 代替原文。
- 各 benchmark 请引用其论文和项目主页；论文 PDF 只作为研究资料归档，版权归原作者/出版方。
- 上游测试集、系统镜像、攻击脚本和模型输出可能适用不同许可证；逐项许可见 `03-benchmarks/file-manifest.csv` 和基准目录 README。
- 本包新增的整理表、分析文档和映射文档用于研究与评测准备；引用具体数值时请同时注明原论文表号或 CSV 表名，避免只引用二次汇总。

---

**当前一句话总结**：这是一个以 40 项 benchmark 为骨架、以 38 篇论文和 516 张结构化表为证据层、并用 OWASP ASI 映射和模型索引连接风险与模型的智能体安全测评资料包。
