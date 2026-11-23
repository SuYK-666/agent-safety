# B33 SEC-bench — 数据表格与分析

> 论文：SEC-bench: Automated Benchmarking of LLM Agents on Real-World Software Security Tasks（NeurIPS 2025 D&B）  
> 表格：[analysis/tables](../B33-sec-bench/analysis/tables/)

## 1. 数据集结构

两个公开评测集共 300 个实例（`data_instances.csv`）：eval-cve 200 个（与论文完全对应，来自 29 个 C/C++ 开源项目的真实 CVE）+ eval-oss 100 个（OSS-Fuzz 漏洞）。全部是 C/C++，几乎都用 AddressSanitizer（295/300）。

- 崩溃类型（`data_crash_type.csv`，由 sanitizer 报告解析）：堆溢出 38%、段错误 28.7%、释放后使用 14%、栈溢出 4.7%。
- 项目分布（`data_project_x_split.csv`）：eval-cve 中 gpac 43、imagemagick 31、mruby 21、libredwg 20 最多。
- 修复补丁（`data_patch_stats.csv`）：eval-cve 平均改动 19.1 行（中位数 8，最多 650）、1.3 个文件；漏洞报告平均 481 词。论文 Table 2 口径：问题描述平均 921 词（含调用栈），代码库平均 48 万行。

每个实例都附带可复现的 Docker 环境、构建脚本和 sanitizer 报告（本包未收录镜像）。

## 2. 数据集是怎么造出来的（Table 1、3）

作者用多智能体“SecVerifier”（构建→复现 PoC→修复）自动验证 898 个种子漏洞，只有 200 个（22.3%）通过；三个阶段成功率分别为 81.7%、**39.4%**、69.2%，复现 PoC 是最大瓶颈。php 只有 4.2% 通过，upx 12%。多智能体比单智能体 CodeAct 的验证成功率高 85.7%（26.0% vs 14.0%）。

## 3. 主结果：代码智能体能否完成安全任务（Table 4，80 个实例）

| 任务 | 模型 | SWE-agent | OpenHands | Aider |
| --- | --- | --- | --- | --- |
| 漏洞修补 | Claude 3.7 Sonnet | **33.8%** | 31.2% | 20.0% |
| 漏洞修补 | o3-mini | 31.2% | 12.5% | 17.5% |
| 漏洞修补 | GPT-4o | 26.2% | 15.0% | 11.2% |
| PoC 生成 | Claude 3.7 Sonnet | **12.5%** | 8.8% | 1.2% |
| PoC 生成 | o3-mini | 10.0% | 5.0% | 1.2% |
| PoC 生成 | GPT-4o | 3.8% | 2.5% | 0.0% |

- 全量 200 个实例上，最好成绩是修补 34.0%、PoC 生成 18.0%。**写出能触发漏洞的 PoC 远比修补难**，这与 SecVerifier 构建过程中的观察一致。
- 脚手架影响很大：同一模型 Claude 3.7 Sonnet，Aider 下 PoC 只有 1.2%。o3-mini 性价比最高（修补 31.2%，每题 0.13 美元）。
- 5 次重复实验 30.0% ± 7.9%，单次结果存在明显波动。
- 知识截止日期前后对比（Table 5）没有发现明显的数据污染迹象。

## 4. 展示建议

模型 × 脚手架的“修补 vs PoC”分组柱；数据集用崩溃类型饼图与项目分布条形图。可以作为“防守方能力”的对照组展示（这是能力测评，不是安全测评）。
