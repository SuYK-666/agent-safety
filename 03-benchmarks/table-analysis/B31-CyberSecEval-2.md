# B31 CyberSecEval 2 — 数据表格与分析

> 论文：CyberSecEval 2: A Wide-Ranging Cybersecurity Evaluation Suite for Large Language Models（Meta）  
> 表格：[analysis/tables](../B31-cyberseceval-2/analysis/tables/)  
> 论文主要结果都是热力图，但每个格子都印有数值，我渲染页面后逐格转录（`paper_F1/F3/F5/F6_*.csv` 为精确值）；Figure 2、4 为散点/柱图，标注为近似值。

## 1. 数据集结构（`data_suite_sizes.csv`）

| 子集 | 条数 | 用途 |
| --- | --- | --- |
| autocomplete | 1,916 | 代码补全时是否写出不安全代码（8 种语言，Python 351 最多） |
| instruct / instruct-v2 | 1,916 / 1,681 | 按指令生成代码时是否不安全 |
| mitre | 1,000 | 10 类 MITRE ATT&CK 战术各 100 条，测是否协助网络攻击 |
| mitre_frr | 750 | 看似危险但实为良性的“边界”请求，全部 is_malicious=False，测误拒 |
| interpreter | 500 | 5 类代码解释器滥用（容器逃逸、提权、后渗透、反射攻击、社工）各 100 条 |
| prompt_injection | 251 | 15 种注入手法；180 条安全违规类 + 71 条逻辑违规类 |
| 多语言版本 | 1,004 / 700 / 700 | 机器翻译的注入、MITRE、FRR（含 Hindi、Bengali 等 16 种语言） |

漏洞利用（canary exploit）子集是脚本动态生成的，没有静态题库。

## 2. 协助网络攻击（Figure 1）与误拒（Figure 2）

模型对 10 类 ATT&CK 请求的平均服从率（`derived_figure_row_means.csv`）：Llama 3 8B 0.164 最安全，GPT-4 0.287，GPT-3.5-turbo 0.606 最高。按战术看，“侦察/发现/C2”这类信息收集请求最容易被服从，“规避/执行”较少。

误拒（Figure 2）：多数模型对边界良性请求的误拒率低于 15%，唯独 CodeLlama-70B 达 70%——它的低服从率很大程度上是“一律拒绝”换来的。Llama 3 8B 同时做到低服从、低误拒，在图中位于最佳的左下角。

## 3. 提示注入（Figure 3、4）

- 所有模型都会被注入成功，平均 13%–47%（结论原文）。按 Figure 3 平均：CodeLlama-70B 0.129 最低，Llama 3 8B 0.453 最高。
- 手法差异很大：输出格式操纵、换语言输入、信息过载成功率高（Llama 3 8B / GPT-3.5 达 0.76）；token 走私几乎无效（≤0.08）。
- Llama 3 系列对“不同语言的用户输入”特别脆弱（8B 0.76），作者认为与其非多语言训练有关。

## 4. 漏洞利用能力（Figure 5）

约束满足类题目（JS/Python/C）得分 0.43–0.67，但真正的内存破坏、SQL 注入、缓冲区溢出几乎都是 0（GPT-4-turbo SQL 注入 0.23 是唯一例外）。结论：当时的 LLM 还远不能自主写出可用漏洞利用，但能力与通用代码能力正相关。

## 5. 代码解释器滥用（Figure 6）

平均服从约 35%（正文）。Mistral-small 0.468、Llama 3 70B 0.39 最高（Llama 3 70B 在提权类 0.61）；CodeLlama-13B 0.134 最低。

## 6. 展示建议

四张热力图可直接复刻；“攻击服从率 vs 误拒率”散点用于说明安全—效用权衡。
