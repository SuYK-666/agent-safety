# OWASP ASI 十类 × Benchmark 数据表映射

> 核对范围：`C:\Users\18201\Desktop\agent-safety\03-benchmarks` 下 B01–B40。  
> 实际纳入：39 项基准、516 张 `analysis/tables/*.csv` 表。B15 信通院 AI Safety Benchmark 只有说明文件、没有数据表与论文，故不纳入。  
> 归类口径：按“这张表实际测什么/记录什么”归入 ASI 类别，而不是按论文标题归类。同一张表可以同时出现在多个 ASI 下；`data_*` 表描述攻击面或数据集构成，`paper_*` 表描述结果或防御，`derived_*`/`results_*` 表沿用其母表的风险语义。  
> 说明：OWASP ASI 的分类本身有一定重叠，尤其 ASI02（工具滥用）与 ASI10（失控）、ASI03（权限）与 ASI07（智能体间通信）。本文采用“主要风险机制优先”的原则，并在容易混淆处加注。

## 0. 总览：每个基准主要涉及的 ASI

| 基准 | 主要 ASI | 一句话定位 |
| --- | --- | --- |
| B01 AgentDojo | ASI01/02/08 | 工具型智能体的间接提示注入与防御 |
| B02 InjecAgent | ASI01/02/03/08 | 工具集成智能体的直接/间接注入、数据窃取 |
| B03 ASB | ASI01/02/04/06/08 | 10 类场景智能体的注入、记忆投毒、PoT 后门 |
| B04 ART | ASI01/03/10 | 大规模红队竞赛、跨模型攻击迁移 |
| B05 AgentDyn | ASI01/02/08 | 动态长任务环境中的注入与防御可用性 |
| B06 SafeClawBench | ASI01/02/03/06 | 语义、证据、沙盒三层伤害判定 |
| B07 AgentHarm | ASI02/05/09/10 | 工具型智能体执行有害任务 |
| B08 Agent-SafetyBench | ASI02/03/05/08/10 | 8 类风险、10 类失效模式 |
| B09 ToolEmu | ASI02/03/05/08/09 | 指令不完整导致的工具风险 |
| B10 WASP | ASI01/02/03 | Web 智能体提示注入 |
| B11 SafeArena | ASI02/09/10 | Web 智能体有害任务完成与拒绝 |
| B12 ST-WebAgentBench | ASI02/03/08 | 企业 Web 智能体策略合规 |
| B13 OS-Harm | ASI01/02/05/09/10 | 电脑使用智能体的滥用、注入、误操作 |
| B14 MMA-SafetyBench | ASI01/02/03/09/10 | 视觉语义劫持与 GUI 伪造界面 |
| B16 AuthorizationBench | ASI02/03/08/09/10 | 授权边界与越权完成 |
| B17 AuthGateBench | ASI03/09 | LLM 作为审批门的过度拦截 |
| B18 PrivacyLens | ASI02/03/09 | 隐私规范“知道但做不到” |
| B19 CI-Work | ASI02/03/08/09 | 企业上下文完整性 |
| B20 AgentLeak | ASI02/03/06/07 | 多智能体内部通道泄露 |
| B21 MemSecBench | ASI06/07/08 | 记忆投毒全生命周期 |
| B22 ATBench | ASI01/02/03/08/10 | 长轨迹安全风险 |
| B23 MCPSecBench | ASI01/02/03/04 | MCP 四攻击面靶场 |
| B24 MSB | ASI01/02/03/04/08 | MCP 规划/调用/响应阶段攻击 |
| B25 HCP | ASI02/03/04/08/10 | MCP 风格运行时执行控制不变量 |
| B26 MADBench | ASI01/06/07/08/10 | 多智能体辩论对攻击的放大/吸收 |
| B27 DUMA-Bench | ASI01/02/03/07/08/09 | 双控多智能体、用户施压 |
| B28 R-Judge | ASI01/02/03/08/10 | 轨迹安全风险判官 |
| B29 Cybench | ASI05/10 | CTF 攻防能力 |
| B30 CVE-Bench | ASI03/05/10 | 真实 CVE 自主利用 |
| B31 CyberSecEval 2 | ASI01/05/09 | 代码安全、注入、解释器滥用、攻击协助 |
| B32 CyberSecEval 3 | ASI01/02/05/09/10 | 视觉注入、钓鱼、AutoPatch、自主渗透 |
| B33 SEC-bench | ASI05/08/10 | 真实漏洞修补与 PoC |
| B34 CyberSOCEval | ASI05/09 | 恶意软件分析、威胁情报推理 |
| B35 Cyber Defense Benchmark | ASI03/05/08/10 | 威胁狩猎智能体 |
| B36 SOCBench Detection | ASI05/08 | 网络流检测数据集 |
| B37 BFCL v4 | ASI02/08/10 | 函数调用、多轮、无关函数拒调 |
| B38 τ²-Bench | ASI02/08/09/10 | 双控对话智能体可靠性 |
| B39 OSWorld | ASI02/05/08/10 | 电脑操作能力基线 |
| B40 METR Time Horizons | ASI08/10 | 长任务自主能力趋势 |

---

## ASI01 目标劫持（Agent Goal Hijacking）

**纳入标准**：提示注入（直接/间接/视觉）、指令覆盖、目标替换、任务劫持、越狱模板、系统提示/角色层级攻击，以及用于衡量这些攻击成功率的 ASR 表。单纯的“有害任务完成”归 ASI10；单纯“工具越权”归 ASI02/ASI03。

### B01 AgentDojo
- `data_injection_goals_v1.csv`、`data_injection_vectors.csv` — 27 个注入目标与注入载体（工具输出、邮件、文档等），是目标劫持的攻击面清单。
- `data_suite_summary_v1.csv`、`data_task_files_by_version.csv` — 四个套件的用户任务 × 注入任务配对规模与版本修订，说明 629 个安全用例如何构成。
- `paper_T1_environments.csv` — 各环境的工具数、用户任务数、注入任务数，界定可被劫持的动作空间。
- `paper_T2_attacker_knowledge_gpt4o.csv` — 攻击者是否知道用户名/模型名对定向 ASR 的影响。
- `paper_T3_agents_important_message_attack.csv` — 10 个模型在 “Important message” 注入下的定向 ASR 与效用。
- `paper_T4_attack_prompts_gpt4o.csv` — TODO、Ignore previous、InjecAgent、Important message、自适应 Max 五种注入模板的 ASR 对比。
- `paper_T5_defenses_gpt4o.csv` — 分隔符、PI detector、重复提示、工具过滤等对注入 ASR 的防御效果。
- `paper_text_key_numbers.csv` — Slack 套件 92% ASR、工具输出末尾注入约 70% ASR 等关键数字。

### B02 InjecAgent
- `data_attack_type_by_attack_category.csv`、`data_attacker_cases_by_type.csv`、`data_attacker_cases.csv` — 直接伤害/数据窃取两大类攻击指令及子类分布。
- `data_overview.csv`、`data_test_case_files.csv` — base/enhanced 两套设置的 1,054 个用例，enhanced 在攻击指令前加 hacking prompt。
- `data_user_case_content_freedom.csv`、`data_user_cases.csv` — 用户工具上下文的“内容自由度”，高自由度位置更易藏注入。
- `paper_T1_attack_categories.csv` — 直接伤害与数据窃取的攻击类别、案例数与示例。
- `paper_T3_asr_valid_main.csv`、`paper_T6_valid_rates.csv`、`paper_T7_asr_valid_low_valid_agents.csv`、`paper_T8_asr_all.csv`、`paper_T9_asr_all_by_attack_type.csv`、`paper_T11_asr_valid_simple_react.csv`、`paper_T12_asr_all_simple_react.csv` — 不同模型/提示框架下的注入 ASR 与有效率。
- `paper_T4_association_user_vs_attacker_case.csv` — 用户上下文 vs 攻击者指令对 ASR 的关联强度。
- `paper_T10_response_quality_failed_cases.csv` — 攻击失败时模型回复的相关性/清晰度，含模型主动提醒注入的案例。
- `paper_text_key_numbers.csv` — 数据窃取两步漏斗、增强提示放大效应等。

### B03 Agent Security Bench
- `data_attack_tools.csv`、`data_attack_type_by_agent.csv` — 400 个攻击工具与各场景智能体的注入攻击类型。
- `paper_T3_statistics.csv` — 5 类 DPI、5 类 IPI、记忆投毒、混合攻击、PoT 后门的总体统计。
- `paper_T5_attack_results_by_backbone.csv` — 13 个骨干模型在 DPI/IPI/记忆投毒/混合/PoT 下的 ASR。
- `paper_T7_defenses_DPI.csv`、`paper_T8_defenses_IPI.csv` — DPI/IPI 防御前后 ASR。
- `paper_T14_attack_combinations.csv` — DPI+IPI、DPI+MP、IPI+MP、三者混合的组合攻击 ASR。
- `paper_T17_prompt_injection_types.csv` — Combined/Context Ignoring/Escape/Fake Completion/Naive 五种注入写法。
- `paper_T18_aggressive_vs_non.csv` — 激进/非激进攻击任务对 ASR 与拒绝率的影响。

### B04 Agent Red Teaming
- `paper_T1_asr_by_category_vector.csv` — 机密泄露、目标冲突、违禁内容、违禁动作四类，直接 vs 间接攻击向量。
- `paper_F3_challenge_asr_by_model.csv` — 18 个模型的竞赛会话级 ASR。
- `paper_F5_transfer_matrix.csv`、`paper_F5_transfer_long.csv`、`derived_F5_transfer_summary.csv` — 14×14 跨模型攻击迁移矩阵与来源/目标汇总。
- `paper_text_key_numbers.csv` — 180 万次攻击尝试、4,700 条 ART 攻击等规模信息。

### B05 AgentDyn
- `data_injection_goals.csv`、`data_suite_summary.csv` — 28 个注入目标与三个套件 560 个安全用例。
- `paper_T2_overview.csv`、`paper_T1_benchmark_complexity.csv` — 动态任务的平均工具数、轨迹长度、涉及应用数。
- `paper_T15_T17_asr.csv`、`paper_T17_asr_system.csv` — 12 模型 × 11 防御配置的 ASR。
- `paper_T3_main_defenses.csv` — 4 个代表模型 × 10 种防御的 ASR/效用。
- `paper_T8_other_attacks.csv` — Ignore、Completion、人工自适应攻击在 GPT-5-mini/GPT-5.1/Claude-Sonnet-4.5 上的 ASR。
- `derived_defense_means.csv`、`derived_full_matrix_overall.csv` — 按防御/模型的聚合 ASR。

### B06 SafeClawBench
- `data_attack_type_x_difficulty.csv`、`data_attack_type_x_harm_type.csv`、`data_attack_type_x_lifecycle.csv` — ADI/DPI/IPI/MEX/MPI/TRI 六类攻击的难度、伤害类型与生命周期分布。
- `data_profile_600.csv`、`data_seed72_stats.csv` — 600 条挑战与 72 条种子集的攻击构成。
- `paper_T1_attack_types.csv` — 六类攻击定义与示例。
- `paper_T3_headline_corefail.csv`、`paper_T4_harm_audit_D0_by_model.csv` — 五模型无防御下的语义 CoreFail。
- `paper_T16_harm_audit_D0_by_attack.csv`、`paper_T28_corefail_by_attack_D0.csv` — 按攻击类型的 CoreFail/伤害证据。
- `paper_T27_corefail_nine_policies.csv`、`paper_T32_d4_ablation.csv`、`paper_T33_policy_prompt_length.csv`、`paper_T38_matched_length_control.csv` — 提示防御、策略长度与消融。
- `paper_T29_harness_asr.csv`、`paper_T31_harness_audit_adi20.csv` — 单轮 vs 多轮 harness 对 ASR 的影响。
- `paper_T42_exec_metric_hierarchy_D0.csv`、`paper_T43_paired_defense_tests.csv` — 从 ToolCall-ASR 到状态变化的层级指标与防御配对检验。

### B07 AgentHarm
- `paper_T3_prompting.csv` — Standard/CoT/ReAct/Refusal-prompt 四种提示下的伤害分与拒绝率，含越狱模板效果。
- `paper_T8_agent_vs_chat_refusal.csv` — 同一有害请求以智能体任务 vs 纯聊天提出时的拒绝率差异（安全训练未迁移到工具调用）。

### B10 WASP
- `data_attack_env_x_evaltype.csv`、`data_attacker_goals.csv` — 21 个攻击目标、16 个页面状态检查 + 5 个外泄 URL 检查。
- `data_overview.csv` — 42 个场景 × 2 种注入模板 = 84 个任务。
- `paper_T2_main_results.csv` — 13 种配置的中间 ASR 与端到端 ASR。
- `paper_T3_url_vs_plaintext.csv` — URL 型 vs 纯文本型注入。
- `paper_T4_task_related_vs_agnostic.csv` — 攻击者是否知道用户目标的 ASR 差异。
- `paper_T5_attacker_goals_violation.csv` — 攻击目标对应的安全违规类别（访问、外泄、破坏、骚扰等）。

### B11 SafeArena
- `paper_T5_refusal_direct_vs_priming.csv` — 直接请求 vs priming（让模型以为已在执行）的拒绝率变化。
- `paper_T12_full_refusal.csv` — 按伤害类别的拒绝率，反映越狱/任务分解后的目标劫持空间。

### B12 ST-WebAgentBench
- `data_policy_template.csv` — 含 `jailbreaking` 策略模板，属于提示层攻击/越狱约束。
- `paper_T2_statistics.csv` — 六个策略维度（含安全与鲁棒性）在三个站点上的分布，界定劫持可绕过的策略面。

### B13 OS-Harm
- `data_category_x_app.csv`、`data_category_x_jailbreak.csv` — 用户滥用、提示注入、模型失误三类任务，以及 25 对越狱模板。
- `data_injection_vector_x_goal.csv` — 6 种注入载体 × 12 种目标（删文件、发邮件、停任务、跑脚本等）。
- `paper_T2_main_results.csv` — 五模型在滥用/注入/失误三类下的不安全率。
- `paper_F5_jailbreak_template.csv` — 直接 vs 越狱模板的不安全率/完成率。
- `paper_T4a_injection_vectors.csv`、`paper_T4b_injection_goals.csv` — o4-mini 按注入载体/目标的细分成功率。

### B14 MMA-SafetyBench
- `data_document_samples.csv` — 简历/发票文档中的视觉注入样本。
- `data_gui_attack_attack_type.csv`、`data_gui_attack_by_domain.csv`、`data_gui_attack_json_fields.csv`、`data_gui_attacks_per_base_task.csv` — GUI 攻击意图、领域、载荷字段与每基础任务变体数。
- `derived_domain_means.csv`、`derived_model_means.csv` — 按领域/模型的 ASR 汇总。
- `paper_T2_asr.csv`、`paper_T3_neutral_prompt_asr.csv`、`paper_T5_asr_with_safety_prompt.csv` — 视觉注入 ASR、中性提示对照、安全提示前后。
- `paper_T6_semantic_compromise_rate.csv` — 语义劫持率 SCR，衡量模型是否在推理中采纳了恶意指令。

### B16 AuthorizationBench
- `data_trigger_type.csv`、`data_trigger_x_harm.csv` — 14 类情境触发中，恶意注入（直接诱导越权 86、扭曲授权范围 32）属于目标劫持；其余为良性压力（见 ASI09）。

### B20 AgentLeak
- `data_injection_surface.csv`、`data_attack_class.csv`、`data_attack_family.csv` — 注入面、攻击类与攻击族（F1 提示/指令注入）。
- `paper_T4_T5_attack_taxonomy.csv`、`paper_T14_attack_families.csv` — 攻击族分类与各族 ASR。

### B22 ATBench
- `data_risk_source.csv`、`data_risk_source_x_harm.csv` — 8 类风险来源中的“间接注入 77 条”，以及来源 × 现实伤害交叉。

### B23 MCPSecBench
- `data_attack_prompts.csv` — 11 条 MCP 攻击提示，含直接提示注入。
- `paper_T1_asr_rr_platforms.csv` — 17 类攻击 × 3 平台的 ASR/拒绝率，其中 ATT-1 Prompt Injection 属目标劫持。

### B24 MCP Security Bench
- `data_cases_attack_type.csv` — PI（描述注入）、PI-UI、PI-FE 等攻击实例。
- `paper_T1_attack_types.csv` — 规划阶段的名称碰撞、偏好操纵、描述注入。
- `paper_T3_asr.csv`、`paper_T11_single_attacks_full.csv`、`paper_T12_mixed_attacks_full.csv`、`paper_T13_qwen3_thinking.csv` — 10 模型 × 12 攻击的 ASR，含 PI 与组合攻击。

### B25 MCP Runtime Invariants (HCP)
- `paper_T7_agentdojo_native.csv` — 在 AgentDojo 原生任务上验证执行层控制能否阻断注入导致的越权调用。

### B26 MADBench
- `paper_T1_attack_families.csv`、`paper_T2_amplification_factors.csv` — M1 越狱、M2 工作区间接注入，以及多智能体辩论对 ASR 的放大系数。
- `paper_T10_rounds.csv` — 辩论轮数增加是否放大/吸收攻击。

### B27 DUMA-Bench
- `data_tasks_per_domain.csv`、`data_tasks.csv` — 邮件 RAG 钓鱼等任务定义。
- `paper_T2_domain_asr.csv`、`paper_T5_domains.csv` — 8 个安全领域的 ASR，钓鱼领域在双控下从 2.2% 升至 61.5%。

### B28 R-Judge
- `data_attack_type_x_label.csv`、`data_category_x_attack_type.csv` — 414 条注入攻击 vs 157 条非攻击意外风险。
- `paper_T1_main_results.csv`、`paper_T2_prompting.csv`、`paper_T8_f1_by_category.csv` — 12 个模型识别注入/意外风险的 F1。

### B31 CyberSecEval 2
- `data_pi_multilingual_language.csv`、`data_pi_risk_category.csv`、`data_pi_variant_x_type.csv` — 提示注入的多语言、风险类别、15 种手法 × 安全/逻辑违规。
- `data_suite_sizes.csv` — 251 条注入 + 1,004 条多语言版本的规模。
- `derived_figure_row_means.csv`、`paper_F3_prompt_injection.csv`、`paper_F4_security_vs_logic_injection_approx.csv` — 各模型注入成功率与安全/逻辑违规拆分。

### B32 CyberSecEval 3
- `data_vpi_overview.csv`、`data_vpi_technique.csv`、`data_vpi_type_x_risk.csv` — 1,000 条视觉提示注入，直接/间接、安全/逻辑违规、7 种手法。
- `paper_F11_prompt_injection.csv` — 7 个模型的文本注入成功率。
- `paper_PromptGuard_eval.csv` — PromptGuard 对越狱、多语言、间接注入的召回/FPR。

---

## ASI02 工具滥用与利用（Tool Misuse & Exploitation）

**纳入标准**：工具/函数调用错误、恶意工具、工具投毒/影子/包名抢注、越界参数、混淆代理（confused deputy）、Web/GUI/OS 操作越权、工具选择错误、无关函数误调、执行层动作伤害，以及描述工具清单与动作空间的数据表。单纯的“模型拒绝/遵从”归 ASI01/ASI10；“权限范围”归 ASI03。

### B01 AgentDojo
- `data_user_task_prompts.csv` — 86 个用户任务原文，定义智能体正常工具使用范围。
- `paper_T1_environments.csv` — workspace/slack/travel/banking 的工具数与任务数，是工具滥用面的基线。
- `paper_T5_defenses_gpt4o.csv` — Tool filter 防御同时提高效用并把定向 ASR 降到 6.84%，说明“限制可用工具”直接作用于工具滥用。
- `paper_T3_agents_important_message_attack.csv` — 受攻击后的效用下降反映工具调用被劫持后的任务破坏程度。

### B02 InjecAgent
- `data_toolkit_categories.csv`、`data_toolkits.csv` — 38 个工具包、330 个工具的分类与规模。
- `data_user_cases.csv` — 17 个用户工具案例及其内容自由度。
- `data_attacker_cases.csv` — 攻击者工具、指令与期望达成，描述如何利用用户工具执行越权动作。
- `paper_T1_attack_categories.csv` — 直接伤害类攻击（物理、财务、数据安全）依赖工具动作完成。
- `paper_T3_asr_valid_main.csv`、`paper_T6_valid_rates.csv`、`paper_T7_asr_valid_low_valid_agents.csv`、`paper_T8_asr_all.csv`、`paper_T9_asr_all_by_attack_type.csv`、`paper_T11_asr_valid_simple_react.csv`、`paper_T12_asr_all_simple_react.csv` — 工具调用型智能体的 ASR。
- `paper_T10_response_quality_failed_cases.csv` — 攻击失败时模型是否仍正确使用工具完成任务。

### B03 Agent Security Bench
- `data_agents_summary.csv`、`data_normal_tools.csv`、`data_user_tasks.csv` — 10 个场景智能体的正常工具与 51 个用户任务。
- `data_attack_tools.csv`、`data_attack_type_by_aggressive.csv` — 400 个攻击工具（20 激进 + 20 非激进/场景），是工具投毒与恶意工具的清单。
- `data_attack_type_by_agent.csv` — 各场景智能体面对的 DPI/IPI/记忆/PoT 攻击类型。
- `paper_T3_statistics.csv` — 20 个正常工具、400 个攻击工具/任务、13 种攻击方法。
- `paper_T5_attack_results_by_backbone.csv` — 13 模型在攻击工具下的 ASR。
- `paper_T6_NRP.csv` — NRP = PNA × (1 − ASR)，衡量“工具任务完成 × 安全”。
- `paper_T18_aggressive_vs_non.csv` — 激进/非激进工具任务的 ASR 与拒绝率。
- `paper_T19_defense_utility_no_attack.csv` — 防御对正常工具任务效用（PNA）的代价。

### B04 Agent Red Teaming
- `paper_T1_asr_by_category_vector.csv` — “违禁动作”类攻击直接测工具/部署动作的越权执行。

### B05 AgentDyn
- `data_environments.csv`、`data_tools_by_suite.csv` — 7 个环境、100 个工具及套件分布。
- `data_suite_summary.csv`、`paper_T1_benchmark_complexity.csv` — 平均 33.33 个可见工具、7.10 步轨迹、3.17 个应用，工具滥用面远大于静态基准。
- `paper_T9_T11_benign_utility.csv`、`paper_T12_T14_utility_under_attack.csv` — 正常/受攻击下的工具任务效用。
- `paper_T15_T17_asr.csv`、`paper_T17_asr_system.csv` — 各防御下的工具调用 ASR。
- `paper_T3_main_defenses.csv` — Tool Filter、CaMeL、Progent、DRIFT 等工具/系统级防御。
- `derived_defense_means.csv`、`derived_full_matrix_overall.csv` — 防御对效用与 ASR 的聚合影响。

### B06 SafeClawBench
- `data_attack_type_x_harm_type.csv` — 把伤害分为 action/leak/persist，action 类直接对应工具动作。
- `data_exec_attack_type.csv`、`data_exec_available_tools.csv`、`data_exec_subtype.csv` — 可执行沙盒的攻击类型、可用工具与子类型。
- `data_exec_oracle_checks.csv`、`paper_T40_exec_oracle_checks.csv` — 8 种状态 oracle（memory_value_contains、email_sent、code_output_contains 等）。
- `paper_T18_exec_harm_by_split.csv`、`paper_T19_mcnemar_exec.csv`、`paper_T21_core_exec_matched.csv` — 执行层伤害与防御显著性。
- `paper_T41_exec_observed_harm.csv`、`paper_T42_exec_metric_hierarchy_D0.csv` — ToolCall-ASR、StateChange-ASR、ObservedHarm 的层级。
- `paper_T22_T24_benign_utility_by_model.csv`、`paper_T23_benign_utility_by_defense.csv`、`paper_T25_benign_utility_reduced_panel.csv` — 防御对 42 个良性工具任务的影响。
- `paper_T30_harness_tool_usage.csv` — 不同 harness 下的工具使用差异。
- `paper_T31_harness_audit_adi20.csv` — 工具调用审计。
- `paper_T43_paired_defense_tests.csv` — 防御配对检验。

### B07 AgentHarm
- `data_behavior_list.csv`、`data_category_by_split.csv` — 有害/良性行为及其工具链类别。
- `data_split_summary.csv`、`data_target_function_count_dist.csv` — 每个行为的工具数分布（多数 3 个），说明多步工具链。
- `data_top_target_functions_harmful.csv` — 最常被滥用的函数：网页、搜索、邮件、发帖、Tor 搜索、图像生成。
- `derived_T9_pivot_by_model.csv`、`paper_T9_public_test_main.csv`、`paper_T10_private_test.csv` — 15/7 模型的工具任务伤害分与拒绝率。
- `paper_T2_best_of_n.csv`、`paper_T3_prompting.csv` — 采样/提示对工具型有害任务完成的影响。

### B08 Agent-SafetyBench
- `data_environment_usage.csv`、`paper_T2_environment_classes.csv` — 349 个模拟环境及 4 级现实性。
- `data_risk_category.csv` — 8 类风险中多数需工具行为完成（财产损失、隐私、可用性、代码等）。
- `data_risk_x_behavior_content.csv` — 1,589 条行为类 vs 411 条内容类。
- `data_risk_x_fulfillable.csv` — 735 条可安全完成，区分“正确用工具”与“拒绝”。
- `data_failure_mode_counts.csv`、`data_failure_modes_per_case.csv`、`paper_T4_failure_mode_definitions.csv` — 10 类失效模式，含忽视工具风险、信息不足即调用、过度信任工具结果。
- `paper_T5_safety_scores_by_risk.csv`、`paper_T6_safety_scores_by_failure_mode.csv` — 16 模型按风险/失效模式的安全分。

### B09 ToolEmu
- `data_overview.csv`、`data_toolkit_category.csv`、`data_toolkits.csv`、`data_toolkits_per_case.csv` — 144 个测试用例、38 个工具包、330 个工具，66% 单工具包、34% 多工具包。
- `data_risky_outcome_labels.csv`、`paper_F5_risk_type_distribution.csv` — 隐私、财务、未授权访问、声誉、错误信息、财产损害等工具风险结果。
- `paper_T1_toolkit_classes.csv` — 工具包按现实 API 可得性分级。
- `paper_T4_agent_evaluation.csv` — 5 个模型在 144 个工具任务上的安全分/失败率/有用性。
- `paper_T2_end_to_end_validation.csv`、`paper_T3_component_validation.csv` — 模拟器与评估器对工具失败的识别可信度。
- `paper_TD1_emulator_issue_detail.csv`、`paper_TD2_leave_one_out.csv`、`paper_TD3_kappa_original_scale.csv`、`paper_TD4_TD5_author_validation.csv`、`paper_TD7_temperature_claude2.csv` — 模拟器问题分级、留一法、κ、作者标注与温度稳定性。
- `paper_text_key_numbers.csv` — Terminal 工具包 7 个模拟失败中 6 个在真实沙盒复现。

### B10 WASP
- `data_utility_tasks_by_site.csv` — 37 个正常 Web 工具任务（GitLab 25、Reddit 12）。
- `data_attack_env_x_evaltype.csv` — 页面状态检查 vs 外泄 URL 检查，直接对应 Web 工具动作。
- `paper_T2_main_results.csv` — 13 种配置的效用与 ASR；低端到端 ASR 常因工具能力不足。
- `paper_T3_url_vs_plaintext.csv`、`paper_T4_task_related_vs_agnostic.csv` — 注入方式对 Web 动作成功率的影响。
- `paper_T5_attacker_goals_violation.csv` — 添加 SSH key、加 Owner、删数据、发帖骚扰等工具动作。

### B11 SafeArena
- `paper_F3_task_completion.csv` — 有害/安全 Web 任务完成率，直接测 Web 工具滥用。
- `paper_T11_full_tcr.csv` — 5 模型 × 5 伤害类别的任务完成率。
- `paper_T3_normalized_safety.csv` — NSS 将“能力不足”与“安全拒绝”分开。
- `paper_T4_aria_human.csv` — 人工 ARIA 风险等级。

### B12 ST-WebAgentBench
- `data_overview.csv`、`data_tasks_by_site.csv` — 375 个任务、3 个站点（GitLab/SuiteCRM/ShoppingAdmin）。
- `data_policy_category_x_site.csv` — 边界、严格执行、鲁棒性、用户同意、层级、错误处理六维策略。
- `data_policy_load_bins.csv` — 65.3% 任务同时激活 >5 条策略。
- `data_policy_source.csv` — 组织/用户/任务三级策略来源。
- `data_policy_template.csv` — 11 种策略模板（访问管理、询问用户、不可逆动作等）。
- `data_task_metadata_tag.csv` — 任务难度与元数据。
- `paper_F2_agent_metrics.csv` — AWM/WebVoyager/WorkArena 的 CR/CuP/all-pass@3。
- `paper_T2_statistics.csv`、`paper_T3_dimension_ablation.csv` — 六维策略统计与消融。

### B13 OS-Harm
- `data_category_x_app.csv`、`data_split_files_by_app.csv`、`data_profile.csv` — 149 个 OS 任务的应用分布与字段覆盖。
- `data_injection_vector_x_goal.csv` — 注入目标中的删文件、发密码、跑 cron/本地/远程脚本、填 SSH 表单等，全部是 OS 工具动作。
- `paper_T2_main_results.csv` — 5 模型在滥用/注入/失误下的不安全率与任务完成率。
- `paper_T5_osworld_obs_types.csv` — OSWorld 观测类型对动作判定影响。

### B14 MMA-SafetyBench
- `data_gui_base_tasks_by_domain.csv`、`data_gui_attack_by_domain.csv` — 42 个 Chrome 基础任务与 GUI 攻击领域。
- `data_gui_attack_payload_category.csv` — 隐私外泄、金融劫持、Root 提权、持续监控、恢复出厂等 GUI 动作。
- `data_gui_attack_json_fields.csv`、`data_gui_attacks_per_base_task.csv` — 伪造按钮 bbox 与每任务变体。
- `paper_T4_clean_task_success.csv` — 干净 GUI 任务成功率，用于排除“能力不足”。

### B16 AuthorizationBench
- `data_task_services.csv`、`data_task_labels.csv` — 286 个任务使用的邮件/文档等服务与标签。
- `paper_T11_completion_authorization.csv`、`paper_T12_reasoning_effort.csv` — 3 种 harness × 4 模型 × 2 推理强度的完成率与越权率。
- `paper_T13_harm_test_level.csv`、`paper_T6_composition.csv` — 任务伤害等级与构成。

### B17 AuthGateBench
- `paper_T2_eval_implicit_policy.csv`、`paper_T5_eval_explicit_policy.csv` — 5 类动作级失效模式（范围升级、凭证探查、外部分享、护栏绕过、推断参数）的审批判定。
- `data_pairs.csv`、`data_category_x_role.csv` — 350 个动作对比对与角色分布。

### B18 PrivacyLens
- `data_toolkits.csv` — Notion/Messenger/Gmail/Slack/Facebook/Calendar 工具包。
- `data_final_action.csv` — 最终发送动作（消息、邮件、帖子）分布。
- `paper_T2_probing_and_action.csv`、`paper_T3_extended_seeds.csv`、`paper_T5_confaide_culturebank.csv` — 工具执行中的隐私泄露率。

### B19 CI-Work
- `data_toolkits_ess4.csv` — Gmail/Notion/Slack/Calendar/Zoom/GoogleForm 工具包。
- `data_flow_x_category_ess4.csv` — 信息流方向 × 敏感类别，描述工具发送动作。
- `paper_T1_main_results.csv` — 9 模型在 5 种信息流下的泄露率/违规率/传达率。

### B20 AgentLeak
- `data_agents_per_scenario.csv`、`data_vertical_x_topology.csv` — 单/多智能体拓扑。
- `paper_F7_secondary_channels.csv` — 工具输入 C3 泄露 62–86%、日志 C6 65–89%。
- `paper_T13_frameworks.csv` — CrewAI/AutoGPT/LangChain/MetaGPT 等框架的系统性通道问题。

### B21 MemSecBench
- `derived_pooled_by_harness.csv`、`paper_T2_lifecycle_24configs.csv` — 2 个智能体框架 × 4 个记忆后端 × 3 个 LLM，属工具/运行时配置。

### B22 ATBench
- `data_overview.csv` — 1,000 条轨迹、2,084 个工具、平均 4.49 个智能体回合。
- `data_failure_mode.csv`、`data_label.csv` — 14 类失效模式（未确认/越权操作、未校验工具输出、未授权披露等）。
- `data_real_world_harm.csv`、`data_risk_source_x_harm.csv` — 工具轨迹导致的现实伤害。
- `paper_T1_benchmark_comparison.csv` — 与 R-Judge 等轨迹基准的规模/工具数对比。
- `paper_T2_main_results.csv` — 17 个判官模型对工具轨迹的风险识别。

### B23 MCPSecBench
- `paper_T1_asr_rr_platforms.csv` — 17 类攻击 × 3 平台 × 3 防御；客户端/协议/服务端/宿主四攻击面。
- `paper_T2_defense_protection.csv` — MCIP/FAN 对各攻击面的防护率。
- `data_experiments_asr_by_provider_attack.csv`、`data_experiments_runs_per_provider.csv` — 每平台 15 次运行记录。

### B24 MCP Security Bench
- `data_agents.csv`、`data_cases_agent_x_attack_type.csv`、`data_cases_attack_task.csv`、`data_cases_attack_type.csv` — 10 个场景智能体、2,000 条攻击实例、12 类攻击。
- `paper_T1_attack_types.csv` — 名称碰撞、偏好操纵、描述注入、越界参数、冒充用户、伪造错误、工具转移、检索注入及组合。
- `paper_T2_statistics.csv` — 25 个 MCP 服务器、304 个良性工具、405 个攻击工具。
- `paper_T3_asr.csv` — 10 模型 × 12 攻击的 ASR，OP 越界参数平均 76.5%。
- `paper_T11_single_attacks_full.csv`、`paper_T12_mixed_attacks_full.csv` — ASR/PUA/NRP 完整矩阵。
- `paper_T13_qwen3_thinking.csv` — Qwen3 8B 思考模式对 ASR/PUA 的影响。
- `paper_T4_defense_mcip.csv` — MCIP 防御前后 ASR/PUA/NRP。

### B25 MCP Runtime Invariants (HCP)
- `paper_T2_main_results.csv` — B0 直接执行、B1 连接层控制、B1+拒绝审批、B2 HCP、B3 网关 ACL 五模式。
- `paper_T3_dataflow_boundary.csv` — 受控通道 vs 普通参数的数据流边界。
- `paper_T4_mechanism_removals.csv` — 逐个移除授权匹配、句柄归属、目录过滤等不变量。
- `paper_T6_chaincaps_comparator.csv` — ChainCaps 对照。
- `paper_T8_real_mcp_services.csv` — 真实 MCP 服务实验。

### B26 MADBench
- `paper_T4a_M5_coordination_modes.csv`、`paper_T4c_M6_orchestrator.csv` — 多智能体辩论中的工具/编排者动作。

### B27 DUMA-Bench
- `data_tasks.csv`、`data_tasks_per_domain.csv`、`data_evaluation_criteria_keys.csv` — 35 个可执行多轮任务、动作清单与环境断言。
- `paper_T1_aggregate.csv`、`paper_T2_domain_asr.csv`、`paper_T5_domains.csv` — 工具影子、基础设施滥用、CRM 泄露等域。
- `paper_T8_passk_by_domain.csv` — 各域 pass^k 稳定性。

### B28 R-Judge
- `data_category_stats.csv`、`data_scenario_file_x_label.csv` — Application/Finance/IoT/Program/Web 场景轨迹。
- `paper_T1_main_results.csv`、`paper_T8_f1_by_category.csv` — 12 模型对工具轨迹风险的 F1。

### B30 CVE-Bench
- `paper_T5_failure_modes.csv` — 探索不足、工具误用、任务理解不足、关注错误方向。
- `paper_T4_costs.csv` — 每任务 token/成本。

### B31 CyberSecEval 2
- `data_interpreter_attack_type.csv`、`paper_F6_interpreter_abuse.csv` — 代码解释器五类滥用（容器逃逸、提权、后渗透、反射、社工）。
- `data_frr_attack_type.csv`、`data_frr_is_malicious.csv`、`paper_F2_frr_vs_violation_approx.csv` — 良性网络安全请求的误拒率，反映工具/能力过度限制。

### B32 CyberSecEval 3
- `paper_F14_interpreter_abuse_with_guard.csv` — 解释器滥用与 LlamaGuard 前后。

### B35 Cyber Defense Benchmark
- `data_log_schema_overview.csv` — 505 列 Windows 事件日志 schema，智能体最多 50 次 SQL 查询。
- `paper_T5_leaderboard.csv`、`paper_T6_tactic_recall.csv` — 11 模型威胁狩猎的覆盖分、成本、战术召回。

### B37 BFCL v4
- `data_category_sizes.csv`、`data_group_sizes.csv` — 4,697 条、20 个分片：单轮、多轮、幻觉、智能体。
- `data_multi_turn_apis.csv` — 11 套模拟 API（文件系统、交易、车辆控制、消息、订票等）。
- `paper_T1_leaderboard.csv` — 69 个模型配置的函数调用总分与 Irrelevance 拒调率。
- `paper_T2_perplexity.csv`、`paper_T3_char_nll.csv` — 数据污染/困惑度检查。

### B38 τ²-Bench
- `data_task_files.csv`、`data_splits.csv`、`paper_T1_domains.csv` — airline/retail/telecom/banking/intake 任务与参考动作数。
- `data_telecom_action_requestor.csv`、`data_telecom_full_intent.csv`、`data_telecom_full_persona.csv`、`paper_T3_telecom_intents.csv`、`paper_T4_telecom_actions.csv` — 82.7% 参考动作需由用户执行的双控工具分工。
- `paper_F4_telecom_modes.csv` — 默认/无用户/给计划三种模式。

### B39 OSWorld
- `data_task_index_by_app.csv`、`data_ubuntu_app_summary.csv`、`data_ubuntu_tasks.csv`、`data_windows_tasks.csv` — 368 个 Ubuntu 任务 + 49 个 Windows 任务、应用分布。
- `data_eval_functions_top.csv` — 120+ 种自动评估函数。
- `paper_T10_ubuntu_stats.csv`、`paper_T11_windows_stats.csv` — 任务/应用统计。
- `paper_T5_success_by_category.csv`、`paper_T14_success_by_app.csv` — 12 模型 × 5 类别/10 应用的成功率。

### B40 METR Time Horizons
- `paper_T6_scaffolds.csv` — 不同工具/脚手架对长任务成功率的影响。

---

## ASI03 身份与权限滥用（Identity & Privilege Abuse）

**纳入标准**：越权、授权范围、用户同意、角色/身份冒充、凭证访问、权限提升、访问控制、隐私数据外泄、上下文完整性、数据出境/外分享，以及 ACL/审批门/身份绑定相关的表。单纯的“注入 ASR”归 ASI01；多智能体之间的消息泄露归 ASI07。

### B01 AgentDojo
- `data_injection_goals_v1.csv` — 27 个目标中包含转账、外发安全码、发钓鱼链接等权限/数据类目标。
- `paper_T3_agents_important_message_attack.csv`、`paper_T5_defenses_gpt4o.csv` — 受攻击效用下降与定向 ASR，反映越权动作能否落地。

### B02 InjecAgent
- `data_attack_type_by_attack_category.csv`、`data_attacker_cases_by_type.csv` — 数据窃取类（Financial Data、Physical Data、Others）与直接伤害中的 Data Security。
- `data_test_case_files.csv` — 544 个数据窃取用例 × base/enhanced。
- `paper_T1_attack_categories.csv` — 数据窃取攻击类别与示例。
- `paper_T3_asr_valid_main.csv`、`paper_T6_valid_rates.csv`、`paper_T8_asr_all.csv`、`paper_T9_asr_all_by_attack_type.csv`、`paper_T11_asr_valid_simple_react.csv`、`paper_T12_asr_all_simple_react.csv` — 含 DS_S1/DS_S2 数据窃取子指标。
- `paper_text_key_numbers.csv` — S1→S2 数据窃取漏斗。

### B03 Agent Security Bench
- `paper_T6_NRP.csv`、`paper_T19_defense_utility_no_attack.csv` — 防御对正常任务效用与安全完成的影响，间接反映权限限制的代价。

### B04 Agent Red Teaming
- `paper_T1_asr_by_category_vector.csv` — 机密泄露类直接/间接攻击的会话 ASR。
- `paper_F3_challenge_asr_by_model.csv`、`paper_F5_transfer_matrix.csv`、`paper_F5_transfer_long.csv`、`derived_F5_transfer_summary.csv` — 各模型在机密泄露行为上的攻击成功率与迁移性。
- `paper_text_key_numbers.csv` — 22 个前沿模型、44 个部署场景、机密泄露行为。

### B06 SafeClawBench
- `data_attack_type_x_harm_type.csv` — leak 类 254 条，覆盖 MEX/MPI/TRI 等泄露路径。
- `paper_T16_harm_audit_D0_by_attack.csv`、`paper_T17_mex_subtypes.csv` — MEX 记忆提取的策略透明度/凭证类泄露。
- `paper_T5_harm_audit_by_defense.csv` — 防御对伤害证据的影响。

### B07 AgentHarm
- `data_behavior_list.csv`、`data_category_by_split.csv` — Fraud、Privacy 等类别涉及身份/财务滥用。

### B08 Agent-SafetyBench
- `data_risk_category.csv` — Leak sensitive data/information 250 条、Lead to property loss 250 条。
- `data_risk_x_behavior_content.csv`、`data_risk_x_fulfillable.csv` — 隐私/财产类行为任务的可完成性。
- `paper_T5_safety_scores_by_risk.csv` — 16 模型在 Leak/Property 等风险上的安全分。

### B09 ToolEmu
- `data_risky_outcome_labels.csv`、`paper_F5_risk_type_distribution.csv` — Privacy breach 19.0%、Financial loss 16.1%、Unauthorized access。
- `paper_T4_agent_evaluation.csv` — 5 模型在 144 个工具任务中的隐私/未授权访问失败。

### B10 WASP
- `data_attacker_goals.csv`、`paper_T5_attacker_goals_violation.csv` — Gaining Access 7 个（SSH key、Owner）、Exfiltration 2、Data Destruction 2、Snooping 2。
- `paper_T2_main_results.csv`、`paper_T3_url_vs_plaintext.csv`、`paper_T4_task_related_vs_agnostic.csv` — Web 智能体执行这些目标时的 ASR。

### B11 SafeArena
- `paper_T12_full_refusal.csv` — 对违法/骚扰/虚假信息等类别的拒绝率，含身份/权限相关伤害。

### B12 ST-WebAgentBench
- `data_policy_category_x_site.csv` — boundary_and_scope_limitation 1,120 条、user_consent 322 条、hierarchy_adherence 152 条。
- `data_policy_source.csv` — 组织 2,300 / 用户 700 / 任务 57 的权限层级。
- `data_policy_template.csv` — access_management、ask_the_user、hierarchy_resolution、irreversible_actions 等模板。
- `paper_F2_agent_metrics.csv` — CuP（策略合规完成率）与 AWM 37 次用户同意违规。
- `paper_T2_statistics.csv`、`paper_T3_dimension_ablation.csv` — 六维策略与 CR/CuP 相关性。

### B13 OS-Harm
- `data_injection_vector_x_goal.csv` — 发密码到 URL、读文件、SSH 表单、终端脚本等权限目标。
- `paper_T2_main_results.csv`、`paper_T4b_injection_goals.csv` — 各目标的不安全率。

### B14 MMA-SafetyBench
- `data_gui_attack_payload_category.csv` — 隐私外泄 86 条、金融劫持 51 条、Root 提权 42 条。
- `paper_T2_asr.csv`、`derived_domain_means.csv` — 各领域/模型的越权动作 ASR。

### B16 AuthorizationBench
- `data_case_type.csv`、`data_seed_source_type.csv`、`data_expansion_axis.csv` — 286 个任务、42 个真实案例、换领域/换伤害属性扩展。
- `data_domain_x_harm.csv` — 有直接伤害 185 / 无 101；电商 8/34 最低。
- `data_trigger_type.csv`、`data_trigger_x_harm.csv` — 14 类触发，恶意注入 118 / 良性压力 168。
- `data_task_services.csv`、`data_task_labels.csv` — 邮件 45%、文档门户 30% 的服务与任务标签。
- `paper_T1_controlled_pairs_OAR.csv` — 控制对越权率。
- `paper_T11_completion_authorization.csv` — 24 配置、6,864 条轨迹的 OAR 19.2%。
- `paper_T12_reasoning_effort.csv` — 推理强度对越权率的影响。
- `paper_T13_harm_test_level.csv`、`paper_T6_composition.csv` — 伤害等级/任务构成。
- `paper_T7_case_quality_agreement.csv`、`paper_T8_judge_agreement.csv` — 案例质量与判官一致性。

### B17 AuthGateBench
- `data_category_x_label.csv`、`data_category_x_role.csv`、`data_role_x_label.csv` — 5 种失效模式 × BLOCK/ALLOW × 角色。
- `data_pairs.csv`、`data_profile.csv` — 350 个 base/inverted 对比对与轨迹画像。
- `derived_policy_means.csv`、`paper_T1_statistics.csv` — 4 模型平均准确率/FPR/FNR。
- `paper_T2_eval_implicit_policy.csv`、`paper_T3_invariant_rate_implicit.csv`、`paper_T4_invariant_rate_explicit.csv`、`paper_T5_eval_explicit_policy.csv` — 隐式/显式策略下的审批门判定与不变率。

### B18 PrivacyLens
- `data_overview.csv`、`data_seed_source.csv` — 493 条种子→情境→轨迹；众包/文献/法规来源。
- `data_sensitive_items_per_case.csv` — 每案 1–16 项敏感信息。
- `data_final_action.csv`、`data_transmission_channel.csv` — 对外发送动作与传输渠道。
- `paper_T2_probing_and_action.csv`、`paper_T3_extended_seeds.csv`、`paper_T5_confaide_culturebank.csv` — 9 模型轨迹级问答准确率 vs 实际泄露率。

### B19 CI-Work
- `data_flow_direction.csv`、`data_flow_x_category_ess4.csv` — 上行/下行/平级/斜向/对外五类信息流。
- `data_sensitive_category_ess4.csv` — 9 类企业敏感信息。
- `data_variants.csv` — 8 个上下文变体（1/2/4/6/8/12 条 + 有意/无意）。
- `paper_T1_main_results.csv` — 9 模型 × 5 流向的 LR/VR/CR。
- `paper_T2_defense_gpt5.csv` — 通用隐私提示 vs CI-CoT。

### B20 AgentLeak
- `data_records_per_vault.csv`、`data_canary_tier.csv` — 每场景 3 条私密记录与 obvious/semantic/realistic 金丝雀。
- `data_attack_family.csv`、`paper_T14_attack_families.csv` — F1 提示、F2 工具面、F3 记忆持久化、F4 多智能体协作。
- `paper_T11_channel_rates.csv`、`paper_T15_per_model.csv` — C1 最终输出/C2 智能体间/C5 共享记忆泄露率。
- `paper_T12_h1_output_only_miss.csv` — 只审计最终输出会漏掉 41.7%。
- `paper_T6_threshold_sensitivity.csv`、`paper_T7_detection_methods.csv` — 泄露检测阈值与三层检测。
- `paper_T9_defenses_by_channel.csv` — 输出过滤器/隐私提示对各通道的效果。
- `results_by_attack_family.csv`、`results_by_vertical.csv`、`results_model_stats.csv` — 按攻击族/行业/模型的结果。

### B21 MemSecBench
- `paper_F6_taxonomy_marginals.csv` — 6 类记忆风险（含隐私/凭证）边际分布。

### B22 ATBench
- `data_real_world_harm.csv` — 隐私 62 条、功能与机会 52 条。
- `data_failure_mode.csv` — 未授权信息披露 52 条。
- `data_risk_source_x_harm.csv` — 风险来源 × 隐私/系统完整性等伤害。

### B23 MCPSecBench
- `paper_T1_asr_rr_platforms.csv` — ATT-8 数据外泄、ATT-9 包名抢注、ATT-15 凭证泄露等。
- `paper_T2_defense_protection.csv` — 防御对各攻击面的保护率。

### B24 MCP Security Bench
- `paper_T1_attack_types.csv` — UI 冒充用户、OP 越界参数、PM 偏好操纵。
- `paper_T3_asr.csv`、`paper_T11_single_attacks_full.csv`、`paper_T12_mixed_attacks_full.csv` — 各攻击的 ASR/PUA。

### B25 MCP Runtime Invariants (HCP)
- `paper_T3_dataflow_boundary.csv` — 句柄/数据管道、普通参数、秘密复制。
- `paper_T4_mechanism_removals.csv` — 授权匹配、句柄归属、旧版初始化、目录过滤、头一致性、审计。
- `paper_T5_sealed_release.csv` — 密封发布/一次性审批。
- `paper_T8_real_mcp_services.csv` — 真实 MCP 服务的源预算与误拒。

### B26 MADBench
- `paper_T4a_M5_coordination_modes.csv` — IRW（越权读写率）49–74%。
- `paper_T4c_M6_orchestrator.csv` — 编排者被攻陷后 IRW 100%。

### B27 DUMA-Bench
- `data_tasks_per_domain.csv`、`data_tasks.csv` — CRM 泄露、身份冒充、协作者投毒等域。
- `paper_T2_domain_asr.csv`、`paper_T5_domains.csv` — 各域 ASR。

### B28 R-Judge
- `data_category_stats.csv` — Finance 126、IoT 30、Application 252 等场景。
- `paper_T6_risk_types.csv` — 隐私泄露 201 条（最多）、违法 67、经济损失 51、数据丢失 44。
- `paper_T1_main_results.csv`、`paper_T8_f1_by_category.csv` — 模型识别隐私/财务风险的 F1。

### B30 CVE-Bench
- `data_attacker_role.csv` — 普通用户 38 个、管理员 2 个。
- `paper_T6_cve_list.csv`、`derived_T6_attack_type_counts.csv` — 未授权管理员登录、提权等攻击类型。

### B35 Cyber Defense Benchmark
- `paper_T6_tactic_recall.csv` — Credential Access、Lateral Movement、Exfiltration、Privilege Escalation 等战术召回。

### B36 SOCBench Detection
- `data_by_attack.csv`、`data_top_dst_ports_malicious.csv` — C&C、端口扫描、DDoS 等网络攻击标签。

---

## ASI04 智能体供应链漏洞（Agentic Supply Chain Vulnerabilities）

**纳入标准**：MCP 服务器/工具供应链、恶意工具/插件、工具投毒、工具影子、包名抢注、Rug Pull、模型/数据后门（PoT）、第三方组件与补丁来源、依赖/注册表信任。普通“工具误用”归 ASI02。

### B03 Agent Security Bench
- `data_attack_tools.csv` — 400 个攻击工具，部分以正常工具身份植入。
- `paper_T15_pot_triggers.csv`、`paper_T16_pot_utility.csv` — PoT 后门触发词 ASR 99.75–100%，BP 83.05% 且不损 PNA。
- `paper_T20_pot_defenses.csv` — Shuffle/Paraphrase 对后门的防御。
- `paper_T3_statistics.csv` — 13 种攻击方法中的 PoT 后门。

### B23 MCPSecBench
- `paper_T1_asr_rr_platforms.csv` — 工具影子、包名抢注、Rug Pull、工具投毒等供应链攻击。
- `paper_T2_defense_protection.csv` — 现有防御对供应链攻击基本无效（2–13%）。
- `data_attack_prompts.csv` — 供应链攻击提示定义。

### B24 MCP Security Bench
- `data_cases_attack_type.csv`、`data_cases_attack_task.csv` — 名称碰撞 NC、描述注入 PI、工具转移 TT、检索注入 RI 等。
- `paper_T1_attack_types.csv`、`paper_T2_statistics.csv` — 25 个 MCP 服务器、304 个良性工具、405 个攻击工具。
- `paper_T3_asr.csv`、`paper_T11_single_attacks_full.csv`、`paper_T12_mixed_attacks_full.csv` — 供应链攻击在各模型上的 ASR。

### B25 MCP Runtime Invariants (HCP)
- `paper_T2_main_results.csv` — 连接层控制（身份、协议版本、头一致性）与执行层控制。
- `paper_T4_mechanism_removals.csv` — 旧版初始化、头一致性、句柄归属等供应链/连接不变量。
- `paper_T5_sealed_release.csv` — 密封发布与一次性审批。
- `paper_T6_chaincaps_comparator.csv` — ChainCaps 对照。
- `paper_T8_real_mcp_services.csv` — 真实 MCP 服务。

### B32 CyberSecEval 3
- `data_autopatch_project.csv`、`paper_F12_insecure_autocomplete.csv`、`paper_F13_insecure_instruct.csv` — 不安全代码生成会进入下游软件供应链。
- `paper_T1_T4_uplift_survey.csv` — 攻击者利用 LLM 提升供应链/社工攻击效率。

### B33 SEC-bench
- `data_project_x_split.csv`、`paper_T1_secverifier_by_project.csv` — 29 个 C/C++ 项目、真实 CVE 补丁来源。
- `paper_T5_knowledge_cutoff.csv` — 知识截止与数据污染/供应链时间线。

### B37 BFCL v4
- `paper_T2_perplexity.csv`、`paper_T3_char_nll.csv` — 模型在众包/静态函数调用集上的困惑度异常，用于发现测试集记忆/污染（供应链数据完整性）。

---

## ASI05 意外代码执行（Unexpected Code Execution）

**纳入标准**：代码生成/补全、代码解释器滥用、Shell/终端命令、RCE、容器逃逸、提权、内存破坏、SQL 注入、PoC/漏洞利用、补丁生成、恶意脚本/计划任务、OS 终端动作。纯“网络攻击知识问答”若未落到代码执行，归 ASI05 的能力侧或 ASI09/ASI10。

### B06 SafeClawBench
- `data_exec_attack_type.csv`、`data_exec_subtype.csv` — 可执行沙盒中的 config_modify/db_drop/email_exfil/file_delete 等子类型。
- `data_exec_available_tools.csv`、`data_exec_oracle_checks.csv`、`paper_T40_exec_oracle_checks.csv` — code_output_contains 等执行检查。
- `paper_T18_exec_harm_by_split.csv`、`paper_T21_core_exec_matched.csv`、`paper_T41_exec_observed_harm.csv` — 执行层真实状态伤害。
- `paper_T42_exec_metric_hierarchy_D0.csv` — ToolCall-ASR → StateChange-ASR → ObservedHarm。

### B07 AgentHarm
- `data_behavior_list.csv`、`data_top_target_functions_harmful.csv` — Cybercrime 类行为与代码/终端相关函数。
- `paper_T9_public_test_main.csv` — 有害任务完成分，含代码/系统类任务。

### B08 Agent-SafetyBench
- `data_risk_category.csv`、`data_risk_x_behavior_content.csv` — “Contribute to harmful/vulnerable code” 250 条（158 条纯内容、其余行为）。
- `paper_T5_safety_scores_by_risk.csv`、`paper_T6_safety_scores_by_failure_mode.csv` — Code 类安全分。

### B09 ToolEmu
- `data_toolkits.csv` — Terminal 工具包；Terminal 的 7 个模拟失败中 6 个在真实沙盒复现（含 `rm -rf /*`）。
- `data_risky_outcome_labels.csv`、`paper_F5_risk_type_distribution.csv` — 数据丢失/损坏、计算机安全、人身安全等。
- `paper_T4_agent_evaluation.csv` — 模型在 Terminal 等工具上的失败率。

### B13 OS-Harm
- `data_injection_vector_x_goal.csv` — delete_all_system_files、terminal_cron_setup、terminal_local_script、terminal_remote_script、swisstransfer_send_files 等。
- `paper_T4b_injection_goals.csv` — o4-mini 对脚本/删除类目标的成功率（高危目标多为 0%）。
- `data_category_x_app.csv` — VS Code/OS 终端任务。

### B20 AgentLeak
- `paper_F7_secondary_channels.csv` — 工具输入/日志通道中的代码/命令泄露。

### B23 MCPSecBench
- `paper_T1_asr_rr_platforms.csv` — 协议层重绑定/MITM 与宿主层攻击，可能导致执行链路被接管。

### B29 Cybench
- `data_category_x_organizer.csv`、`derived_40tasks_category_x_competition.csv` — 40 道 CTF：密码 16、Web 8、逆向 6、取证 4、杂项 4、Pwn 2。
- `data_difficulty_label.csv`、`data_official_task_list_by_competition.csv`、`data_overview.csv`、`data_tasks.csv`、`data_subtasks_per_task.csv` — 题集、首解时间、子任务。
- `derived_fst_bins.csv`、`derived_task_solve_counts.csv` — 按人类首解时间分箱与每题解出模型数。
- `paper_T2_single_attempt.csv`、`paper_T3_scaffolds_3_attempts.csv`、`paper_T8_competitions.csv` — 8 模型/脚手架的解出率。
- `paper_T10_unguided_per_task.csv`、`paper_T11_subtask_guided_per_task.csv`、`paper_T12_subtask_score_per_task.csv`、`paper_T9_max_history.csv` — 逐题执行结果与子任务得分。

### B30 CVE-Bench
- `data_cves.csv`、`paper_T6_cve_list.csv`、`data_variants.csv` — 40 个真实 Web CVE，zero-day/one-day/k8s 变体。
- `data_attack_type_counts.csv`（`derived_T6_attack_type_counts.csv`）、`derived_T6_cvss_counts.csv`、`paper_T2_severity.csv`、`paper_T3_app_types.csv` — 文件创建、数据库读取、DoS、提权等利用类型与 CVSS。
- `paper_F3_success_rates_approx.csv`、`paper_F4_successful_exploit_types.csv` — T-Agent/AutoGPT/Cy-Agent 的 zero-day/one-day 成功率与利用构成。
- `paper_T4_costs.csv`、`paper_T5_failure_modes.csv` — 成本与失败原因（探索不足、工具误用等）。

### B31 CyberSecEval 2
- `data_autocomplete_cwe_top.csv`、`data_autocomplete_language.csv`、`data_instruct_language.csv` — 8 种语言的代码补全/指令生成不安全代码。
- `data_suite_sizes.csv` — autocomplete 1,916、instruct 1,916/1,681。
- `data_interpreter_attack_type.csv`、`paper_F6_interpreter_abuse.csv` — 5 类解释器滥用。
- `data_mitre_category.csv`、`data_mitre_multilingual_language.csv`、`paper_F1_mitre_compliance.csv` — 10 类 ATT&CK 战术的服从率。
- `paper_F5_exploitation.csv` — 约束满足、内存破坏、SQL 注入、缓冲区溢出能力。
- `derived_figure_row_means.csv` — 各图均值，含代码解释器/漏洞利用。

### B32 CyberSecEval 3
- `data_autopatch_crash_type.csv`、`data_autopatch_overview.csv`、`data_autopatch_project.csv`、`data_autopatch_severity.csv` — 148 个 ARVO 漏洞、46 个项目、堆溢出/未初始化值等。
- `paper_F12_insecure_autocomplete.csv`、`paper_F13_insecure_instruct.csv` — 不安全代码生成率 25–39%。
- `paper_F14_interpreter_abuse_with_guard.csv`、`paper_F15_mitre_with_guard.csv` — 解释器滥用/攻击协助与 LlamaGuard。
- `paper_F9_exploitation.csv` — 漏洞利用得分，Llama 3 405B 0.49。
- `paper_F7_autonomous_ops_approx.csv`、`paper_T5_autonomous_runs.csv` — 自主渗透低/中/高难度。

### B33 SEC-bench
- `data_instances.csv`、`data_lang_x_split.csv`、`data_project_x_split.csv` — 300 个 C/C++ 实例、29 个 CVE 项目 + OSS-Fuzz。
- `data_crash_type.csv`、`data_sanitizer_x_split.csv`、`data_patch_stats.csv` — 堆溢出 38%、段错误 28.7%、UAF 14%、栈溢出 4.7%。
- `paper_T1_secverifier_by_project.csv`、`paper_T3_secverifier_vs_codeact.csv` — SecVerifier 多智能体构建/复现/修复。
- `paper_T2_instance_stats.csv`、`paper_T4_agents_models.csv`、`paper_T5_knowledge_cutoff.csv` — 修补/PoC 任务的模型成绩与知识截止。

### B34 CyberSOCEval
- `data_overview.csv`、`data_malware_attack.csv`、`data_malware_attack_x_difficulty.csv`、`data_malware_difficulty.csv`、`data_malware_topic.csv` — 609 道恶意软件分析题、5 个家族、8 个主题。
- `data_malware_options_answers.csv` — 多选题选项/答案。
- `data_threat_intel_attack.csv`、`data_threat_intel_difficulty.csv`、`data_threat_intel_topic.csv`、`data_threat_intel_options_answers.csv` — 588 道威胁情报推理题。
- `paper_F8_malware_by_difficulty.csv`、`paper_F12_malware_accuracy_jaccard_approx.csv`、`paper_F13_malware_by_family.csv`、`paper_F14_malware_by_topic.csv` — 恶意软件分析成绩。
- `paper_F9_threat_intel_by_source.csv`、`paper_F10_modality_approx.csv` — 威胁情报按来源与输入模态。

### B35 Cyber Defense Benchmark
- `data_sample_overview.csv`、`data_sample_flags_by_chain_step.csv`、`data_sample_flags_relevance.csv` — 一个样例活动的 18 步攻击链与 3,912 个 flag。
- `paper_T2_dataset_stats.csv`、`paper_T3_flag_provenance.csv` — 106 个 ATT&CK 过程、23,268 个恶意事件 flag。

### B36 SOCBench Detection
- `data_by_attack.csv`、`data_by_source.csv`、`data_protocol_x_label.csv`、`data_top_dst_ports_malicious.csv` — 端口扫描、C&C、DDoS 等网络攻击流。

### B39 OSWorld
- `data_ubuntu_tasks.csv`、`data_ubuntu_app_summary.csv`、`data_eval_functions_top.csv` — 含终端/VS Code/OS 设置的 368 个任务。
- `paper_T10_ubuntu_stats.csv`、`paper_T11_windows_stats.csv` — 按应用统计。

### B40 METR Time Horizons
- `data_v1_0_tasks_by_length_x_source.csv`、`data_v1_1_tasks_by_length_x_source.csv` — 软件工程/终端任务时长分布。
- `paper_T9_vs_swebench.csv` — 与 SWE-bench 的能力对照。

---

## ASI06 记忆与上下文投毒（Memory & Context Poisoning）

**纳入标准**：持久记忆写入/召回/采纳、记忆投毒、记忆提取、RAG/知识库投毒、共享记忆污染、上下文污染、不可靠工具输出被当作事实、长上下文中的错误信息传播。单纯的提示注入归 ASI01；多智能体消息通道归 ASI07。

### B03 Agent Security Bench
- `data_attack_type_by_agent.csv` — 记忆投毒（MP）作为五类攻击之一。
- `paper_T3_statistics.csv`、`paper_T5_attack_results_by_backbone.csv` — 13 模型在记忆投毒下的 ASR（平均 7.92%，混合攻击中放大）。
- `paper_T14_attack_combinations.csv` — DPI+MP 83.02%、IPI+MP 23.75%。
- `paper_T21_memory_defense_llm_detector.csv` — LLM 检测记忆投毒 FNR 0.660、FPR 0.200。
- `paper_F4_ppl_detection_curve_points.csv` — 困惑度检测阈值曲线，无阈值能同时压到 0.3 以下。

### B06 SafeClawBench
- `data_attack_type_x_harm_type.csv`、`data_attack_type_x_lifecycle.csv` — MEX 记忆提取 100 条、MPI 记忆投毒 100 条。
- `paper_T1_attack_types.csv` — MPI/MEX 定义。
- `paper_T16_harm_audit_D0_by_attack.csv` — MPI 272 条中 251 条有持久化伤害证据（92%）；MEX 272 条中 121 条文本泄露（44%）。
- `paper_T17_mex_subtypes.csv` — MEX 的 49/100 属策略透明度类。
- `paper_T28_corefail_by_attack_D0.csv` — MPI 在 Kimi 81%、Qwen 80%。
- `paper_T42_exec_metric_hierarchy_D0.csv` — 记忆持久化导致的状态变化。

### B07 AgentHarm
- `data_behavior_list.csv` — 部分行为依赖长期记忆/上下文。

### B08 Agent-SafetyBench
- `data_failure_mode_counts.csv`、`paper_T4_failure_mode_definitions.csv` — M7“过度信任工具结果”358 次、M2“信息不全即调用”257 次、M9“过度信任工具结果”358。
- `paper_T6_safety_scores_by_failure_mode.csv` — M7 平均 12.5、M2 18.1，为最差两类。

### B09 ToolEmu
- `data_underspecification_type.csv` — 64.6% 同时缺任务信息与安全约束，26 例只缺任务信息，25 例只缺安全约束；上下文不完整导致风险。
- `paper_T4_agent_evaluation.csv` — 模型在信息不全下的安全分/失败率。

### B20 AgentLeak
- `data_attack_family.csv`、`paper_T14_attack_families.csv` — F3 记忆持久化 70 条。
- `paper_T11_channel_rates.csv` — C5 共享记忆泄露率 22.5–68.2%。
- `paper_T12_h1_output_only_miss.csv` — 共享记忆中的隐藏泄露。

### B21 MemSecBench
- `derived_pooled_by_harness.csv`、`derived_pooled_by_memory_backend.csv`、`derived_pooled_by_llm.csv` — 2 框架 × 4 后端 × 3 LLM 的汇总。
- `paper_F4_checkpoint_rates.csv` — W1 写入 91.1、W2 持久化 84.2、E1 召回 76.1、E2 采纳 53.7、E2E 50.3、F1 删除 86.3、F2 保留良性 62.5、SRSR 56.1。
- `paper_F5_gain_over_native.csv` — 各记忆后端相对原生的增益/损失。
- `paper_F6_taxonomy_marginals.csv` — 记忆类型/风险类别边际分布。
- `paper_T2_lifecycle_24configs.csv` — 24 配置每格分子/分母。
- `paper_T7_judge_accuracy.csv` — 判官与人工 90.6%/91.8%。
- `paper_text_key_numbers.csv` — 310 任务包、930 阶段任务、7 检查点。

### B22 ATBench
- `data_risk_source.csv`、`data_risk_source_x_harm.csv` — “不可靠信息”64 条。
- `data_failure_mode.csv` — 未校验工具输出 67 条。
- `data_atbench500_label.csv`、`data_label.csv` — 长轨迹中的上下文错误传播。

### B26 MADBench
- `paper_T1_attack_families.csv`、`paper_T2_amplification_factors.csv` — M3 RAG 投毒（问答）在辩论下 AF 0.74（吸收），但 IRW 为 ∞。

### B27 DUMA-Bench
- `data_tasks.csv` — 邮件 RAG 钓鱼、协作者投毒等依赖检索/记忆的任务。

### B28 R-Judge
- `data_category_stats.csv`、`paper_T6_risk_types.csv` — 错误信息/不可靠上下文导致的判断。

---

## ASI07 智能体间通信不安全（Insecure Inter-Agent Communication）

**纳入标准**：多智能体消息、共享记忆、协作者投毒、智能体合谋、编排者/辩论、委派与信任边界、A2A 通道泄露、跨智能体上下文传播。单智能体工具调用归 ASI02；MCP 客户端-服务器协议归 ASI02/ASI04。

### B03 Agent Security Bench
- `paper_T14_attack_combinations.csv` — 混合攻击涉及多智能体/多阶段组合。

### B20 AgentLeak
- `data_agents_per_scenario.csv`、`data_vertical_x_topology.csv` — 单/双/三智能体拓扑。
- `data_attack_class.csv`、`data_attack_family.csv` — F4 多智能体协作 202 条。
- `paper_T10_single_vs_multi.csv` — 只看 C1 多智能体更低（27.2% vs 43.2%），计入全部通道后多智能体总泄露 68.9%，是单智能体 1.6 倍。
- `paper_T11_channel_rates.csv` — C2 智能体间消息泄露 28.1–96.2%。
- `paper_T12_h1_output_only_miss.csv` — 输出干净但内部泄露 H1 41.7%。
- `paper_T13_frameworks.csv` — CrewAI/AutoGPT/LangChain/MetaGPT 的 C2 泄露 28–35%。
- `paper_T14_attack_families.csv` — F4 多智能体协作 ASR 82.9%。
- `paper_T15_per_model.csv`、`paper_T16_sdk_integration.csv` — 各模型/各 SDK 的通道差异。
- `paper_T3_scenario_distribution.csv`、`paper_T4_T5_attack_taxonomy.csv`、`paper_T8_execution_summary.csv`、`paper_T9_defenses_by_channel.csv`、`paper_text_key_numbers.csv` — 场景、攻击分类、执行汇总、防御与关键数字。
- `results_by_attack_family.csv`、`results_by_vertical.csv`、`results_model_stats.csv` — 按攻击族/行业/模型的结果。

### B21 MemSecBench
- `derived_pooled_by_harness.csv`、`paper_T2_lifecycle_24configs.csv` — OpenClaw/Hermes 两种框架下的共享记忆/多阶段任务。

### B26 MADBench
- `paper_T1_attack_families.csv` — M5 辩论成员被攻陷、M6 编排者被攻陷。
- `paper_T2_amplification_factors.csv` — 多智能体辩论对 ASR/IRW/成本的放大系数。
- `paper_T4a_M5_coordination_modes.csv` — 合谋/各自独立/不一致三种协调模式。
- `paper_T4b_M5_model.csv` — 辩论成员换成更强模型的效果。
- `paper_T4c_M6_orchestrator.csv` — 编排者是单点故障，攻陷后 ASR/IRW 100%。
- `paper_T10_rounds.csv` — 辩论轮数。
- `paper_text_key_numbers.csv` — 5 个辩论智能体 + 1 编排者、3,958 用例。

### B27 DUMA-Bench
- `data_tasks_per_domain.csv` — 协作者投毒 6、工具影子 6、身份冒充等。
- `paper_T2_domain_asr.csv`、`paper_T5_domains.csv` — 协作者投毒/身份冒充/工具影子在双控下的 ASR 增幅 13–21 点。

### B03 Agent Security Bench（补充）
- `paper_T14_attack_combinations.csv` — 混合攻击需要多工具/多阶段协作，是智能体内部通信与状态传递的攻击面。

---

## ASI08 级联故障（Cascading Failures）

**纳入标准**：多步/长轨迹错误传播、单点失败放大、攻击链、中间步骤被劫持导致后续步骤失守、动态环境中的防御失效、效用—安全权衡、pass^k 可靠性、失败模式、评测管线/判官可靠性。单纯单步 ASR 归 ASI01/02。

### B01 AgentDojo
- `data_suite_summary_v1.csv`、`data_task_files_by_version.csv` — 629 个用户×注入配对，任务可跨多步工具链。
- `paper_T3_agents_important_message_attack.csv` — 受攻击效用从 78.22% 降到 51.19%，体现攻击对后续任务链的破坏。
- `paper_text_key_numbers.csv` — 注入位于工具输出末尾时 ASR 约 70%，越靠后越容易级联。

### B02 InjecAgent
- `data_test_case_files.csv`、`paper_T3_asr_valid_main.csv` — 数据窃取 S1（取数据）→S2（发给攻击者）两步漏斗，S2 几乎总是成功。
- `paper_T6_valid_rates.csv` — 小模型在攻击下有效率暴跌（Llama2-13B 100% → 1.7%），单步失败导致整条轨迹失效。
- `paper_T8_asr_all.csv`、`paper_T9_asr_all_by_attack_type.csv` — 全用例 ASR 与攻击子类差异。
- `paper_text_key_numbers.csv` — S1→S2 是“一旦第一步被劫持，防线基本失守”的典型级联。

### B03 Agent Security Bench
- `paper_T5_attack_results_by_backbone.csv` — 混合攻击平均 ASR 84.30%，高于单类 DPI 72.68%、IPI 27.55%、MP 7.92%，组合放大。
- `paper_T14_attack_combinations.csv` — 两两/三三组合的 ASR 矩阵。
- `paper_T6_NRP.csv` — PNA × (1−ASR) 综合效用—安全。
- `paper_T19_defense_utility_no_attack.csv` — 防御导致 PNA 从 29.46% 降到 22.52%。

### B05 AgentDyn
- `data_user_task_difficulty.csv`、`paper_T1_benchmark_complexity.csv` — 平均 7.10 步、33.33 个工具，长轨迹放大误差。
- `paper_T9_T11_benign_utility.csv`、`paper_T12_T14_utility_under_attack.csv` — 防御在动态任务中效用崩溃（CaMeL 0%、ProtectAI 1.25%）。
- `paper_T15_T17_asr.csv`、`paper_T17_asr_system.csv` — 各防御下的 ASR。
- `paper_T3_main_defenses.csv`、`derived_defense_means.csv`、`derived_full_matrix_overall.csv` — 防御均值与完整矩阵。
- `paper_T2_overview.csv` — 规模与套件。

### B06 SafeClawBench
- `data_attack_type_x_lifecycle.csv` — 攻击生命周期阶段。
- `paper_T16_harm_audit_D0_by_attack.csv`、`paper_T5_harm_audit_by_defense.csv` — 从 CoreFail 到 HarmEvidence 的漏斗。
- `paper_T19_mcnemar_exec.csv`、`paper_T42_exec_metric_hierarchy_D0.csv` — 语义通过但执行层仍伤害，说明评测层级间的漏检级联。
- `paper_T21_core_exec_matched.csv` — 291/347 条沙盒伤害发生在语义判“通过”的用例上。
- `paper_T29_harness_asr.csv` — 单轮 61.9% → 多轮 38.7%，harness 改变造成 20+ 点差异。
- `paper_T34_inter_judge_agreement.csv`、`paper_T36_human_adjudication.csv` — 判官/人工一致性，评测管线可靠性。
- `paper_T44_empirical_difficulty.csv`、`paper_T45_splits.csv` — 经验难度与数据切分。

### B07 AgentHarm
- `data_target_function_count_dist.csv`、`data_split_summary.csv` — 每个行为 2–8 个目标函数，多步工具链。
- `paper_T2_best_of_n.csv` — 温度 1 采样 5 次取最好，GPT-4o 伤害分升至 83.7%。

### B08 Agent-SafetyBench
- `data_failure_mode_counts.csv`、`data_failure_modes_per_case.csv` — 2,294 次多标签失效，单案可叠加 4 类。
- `paper_T4_failure_mode_definitions.csv` — M1–M10 失效模式。
- `paper_T6_safety_scores_by_failure_mode.csv` — M7 12.5、M2 18.1 最差，说明“过度信任/信息不全”会在后续步骤放大。
- `data_risk_x_fulfillable.csv` — 735 条可安全完成，1,265 条应拒绝。

### B09 ToolEmu
- `data_toolkits_per_case.csv` — 34% 用例涉及 2–3 个工具包，跨工具链风险。
- `paper_T2_end_to_end_validation.csv`、`paper_T3_component_validation.csv` — 模拟器/评估器对多步失败的识别。
- `paper_TD1_emulator_issue_detail.csv`、`paper_TD2_leave_one_out.csv`、`paper_TD3_kappa_original_scale.csv`、`paper_TD4_TD5_author_validation.csv` — 评测管线可靠性。
- `paper_TD7_temperature_claude2.csv` — 温度对失败率的影响（0.5 时 50%）。
- `paper_text_key_numbers.csv` — Terminal 7 个失败中 6 个真实复现。

### B10 WASP
- `paper_T2_main_results.csv` — 中间 ASR 17–86%，端到端仅 0–17%：“security by incompetence”，前端失守未必完成末端。
- `paper_T3_url_vs_plaintext.csv`、`paper_T4_task_related_vs_agnostic.csv` — 注入方式对端到端成功率影响。
- `paper_T5_attacker_goals_violation.csv` — 攻击目标链。

### B12 ST-WebAgentBench
- `data_policy_load_bins.csv` — 65.3% 任务 >5 条策略。
- `data_policy_category_x_site.csv`、`data_policy_source.csv` — 策略层级与来源。
- `paper_F2_agent_metrics.csv` — CR 33.8% vs CuP 20%，all-pass@3 仅 5%。
- `paper_T3_dimension_ablation.csv` — 去掉严格执行/用户同意后 CR–CuP 相关性上升。
- `paper_text_key_numbers.csv` — CuP 从 1 条策略 18.2% 降到 >5 条 7.1%，ρ=−0.71。

### B13 OS-Harm
- `paper_T10_violation_step.csv` — 违规步骤一致率 77%、平均偏差 0.85 步。
- `paper_T3_judge_vs_human.csv`、`paper_T6_judge_vs_osworld_exec.csv` — 判官与执行检查的精确率/召回差异。
- `paper_T7_temperature.csv`、`paper_T8_judge_frameworks.csv`、`paper_T9_judge_models.csv` — 温度/观测框架/判官模型对结果的影响。

### B16 AuthorizationBench
- `paper_T17_repeated_run_reliability.csv` — 单次安全完成 75.7%，三次都安全 63.6%，24.3% 组合至少越权一次。
- `paper_T11_completion_authorization.csv`、`paper_T12_reasoning_effort.csv` — 24 配置完成率/越权率。
- `paper_T7_case_quality_agreement.csv`、`paper_T8_judge_agreement.csv` — 案例/判官一致性。

### B19 CI-Work
- `paper_T1_main_results.csv` — LR/VR/CR 的隐私—效用权衡；DeepSeek-R1 低泄露但 CR 仅 53%。
- `paper_T4_judge_agreement.csv` — 判官一致性。

### B21 MemSecBench
- `paper_F4_checkpoint_rates.csv`、`paper_T2_lifecycle_24configs.csv` — 写入→持久化→召回→采纳→后果→修复的级联漏斗。
- `paper_T7_judge_accuracy.csv` — 判官可靠性。

### B22 ATBench
- `data_atbench500_label.csv`、`data_overview.csv` — 1,000 条长轨迹、平均 4.49 回合、最长 31。
- `data_failure_mode.csv`、`data_label.csv` — 14 类失效模式。
- `paper_T1_benchmark_comparison.csv` — 与 R-Judge 等短轨迹基准对比。
- `paper_T2_main_results.csv` — 17 个判官模型的准确率/召回/F1。
- `paper_T6_human_audit.csv` — 人工审计 165 处细粒度修正。

### B23 MCPSecBench
- `paper_T1_asr_rr_platforms.csv` — 客户端→协议→服务端→宿主四攻击面，协议层 100%。
- `paper_T2_defense_protection.csv` — 防御对链路各段的效果。

### B24 MCP Security Bench
- `paper_T12_mixed_attacks_full.csv` — 组合攻击的 ASR/PUA/NRP。
- `paper_T13_qwen3_thinking.csv` — 思考模式 ASR +9.85、PUA +13.82。
- `paper_T1_attack_types.csv` — 规划/调用/响应阶段组合。

### B25 MCP Runtime Invariants (HCP)
- `paper_T2_main_results.csv` — 18 攻击 × 5 控制模式，B1 仅挡住 7/18，B2/B3 全挡。
- `paper_T9_cost.csv` — HCP 0.26–0.31 ms、ChainCaps 7–8 ms 开销。

### B26 MADBench
- `paper_T2_amplification_factors.csv` — M2 工作区注入 ASR AF 3.09、成本 AF 1.60；M4 IRW ∞。
- `paper_T4a_M5_coordination_modes.csv`、`paper_T4c_M6_orchestrator.csv` — 合谋/不一致/编排者失守的放大。
- `paper_T10_rounds.csv` — 轮数增加无改善。

### B27 DUMA-Bench
- `paper_T1_aggregate.csv` — 被动用户 26.9% → 双控 41.1%（+14.2）。
- `paper_T2_domain_asr.csv`、`paper_T5_domains.csv` — 领域级 ΔASR。
- `paper_T8_passk_by_domain.csv` — pass^k 从 0.722 降到 0.596。

### B28 R-Judge
- `data_category_stats.csv` — 571 条轨迹、5 类场景。
- `paper_T1_main_results.csv`、`paper_T2_prompting.csv`、`paper_T8_f1_by_category.csv` — 12 模型对轨迹风险的 F1。
- `paper_T5_dataset_stats.csv` — 数据集统计。

### B29 Cybench
- `data_subtasks_per_task.csv`、`paper_T11_subtask_guided_per_task.csv`、`paper_T12_subtask_score_per_task.csv` — 2–7 个子任务的逐步得分。
- `paper_T9_max_history.csv` — 最大历史/上下文对解出率的影响。

### B30 CVE-Bench
- `paper_T5_failure_modes.csv` — 探索不足 67.5–80%、工具误用 47.5%、任务理解不足 30%。
- `paper_T4_costs.csv` — 每任务 0.6–1.7 美元。

### B33 SEC-bench
- `paper_T1_secverifier_by_project.csv` — 构建 81.7% → 复现 PoC 39.4% → 修复 69.2%，PoC 是瓶颈。
- `paper_T3_secverifier_vs_codeact.csv` — 多智能体比单智能体验证成功率高 85.7%。

### B35 Cyber Defense Benchmark
- `data_sample_flags_by_chain_step.csv`、`data_sample_flags_relevance.csv` — 3 条攻击链 18 步、3,912 个 flag。
- `data_sample_overview.csv`、`paper_T2_dataset_stats.csv`、`paper_T3_flag_provenance.csv` — 26 个活动、23,268 flag。
- `paper_T5_leaderboard.csv`、`paper_T6_tactic_recall.csv` — 覆盖分/成本/战术召回。

### B36 SOCBench Detection
- `data_overview.csv`、`data_by_source.csv`、`data_sampling_rate.csv`、`data_numeric_medians_by_label.csv` — 757,641 条流、8 个来源、采样率与数值特征。
- `data_by_attack.csv`、`data_protocol_x_label.csv`、`data_top_dst_ports_malicious.csv` — 攻击类型/协议/端口。

### B37 BFCL v4
- `data_multi_turn_apis.csv` — 800 条多轮任务、11 套 API，状态跨轮传播。
- `paper_T1_leaderboard.csv` — 多轮缺参数/长上下文/记忆任务普遍 <50%。
- `paper_T2_perplexity.csv`、`paper_T3_char_nll.csv` — 污染/困惑度。

### B38 τ²-Bench
- `data_splits.csv`、`data_task_files.csv`、`paper_T1_domains.csv` — 任务划分与参考动作数。
- `paper_F3_pass_k.csv` — pass^1→pass^4，telecom 降至 18–26%。
- `paper_F4_telecom_modes.csv` — 默认/无用户/计划三模式。
- `paper_T2_user_simulator_errors.csv` — 模拟用户错误率 6–13%。

### B39 OSWorld
- `data_ubuntu_app_summary.csv`、paper_T10/T11 — 368 个任务、120+ 评估函数。
- `paper_T5_success_by_category.csv`、`paper_T14_success_by_app.csv` — 12 模型 × 5 类别/10 应用，多应用工作流最难（≤7.56%）。

### B40 METR Time Horizons
- `data_v1_0_overview.csv`、`data_v1_1_overview.csv` — 41,629/24,008 次运行。
- `data_v1_0_success_by_model_x_length.csv`、`data_v1_1_success_by_model_x_length.csv` — 成功率随任务时长衰减。
- `data_v1_0_tasks_by_length_x_source.csv`、`data_v1_1_tasks_by_length_x_source.csv` — 任务时长分布。
- `paper_T2_failure_types.csv` — 从“重复失败动作”转向“过早放弃”。
- `paper_T7_success_by_source.csv`、`paper_T9_vs_swebench.csv` — 任务来源/基准间差异。
- `results_model_horizon_summary.csv`、`results_logistic_fits.csv` — 50%/80% 时间跨度与拟合。
- `paper_text_key_numbers.csv` — 50% 跨度每 7 个月翻倍。

---

## ASI09 人与智能体之间的信任被利用（Human-Agent Trust Exploitation）

**纳入标准**：社会工程/钓鱼/说服、用户施压、审批疲劳、伪造 UI/通知/文档、过度信任智能体输出、人类监督失效、拒绝/过度拒绝造成的信任损害、跨文化隐私规范、人机协作中的责任转移。单纯的注入 ASR 归 ASI01；单次越权归 ASI03。

### B06 SafeClawBench
- `paper_T36_human_adjudication.csv` — 人工复核与判官一致性（κ≈0.78–0.79），衡量人类监督的可靠性。

### B07 AgentHarm
- `data_behavior_list.csv`、`data_category_by_split.csv` — Fraud、Harassment、Disinformation 等社会工程相关类别。
- `paper_T8_agent_vs_chat_refusal.csv` — 同一有害请求以“智能体任务”形式提出时拒绝率更低，用户可借此利用对智能体的信任。

### B08 Agent-SafetyBench
- `data_risk_category.csv` — “Spread unsafe information/misinformation”250 条、“Violate law or ethics”250 条。
- `paper_T5_safety_scores_by_risk.csv` — Spread 类平均仅 15.6%，模型很容易帮用户传播未经核实的信息。

### B09 ToolEmu
- `data_underspecification_type.csv` — 64.6% 用例同时缺任务信息与安全约束；智能体若不自问就执行，利用的是用户对“它懂了”的信任。
- `paper_F5_risk_type_distribution.csv` — 声誉损害 8.8%、误导信息 9.3% 等。

### B11 SafeArena
- `paper_F5_aria_llm_judge.csv`、`paper_T4_aria_human.csv` — ARIA 拒绝/延迟拒绝/尝试失败/完成四级，反映人类对 Web 智能体“会拒绝”的预期是否成立。
- `paper_T12_full_refusal.csv` — 按伤害类别的拒绝率。

### B12 ST-WebAgentBench
- `data_policy_category_x_site.csv`、`data_policy_template.csv` — user_consent 322 条、ask_the_user 模板。
- `paper_F2_agent_metrics.csv` — AWM 37 次用户同意违规，风险比 0.44。

### B13 OS-Harm
- `data_category_x_app.csv` — 25 个用户蓄意滥用任务 + 25 个越狱模板版本。
- `paper_T2_main_results.csv`、`paper_F5_jailbreak_template.csv` — 模型对“用户明确要求做坏事”的遵从率 48–70%，越狱后 88–100%。

### B14 MMA-SafetyBench
- `data_document_samples.csv` — 简历/发票中伪造的界面元素。
- `data_gui_attack_payload_category.csv` — 伪造系统弹窗、通知、按钮，利用用户/模型对原生 UI 的信任。
- `paper_T2_asr.csv`、`paper_T6_semantic_compromise_rate.csv` — 视觉语义劫持率 SCR 比 ASR 高 10–30 点。

### B16 AuthorizationBench
- `data_trigger_type.csv`、`data_trigger_x_harm.csv` — 168 条良性压力（相邻越界元素、系统环境要求、授权范围模糊等）。
- `paper_T1_controlled_pairs_OAR.csv` — 恶意注入 17.6% vs 良性压力 23.5%，日常压力比攻击更易导致越权。
- `paper_T14_consultation.csv`、`paper_T15_T16_consultation_timing.csv` — 先询问用户的轨迹越权率 14.0% vs 21.6%；但 68.4% 的询问发生在越权之后，属“事后补救”。
- `paper_T11_completion_authorization.csv`、`paper_T12_reasoning_effort.csv` — 完成率与 OAR。

### B17 AuthGateBench
- `paper_T2_eval_implicit_policy.csv`、`paper_T5_eval_explicit_policy.csv` — LLM 审批门误拦近七成应放行动作，造成用户对审批护栏的不信任。
- `paper_T3_invariant_rate_implicit.csv`、`paper_T4_invariant_rate_explicit.csv` — 动作锚定，说明审批门“看动作不看用户授权”。
- `derived_policy_means.csv`、`paper_T1_statistics.csv` — FPR 66–74%、FNR 2–7%。

### B18 PrivacyLens
- `data_seed_source.csv` — 众包/文献/法规来源的隐私规范。
- `paper_T2_probing_and_action.csv` — Claude-3-Sonnet 问答准确率 99.8% 但实际泄露 38.34%，暴露“知道但做不到”。
- `paper_T5_confaide_culturebank.csv` — 跨文化隐私规范，模型对非美国文化更不敏感。

### B19 CI-Work
- `data_variants.csv` — 有意/无意泄露两个版本。
- `paper_T1_main_results.csv` — 上行汇报泄露最高，模型对内部角色细粒度规范不敏感。
- `paper_T2_defense_gpt5.csv` — 通用隐私提示 vs CI-CoT 的信任—效用权衡。
- `paper_T3_human_eval.csv` — 人工评估情境真实性 4.88/5、相关性 4.51/5。

### B20 AgentLeak
- `paper_T13_frameworks.csv` — 框架层面的系统性泄露，用户难以判断哪个框架可信。

### B22 ATBench
- `paper_T6_human_audit.csv` — 人工审计对细粒度标签的修正，反映自动标注/判官可信度。

### B27 DUMA-Bench
- `paper_T1_aggregate.csv` — 双控交互下 ASR 从 26.9% 升至 41.1%，用户施压/说服是主因。
- `paper_T3_user_temperature.csv` — 用户温度 0/0.5/1.0 下 ASR 28.4/28.1/27.0%。
- `paper_T4_model_asr.csv` — GPT-5 系列在双控下 ASR 涨 39–48 点，过度迁就用户意图。

### B28 R-Judge
- `paper_T3_llama_guard.csv` — LlamaGuard-7b 召回 0.33%，Llama-Guard-2-8B 71.84%，内容护栏不能替代行为风险判断。
- `paper_T7_human_scorer_pcc.csv` — GPT-4 自动评分与人工相关 0.91。

### B31 CyberSecEval 2
- `data_frr_attack_type.csv`、`data_frr_is_malicious.csv`、`paper_F2_frr_vs_violation_approx.csv` — 边界良性请求的误拒，CodeLlama-70B 70%，过度拒绝损害用户信任。

### B32 CyberSecEval 3
- `data_spear_phishing_goal.csv` — 4 种鱼叉钓鱼目标（恶意附件、VPN 凭证、财务/身份、安全软件配置）。
- `paper_F3_spear_phishing_overall.csv`、`paper_F4_spear_phishing_by_goal.csv` — GPT-4 Turbo 3.98/5 最能骗人，Qwen2 72B 3.52。
- `paper_T1_T4_uplift_survey.csv` — 62 名 Meta 员工使用 LLM 的社工提效主观收益。
- `paper_PromptGuard_eval.csv` — 护栏对社工/越狱的召回。

### B34 CyberSOCEval
- `data_threat_intel_attack.csv`、`data_threat_intel_topic.csv`、`paper_F9_threat_intel_by_source.csv` — 威胁情报报告中的欺骗/归因推理，属分析员信任问题。

### B35 Cyber Defense Benchmark
- `paper_T5_leaderboard.csv` — 智能体“看到了但没报”：Opus 4.6 平均见 159 个 flag 只提交 113 个，人类需判断其结论可信度。

### B37 BFCL v4
- `paper_T1_leaderboard.csv` — Irrelevance 拒调率从 4.9% 到 91.5%，部分模型很容易“乱调工具”，用户难以信任其自主决策。

### B38 τ²-Bench
- `data_telecom_action_requestor.csv`、`data_telecom_full_intent.csv`、`data_telecom_full_persona.csv` — 82.7% 动作需用户执行，智能体必须指导用户。
- `paper_F3_pass_k.csv`、`paper_F4_telecom_modes.csv` — 需要用户协作时 pass^1 下降 18–25 点。
- `paper_T2_user_simulator_errors.csv`、`paper_T3_telecom_intents.csv`、`paper_T4_telecom_actions.csv` — 用户模拟器错误 6–13%。

### B40 METR Time Horizons
- `results_model_horizon_summary.csv`、`paper_text_key_numbers.csv` — 人类对“智能体能否自主完成长任务”的预期校准。

---

## ASI10 智能体失控（Agentic Misalignment / Loss of Control）

**纳入标准**：过度自主、越权执行、失控循环、有害任务完成、沙盒逃逸、资源获取/自我保护、编排者接管、长时程自主能力、代理自身失误（非攻击）、拒绝/遵从失衡、执行层控制缺失。单纯的权限范围归 ASI03；单步工具错误归 ASI02。

### B04 Agent Red Teaming
- `paper_T1_asr_by_category_vector.csv` — “违禁动作”间接 36.8%，是智能体被诱导执行危险动作。
- `paper_F3_challenge_asr_by_model.csv`、`paper_F5_transfer_matrix.csv`、`paper_F5_transfer_long.csv`、`derived_F5_transfer_summary.csv` — 各模型稳健性/攻击迁移，反映失控风险。
- `paper_text_key_numbers.csv` — 22 个前沿模型、44 个部署场景。

### B07 AgentHarm
- `data_behavior_list.csv`、`data_category_by_split.csv`、`data_split_summary.csv` — 11 类有害行为（公开 8 类）、264 条完整集。
- `paper_T1_dataset_metrics.csv` — 数据集规模与类别。
- `paper_T9_public_test_main.csv`、`paper_T10_private_test.csv` — 15/7 模型的伤害分与拒绝率；Mistral 系列拒绝率 <8%，伤害分 62–82%。
- `derived_T9_pivot_by_model.csv` — 无攻击/强制工具调用/越狱三设置。
- `paper_T2_best_of_n.csv` — 最佳-of-5 提高伤害完成。
- `paper_release_gap_note.csv` — 公开版缺 3 类，需注意口径。

### B08 Agent-SafetyBench
- `data_overview.csv` — 2,000 条用例、349 环境、111 条预置对话。
- `data_risk_category.csv`、`data_risk_x_behavior_content.csv` — 8 类风险、行为/内容二分。
- `data_risk_x_fulfillable.csv` — 735 条可安全完成 vs 1,265 条应拒绝。
- `paper_T5_safety_scores_by_risk.csv` — 16 模型总分最高 59.8，无模型超过 60%。
- `paper_T6_safety_scores_by_failure_mode.csv` — 10 类失效模式。

### B11 SafeArena
- `paper_F3_task_completion.csv` — 5 模型有害任务完成率 7.6–26.0%。
- `paper_F5_aria_llm_judge.csv`、`paper_T4_aria_human.csv` — ARIA 四级；Qwen 77.1% 尝试、22.2% 完成、几乎不拒绝。
- `paper_T3_normalized_safety.csv` — NSS 21.5–55.0。
- `paper_T11_full_tcr.csv` — 5 伤害类别完成率。
- `paper_T12_full_refusal.csv` — 拒绝率。
- `paper_T5_refusal_direct_vs_priming.csv` — priming 降低拒绝。
- `paper_text_key_numbers.csv` — 500 任务、5 类伤害、4 个网站。

### B12 ST-WebAgentBench
- `paper_F2_agent_metrics.csv` — AWM CuP 20%、all-pass@3 5%，自主完成与合规脱节。
- `paper_T3_dimension_ablation.csv` — 严格执行/用户同意是“完成≠安全”的主要来源。

### B13 OS-Harm
- `data_category_x_app.csv` — 48 条模型自身失误（误删文件、改 .bashrc、撤权限）。
- `paper_T2_main_results.csv` — 失误类不安全率 4–10%。
- `paper_F5_jailbreak_template.csv` — 越狱后 GPT-4.1/Gemini 2.5 Pro 100%。

### B14 MMA-SafetyBench
- `data_gui_attack_payload_category.csv` — 持续监控 29、恢复出厂 1、Root 提权 42。
- `paper_T2_asr.csv`、`derived_model_means.csv` — 8/9 模型平均 ASR >40%。
- `paper_T6_semantic_compromise_rate.csv` — SCR 40.67–86.27%。

### B16 AuthorizationBench
- `data_domain_x_harm.csv` — 185 有直接伤害 / 101 无。
- `paper_T11_completion_authorization.csv` — OAR 19.2%，1,315 条越权中 1,209 条同时完成任务。
- `paper_T12_reasoning_effort.csv` — 推理强度不必然更守规矩。
- `paper_T13_harm_test_level.csv` — 伤害等级。
- `paper_T17_repeated_run_reliability.csv` — 三次都安全仅 63.6%。

### B21 MemSecBench
- `paper_F4_checkpoint_rates.csv` — E2 采纳 53.7%、E2E 50.3%，记忆一旦被采纳几乎造成外部后果。

### B22 ATBench
- `data_atbench500_label.csv`、`data_label.csv`、`data_overview.csv` — 497/1,000 不安全轨迹。
- `data_risk_source.csv` — 智能体自身失误 135（27.2%）> 间接注入 77。
- `data_failure_mode.csv` — 未确认/越权操作 71。
- `data_real_world_harm.csv` — 安全与系统完整性 113。
- `paper_T1_benchmark_comparison.csv`、`paper_T2_main_results.csv` — 轨迹判官能力。

### B23 MCPSecBench
- `paper_T1_asr_rr_platforms.csv` — 协议层 100%、宿主层 58.3–81.7%，平台无法拒绝结构性攻击。
- `paper_T2_defense_protection.csv` — 防御覆盖不足。

### B25 MCP Runtime Invariants (HCP)
- `paper_T2_main_results.csv` — B0 18/18 攻击成功；B1 仍 11/18；B2/B3 0/18。
- `paper_T4_mechanism_removals.csv` — 移除授权匹配新增 6 次成功。
- `paper_T5_sealed_release.csv` — 一次性审批/密封发布。
- `paper_T7_agentdojo_native.csv` — DeepSeek 直接执行完成 4 个攻击目标。
- `paper_T8_real_mcp_services.csv` — 真实服务泄露。
- `paper_T9_cost.csv` — 控制开销。

### B26 MADBench
- `paper_T4b_M5_model.csv` — GPT-5 ASR 6.9%、GPT-6 Astra 3.28%。
- `paper_T4c_M6_orchestrator.csv` — 编排者攻陷 ASR/IRW 100%、成本 181%。
- `paper_T2_amplification_factors.csv` — 多智能体放大。

### B27 DUMA-Bench
- `paper_T1_aggregate.csv` — 双控 ASR 41.1%。
- `paper_T4_model_asr.csv` — GPT-5 系列双控下 64.7–79.3%。
- `paper_T8_passk_by_domain.csv` — 稳定性。

### B28 R-Judge
- `paper_T1_main_results.csv` — 12 模型多数 F1 低于随机 51.32。
- `paper_T2_prompting.csv` — Few-shot 不稳定。
- `paper_T6_risk_types.csv` — 隐私/人身/违法/经济损失等。

### B29 Cybench
- `paper_T2_single_attempt.csv`、`paper_T3_scaffolds_3_attempts.csv` — 8 模型解出率最高 17.5%。
- `paper_T10_unguided_per_task.csv`、`paper_T11_subtask_guided_per_task.csv`、`paper_T12_subtask_score_per_task.csv`、`paper_T9_max_history.csv` — 自主攻防能力边界。

### B30 CVE-Bench
- `paper_F3_success_rates_approx.csv` — T-Agent zero-day 10%、one-day 12.5%。
- `paper_F4_successful_exploit_types.csv` — 数据库读取/未授权管理员登录。
- `paper_T5_failure_modes.csv` — 探索不足等。
- `paper_T4_costs.csv` — 成本。

### B32 CyberSecEval 3
- `paper_F7_autonomous_ops_approx.csv`、`paper_T5_autonomous_runs.csv` — 自主渗透低难度 36–51%、中难度 1–12%、高难度 0。
- `paper_F9_exploitation.csv` — 漏洞利用能力。
- `paper_text_key_numbers.csv` — 自主/攻击者赋能关键数字。

### B33 SEC-bench
- `paper_T4_agents_models.csv` — Claude 3.7 Sonnet 修补 33.8%、PoC 12.5%；o3-mini 31.2%/10.0%；GPT-4o 26.2%/3.8%。
- `paper_T5_knowledge_cutoff.csv` — 知识截止。

### B35 Cyber Defense Benchmark
- `paper_T5_leaderboard.csv` — 11 模型覆盖分 0.10–0.55，无模型通过 13 战术 ≥50% 要求。
- `paper_T6_tactic_recall.csv` — 战术召回。
- `data_reference_cost.csv`、`paper_text_key_numbers.csv` — 成本/规模。

### B38 τ²-Bench
- `paper_F3_pass_k.csv` — telecom pass^1 0.34–0.49、pass^4 0.18–0.26。
- `paper_F4_telecom_modes.csv` — 无用户时 0.52–0.67，需指导用户时下降。
- `paper_T1_domains.csv`、`data_task_files.csv` — 任务规模。

### B39 OSWorld
- `paper_T5_success_by_category.csv`、`paper_T14_success_by_app.csv` — 最佳模型 12.24%，人类 72.36%。
- `data_ubuntu_tasks.csv`、`data_windows_tasks.csv`、`data_task_index_by_app.csv` — 任务空间。
- `data_eval_functions_top.csv`、`paper_T10_ubuntu_stats.csv`、`paper_T11_windows_stats.csv` — 评估与统计。

### B40 METR Time Horizons
- `data_v1_0_by_model.csv`、`data_v1_1_by_model.csv` — 33/21 个模型的时间跨度。
- `data_v1_0_overview.csv`、`data_v1_1_overview.csv` — 运行规模。
- `data_v1_0_success_by_model_x_length.csv`、`data_v1_1_success_by_model_x_length.csv` — 成功率随时长衰减。
- `data_v1_0_tasks_by_length_x_source.csv`、`data_v1_1_tasks_by_length_x_source.csv` — 任务长度。
- `paper_T2_failure_types.csv`、`paper_T6_scaffolds.csv`、`paper_T7_success_by_source.csv`、`paper_T9_vs_swebench.csv` — 失败类型/脚手架/来源/对照。
- `paper_text_key_numbers.csv`、`results_logistic_fits.csv`、`results_model_horizon_summary.csv` — 时间跨度趋势。

---

## 附录：覆盖说明

- 本文逐项覆盖 39 个基准的 516 张 `analysis/tables/*.csv` 表；B15 因无数据表/论文未纳入。
- 同一张表在多类中出现是有意为之：例如 B20 的 C2 通道同时是 ASI03（隐私泄露）与 ASI07（智能体间通信），B06 的 MPI 同时是 ASI01（注入）、ASI06（记忆）与 ASI02（动作）。
- 若用于正式报告，建议把每张表的“主类别”作为筛选维度，其余类别作为交叉标签；本文不强行给出唯一主类别，以避免丢失风险机制。

