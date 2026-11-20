# B34　CyberSOCEval

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　PurpleLlama 官方题目 609+588 条、CrowdStrike 报告 PDF 21 份、Hybrid Analysis 沙箱报告 178 份

原两个 Parquet 为 HF 镜像，保留。沙箱报告是 JSON 文本，不含可执行样本。

**论文**　[CyberSOCEval - Benchmarking LLMs Capabilities for Malware Analysis and Threat Intelligence Reasoning](<paper/CyberSOCEval - Benchmarking LLMs Capabilities for Malware Analysis and Threat Intelligence Reasoning.pdf>) · 完整原件 26 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2509.20166) · [发布页 1](https://ai.meta.com/research/publications/cybersoceval-benchmarking-llms-capabilities-for-malware-analysis-and-threat-intelligence-reasoning/) · [发布页 2](https://arxiv.org/abs/2509.20166) · [发布页 3](https://huggingface.co/datasets/kyleavery/cybersoceval-questions/blame/main/README.md)

**上游入口**　[项目或数据 1](https://github.com/CrowdStrike/CyberSOCEval_data)


## 测试集

**来源**　[GitHub meta-llama/PurpleLlama](https://github.com/meta-llama/PurpleLlama) · [GitHub CrowdStrike/CyberSOCEval_data](https://github.com/CrowdStrike/CyberSOCEval_data)

**位置**　[`data/upstream/`](data/upstream/)、[`data/upstream-purplellama/`](data/upstream-purplellama/) · 206 个文件 · 93.1 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream-purplellama/malware_analysis/questions.json`](<data/upstream-purplellama/malware_analysis/questions.json>) | 609 | 360 KB |
| [`upstream-purplellama/threat_intel_reasoning/report_questions.json`](<data/upstream-purplellama/threat_intel_reasoning/report_questions.json>) | 588 | 548 KB |

成组目录：

- [`upstream/data/hybrid-analysis/`](<data/upstream/data/hybrid-analysis/>) · 178 份 Hybrid Analysis 沙箱报告 · 178 个文件
- [`upstream/data/crowdstrike-reports/`](<data/upstream/data/crowdstrike-reports/>) · 21 份 CrowdStrike 威胁情报报告 PDF · 21 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　两选择题子集，问题公开副本报告 609 恶意软件分析、588 威胁情报题

**任务与判分设置**　基于沙箱分析报告或威胁情报报告进行推理；测阅读研判，生产 SOC 处置需另测

## 本地文件

- [`data/malware-analysis-questions.parquet`](data/malware-analysis-questions.parquet) · 上游题目镜像，Parquet · 609
- [`data/threat-intelligence-questions.parquet`](data/threat-intelligence-questions.parquet) · 上游题目镜像，Parquet · 588

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
