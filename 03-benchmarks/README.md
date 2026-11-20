# Agent 安全评测 Benchmark 档案

资料核对日期　2026-11-19

覆盖 40 项基准。38 项附论文全文 PDF（含正文与附录，按论文标题命名，存于各目录 `paper/`）；B15 信通院 AI Safety Benchmark 与 B36 SOCBench 经核查无对应论文。

测试集：29 项收录上游公开测试集全集，5 项收录作者公开的部分或元数据（B07 AgentHarm、B29 Cybench、B30 CVE-Bench、B35 Cyber Defense Benchmark、B40 METR Time Horizons），6 项未能下载测试集：B11 SafeArena 为需作者授权的 gated 数据集，其余 5 项无公开测试集（B04 Agent Red Teaming（ART）、B15 信通院 AI Safety Benchmark 2026 Q1、B21 MemSecBench、B25 MCP 风格运行时不变量（HCP）、B26 MADBench）。本次新增的上游原文件统一放在各基准 `data/upstream*/`，保持上游原始字节与目录结构，共 10,300 个文件、约 1.7 GB；此前整理的提取视图仍保留在 `data/` 下。

- [总目录 CSV](archive-index.csv) 包含实际收录范围、测试集位置与来源、公开研究口径、项目与论文入口。
- [逐文件清单 CSV](file-manifest.csv) 包含每个文件的上游地址、许可说明、计数及 SHA-256 校验值，覆盖全部 `data/upstream*/` 文件。
- 各基准的 `README.md` 说明数据、论文版本及其他材料。上游测试集原文件位于 `data/upstream*/`，此前整理的提取视图位于 `data/` 其余位置，论文位于 `paper/`，结果汇总位于 `results/`。

同一项基准的论文样本数、数据子集行数、标签行数和结果行数可能不同，按原目录说明分别使用。公开可查但有作者访问限制、许可待核或可直接复用为攻击的内容，表中保留材料状态与文献出处。

本表和逐文件清单对应本次 Benchmark 更新。包内其他目录的索引继续对应上一版。

## 逐项入口

| 编号与基准 | 测试集 | 论文 |
| --- | --- | --- |
| [B01 AgentDojo](B01-agentdojo/README.md) | 公开测试集完整 · [`data/upstream/`](B01-agentdojo/data/upstream/) | [论文全文](<B01-agentdojo/paper/AgentDojo - A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents.pdf>) · 26 页 |
| [B02 InjecAgent](B02-injecagent/README.md) | 公开测试集完整 · [`data/upstream/`](B02-injecagent/data/upstream/) | [论文全文](<B02-injecagent/paper/InjecAgent - Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents.pdf>) · 36 页 |
| [B03 Agent Security Bench（ASB）](B03-agent-security-bench/README.md) | 公开测试集完整 · [`data/upstream/`](B03-agent-security-bench/data/upstream/) | [论文全文](<B03-agent-security-bench/paper/Agent Security Bench (ASB) - Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents.pdf>) · 36 页 |
| [B04 Agent Red Teaming（ART）](B04-agent-red-teaming/README.md) | 无公开测试集 | [论文全文](<B04-agent-red-teaming/paper/Security Challenges in AI Agent Deployment - Insights from a Large Scale Public Competition.pdf>) · 30 页 |
| [B05 AgentDyn](B05-agentdyn/README.md) | 公开测试集完整 · [`data/upstream/`](B05-agentdyn/data/upstream/) | [论文全文](<B05-agentdyn/paper/AgentDyn - Are Your Agent Security Defenses Deployable in Real-World Dynamic Environments.pdf>) · 26 页 |
| [B06 SafeClawBench](B06-safeclawbench/README.md) | 公开测试集完整 · [`data/upstream/`](B06-safeclawbench/data/upstream/) | [论文全文](<B06-safeclawbench/paper/SafeClawBench - Separating Semantic, Audit-Evidence, and Sandbox Harm in Tool-Using LLM Agents.pdf>) · 32 页 |
| [B07 AgentHarm](B07-agentharm/README.md) | 公开测试集（作者部分发布） · [`data/upstream/`](B07-agentharm/data/upstream/) | [论文全文](<B07-agentharm/paper/AgentHarm - A Benchmark for Measuring Harmfulness of LLM Agents.pdf>) · 36 页 |
| [B08 Agent-SafetyBench](B08-agent-safetybench/README.md) | 公开测试集完整 · [`data/upstream/`](B08-agent-safetybench/data/upstream/) | [论文全文](<B08-agent-safetybench/paper/Agent-SafetyBench - Evaluating the Safety of LLM Agents.pdf>) · 26 页 |
| [B09 ToolEmu](B09-toolemu/README.md) | 公开测试集完整 · [`data/upstream/`](B09-toolemu/data/upstream/) | [论文全文](<B09-toolemu/paper/Identifying the Risks of LM Agents with an LM-Emulated Sandbox.pdf>) · 68 页 |
| [B10 WASP](B10-wasp/README.md) | 公开测试集完整 · [`data/upstream/`](B10-wasp/data/upstream/) | [论文全文](<B10-wasp/paper/WASP - Benchmarking Web Agent Security Against Prompt Injection Attacks.pdf>) · 22 页 |
| [B11 SafeArena](B11-safearena/README.md) | 上游访问受限 | [论文全文](<B11-safearena/paper/SafeArena - Evaluating the Safety of Autonomous Web Agents.pdf>) · 38 页 |
| [B12 ST-WebAgentBench](B12-st-webagentbench/README.md) | 公开测试集完整 · [`data/upstream/`](B12-st-webagentbench/data/upstream/) | [论文全文](<B12-st-webagentbench/paper/ST-WebAgentBench - A Benchmark for Evaluating Safety and Trustworthiness in Web Agents.pdf>) · 42 页 |
| [B13 OS-Harm](B13-os-harm/README.md) | 公开测试集完整 · [`data/upstream/`](B13-os-harm/data/upstream/) | [论文全文](<B13-os-harm/paper/OS-Harm - A Benchmark for Measuring Safety of Computer Use Agents.pdf>) · 32 页 |
| [B14 MMA-SafetyBench](B14-mma-safetybench/README.md) | 公开测试集完整 · [`data/upstream/`](B14-mma-safetybench/data/upstream/) | [论文全文](<B14-mma-safetybench/paper/MMA-SafetyBench - A Benchmark for Multimodal Agent Safety Evaluation.pdf>) · 19 页 |
| [B15 信通院 AI Safety Benchmark 2026 Q1](B15-caict-ai-safety-benchmark-2026q1/README.md) | 无公开测试集 | 无对应论文 |
| [B16 AuthorizationBench](B16-authorizationbench/README.md) | 公开测试集完整 · [`data/upstream/`](B16-authorizationbench/data/upstream/) | [论文全文](<B16-authorizationbench/paper/Act on Your Behalf, Beyond Your Authorization - Benchmarking LLM Agent Authorization Alignment.pdf>) · 24 页 |
| [B17 AuthGateBench](B17-authgatebench/README.md) | 公开测试集完整 · [`data/upstream/`](B17-authgatebench/data/upstream/) | [论文全文](<B17-authgatebench/paper/AuthGateBench - Benchmarking LLMs as Authorization Gate.pdf>) · 21 页 |
| [B18 PrivacyLens](B18-privacylens/README.md) | 公开测试集完整 · [`data/upstream/`](B18-privacylens/data/upstream/) | [论文全文](<B18-privacylens/paper/PrivacyLens - Evaluating Privacy Norm Awareness of Language Models in Action.pdf>) · 35 页 |
| [B19 CI-Work](B19-ci-work/README.md) | 公开测试集完整 · [`data/`](B19-ci-work/data/) | [论文全文](<B19-ci-work/paper/CI-Work - Benchmarking Contextual Integrity in Enterprise LLM Agents.pdf>) · 26 页 |
| [B20 AgentLeak](B20-agentleak/README.md) | 公开测试集完整 · [`data/upstream/`](B20-agentleak/data/upstream/) | [论文全文](<B20-agentleak/paper/AgentLeak - A Benchmark for Internal-Channel Privacy Leakage in Multi-Agent LLM Systems.pdf>) · 19 页 |
| [B21 MemSecBench](B21-memsecbench/README.md) | 无公开测试集 | [论文全文](<B21-memsecbench/paper/MemSecBench - Tracking Agent Memory Poisoning from Persistence to Consequence and Repair.pdf>) · 28 页 |
| [B22 ATBench](B22-atbench/README.md) | 公开测试集完整 · [`data/upstream/`](B22-atbench/data/upstream/) | [论文全文](<B22-atbench/paper/ATBench - A Diverse and Realistic Trajectory Benchmark for Long-Horizon Agent Safety.pdf>) · 29 页 |
| [B23 MCPSecBench](B23-mcpsecbench/README.md) | 公开测试集完整 · [`data/upstream/`](B23-mcpsecbench/data/upstream/) | [论文全文](<B23-mcpsecbench/paper/MCPSecBench - A Systematic Security Benchmark and Playground for Testing Model Context Protocols.pdf>) · 20 页 |
| [B24 MCP Security Bench（MSB）](B24-mcp-security-bench/README.md) | 公开测试集完整 · [`data/upstream/`](B24-mcp-security-bench/data/upstream/) | [论文全文](<B24-mcp-security-bench/paper/MCP Security Bench (MSB) - Benchmarking Attacks Against Model Context Protocol in LLM Agents.pdf>) · 32 页 |
| [B25 MCP 风格运行时不变量（HCP）](B25-mcp-runtime-invariants-hcp/README.md) | 无公开测试集 | [论文全文](<B25-mcp-runtime-invariants-hcp/paper/From Tool Connection to Execution Control - Benchmarking Security Invariants in MCP-Style Agent Runtimes.pdf>) · 28 页 |
| [B26 MADBench](B26-madbench/README.md) | 无公开测试集 | [论文全文](<B26-madbench/paper/MADBench - Benchmarking the Security of Multi-Agent Debate.pdf>) · 25 页 |
| [B27 DUMA-Bench](B27-duma-bench/README.md) | 公开测试集完整 · [`data/upstream/`](B27-duma-bench/data/upstream/) | [论文全文](<B27-duma-bench/paper/DUMA-Bench - A Dual-Control Multi-Agent Benchmark for Evaluating LLM Agent Security.pdf>) · 14 页 |
| [B28 R-Judge](B28-r-judge/README.md) | 公开测试集完整 · [`data/upstream/`](B28-r-judge/data/upstream/) | [论文全文](<B28-r-judge/paper/R-Judge - Benchmarking Safety Risk Awareness for LLM Agents.pdf>) · 24 页 |
| [B29 Cybench](B29-cybench/README.md) | 公开测试集（元数据） · [`data/upstream/`](B29-cybench/data/upstream/) | [论文全文](<B29-cybench/paper/Cybench - A Framework for Evaluating Cybersecurity Capabilities and Risks of Language Models.pdf>) · 150 页 |
| [B30 CVE-Bench](B30-cve-bench/README.md) | 公开测试集（元数据） · [`data/upstream/`](B30-cve-bench/data/upstream/) | [论文全文](<B30-cve-bench/paper/CVE-Bench - A Benchmark for AI Agents' Ability to Exploit Real-World Web Application Vulnerabilities.pdf>) · 18 页 |
| [B31 CyberSecEval 2](B31-cyberseceval-2/README.md) | 公开测试集完整 · [`data/upstream-purplellama/` 等](B31-cyberseceval-2/data/upstream-purplellama/) | [论文全文](<B31-cyberseceval-2/paper/CyberSecEval 2 - A Wide-Ranging Cybersecurity Evaluation Suite for Large Language Models.pdf>) · 21 页 |
| [B32 CyberSecEval 3](B32-cyberseceval-3/README.md) | 公开测试集完整 · [`data/upstream-purplellama/` 等](B32-cyberseceval-3/data/upstream-purplellama/) | [论文全文](<B32-cyberseceval-3/paper/CyberSecEval 3 - Advancing the Evaluation of Cybersecurity Risks and Capabilities in Large Language Models.pdf>) · 36 页 |
| [B33 SEC-bench](B33-sec-bench/README.md) | 公开测试集完整 · [`data/upstream/`](B33-sec-bench/data/upstream/) | [论文全文](<B33-sec-bench/paper/SEC-bench - Automated Benchmarking of LLM Agents on Real-World Software Security Tasks.pdf>) · 30 页 |
| [B34 CyberSOCEval](B34-cybersoceval/README.md) | 公开测试集完整 · [`data/upstream/` 等](B34-cybersoceval/data/upstream/) | [论文全文](<B34-cybersoceval/paper/CyberSOCEval - Benchmarking LLMs Capabilities for Malware Analysis and Threat Intelligence Reasoning.pdf>) · 26 页 |
| [B35 Cyber Defense Benchmark](B35-cyber-defense-benchmark/README.md) | 公开样例集 · [`data/upstream/`](B35-cyber-defense-benchmark/data/upstream/) | [论文全文](<B35-cyber-defense-benchmark/paper/Cyber Defense Benchmark - Agentic Threat Hunting Evaluation for LLMs in SecOps.pdf>) · 16 页 |
| [B36 SOCBench（Detection）](B36-socbench-detection/README.md) | 公开测试集完整 · [`data/`](B36-socbench-detection/data/) | 无对应论文 |
| [B37 BFCL](B37-bfcl-v4/README.md) | 公开测试集完整 · [`data/upstream/`](B37-bfcl-v4/data/upstream/) | [论文全文](<B37-bfcl-v4/paper/The Berkeley Function Calling Leaderboard (BFCL) - From Tool Use to Agentic Evaluation of Large Language Models.pdf>) · 22 页 |
| [B38 τ²-Bench](B38-tau2-bench/README.md) | 公开测试集完整 · [`data/upstream/`](B38-tau2-bench/data/upstream/) | [论文全文](<B38-tau2-bench/paper/τ²-Bench - Evaluating Conversational Agents in a Dual-Control Environment.pdf>) · 47 页 |
| [B39 OSWorld](B39-osworld/README.md) | 公开测试集完整 · [`data/upstream/`](B39-osworld/data/upstream/) | [论文全文](<B39-osworld/paper/OSWorld - Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments.pdf>) · 51 页 |
| [B40 METR Time Horizons](B40-metr-time-horizons/README.md) | 公开结果数据 · [`data/upstream/`](B40-metr-time-horizons/data/upstream/) | [论文全文](<B40-metr-time-horizons/paper/Measuring AI Ability to Complete Long Software Tasks.pdf>) · 45 页 |
