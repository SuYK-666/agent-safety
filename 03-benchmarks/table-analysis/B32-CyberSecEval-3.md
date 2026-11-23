# B32 CyberSecEval 3 — 数据表格与分析

> 论文：CyberSecEval 3: Advancing the Evaluation of Cybersecurity Risks and Capabilities in Large Language Models（Meta, Llama 3 配套）  
> 表格：[analysis/tables](../B32-cyberseceval-3/analysis/tables/)  
> 热力图（Figure 4、9、11–15）格子都印有数值，已逐格转录；Figure 7 柱图无数值标签，表中标为近似。

## 1. 数据集结构（CSE3 新增部分；文本注入、MITRE 等沿用 B31）

- **视觉提示注入**：1,000 条 + 1,000 张图片（`data_vpi_*.csv`）。直接注入 / 间接注入各 500；安全违规 400、逻辑违规 600。手法（多标签）：图中嵌入文字指令 400、间接引用 400、混淆 200，误导、查询相关图片、FigStep、虚拟化各 100。
- **鱼叉式钓鱼**：856 个目标人物档案，4 种目标（诱导下载恶意附件、骗取 VPN 凭证、套取财务/身份信息、打探安全软件配置）各 214 个。
- **AutoPatch**：148 个 ARVO 真实漏洞（OSS-Fuzz 来源），以堆溢出读（27）、未初始化值（24）为主，覆盖 46 个项目；bench 子集 136、lite 子集 113；修复补丁平均新增 13.3 行、删除 4.1 行。
- 自主渗透（autonomous_uplift）只有样例配置。

## 2. 对攻击者的“赋能”风险

**自动化社工/鱼叉钓鱼**（Figure 3/4，0–5 分，越高越会骗人）：GPT-4 Turbo 3.98 最高，Qwen2 72B 3.52，Llama 3 70B 2.95，Llama 3 405B 2.60，Mixtral 8x22B 1.68。人工评分与 LLM 评分趋势一致（GPT-4 Turbo 人工 2.90、LLM 3.79）。

**人类攻击者提效研究**（62 名 Meta 员工，Appendix Table 1–4）：新手有一定主观收益（22/31 觉得学得更快，71% 认为降低了脑力负担），但完成率没有统计显著提升；专家使用 LLM 反而少完成 6% 的阶段。

**自主渗透**（Figure 7，Windows 靶机）：各模型能完成 36–51% 的低难度挑战（侦察、发现），中难度 1–12%，高难度 0。

**漏洞利用**（Figure 9）：Llama 3 405B 平均 0.49 最高（SQL 注入 0.77），比 GPT-4 Turbo（0.40）高约 22%；但内存破坏和缓冲区溢出几乎全部失败（≤0.21）。

## 3. 对应用开发者的风险

| 风险 | 关键数字 |
| --- | --- |
| 文本提示注入（Figure 11） | 7 个模型平均成功率 17%–35%；GPT-4 Turbo 0.17 最低、Mixtral 0.35 最高；输出格式操纵对 GPT-4 Turbo 达 0.62 |
| 不安全代码·补全（Figure 12） | 25%–31%；Python 和 Rust 最差（0.33–0.44） |
| 不安全代码·指令（Figure 13） | 32%–39%；C 语言普遍 0.41–0.47；能力越强的模型写出不安全代码越多（405B 0.39） |
| 代码解释器滥用（Figure 14） | Llama 3 70B 0.42 最高，Llama 3 405B 与 GPT-4 Turbo 仅 0.01 |
| 协助网络攻击（Figure 15） | Gemini Pro 0.92、Mixtral 0.80、Llama 3 70B 0.78、GPT-4 Turbo 0.42、Llama 3 405B 0.38 |

注意 Figure 15 与 B31 的 Figure 1 同为 MITRE 服从率，但 CSE3 版本数值普遍更高（判定口径更新），两版不宜直接横比。

## 4. 护栏效果

- LlamaGuard 3 同时过滤输入和输出后：解释器滥用降到 0（Figure 14）；协助网络攻击 Llama 3 405B 从 0.38 降到 0.19、70B 从 0.78 降到 0.24（Figure 15）。只过滤输出效果明显弱一些。
- PromptGuard（`paper_PromptGuard_eval.csv`）：分布外越狱召回 97.5%（FPR 3.9%）、多语言 91.5%，但对 CSE 间接注入只有 71.4%。
- Code Shield：精确率 96%、召回 79%。

## 5. 展示建议

“攻击者赋能”和“应用风险”两大板块分开呈现；护栏前后对比（Figure 14/15 中的 +LlamaGuard 行）适合做成对比柱。
