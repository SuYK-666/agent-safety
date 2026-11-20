# B32　CyberSecEval 3

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　视觉提示注入 1,000 条（含图片）、鱼叉钓鱼 856 条、AutoPatch 148 例、自主提升样例

CSE3 文本提示注入与 MITRE 等沿用 CSE2 题集，见 B31。

**论文**　[CyberSecEval 3 - Advancing the Evaluation of Cybersecurity Risks and Capabilities in Large Language Models](<paper/CyberSecEval 3 - Advancing the Evaluation of Cybersecurity Risks and Capabilities in Large Language Models.pdf>) · 完整原件 36 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2408.01605) · [发布页 1](https://ai.meta.com/research/publications/cyberseceval-3-advancing-the-evaluation-of-cybersecurity-risks-and-capabilities-in-large-language-models/)


## 测试集

**来源**　[HF facebook/cyberseceval3-visual-prompt-injection](https://huggingface.co/datasets/facebook/cyberseceval3-visual-prompt-injection) · [GitHub meta-llama/PurpleLlama](https://github.com/meta-llama/PurpleLlama)

**位置**　[`data/upstream-purplellama/`](data/upstream-purplellama/)、[`data/upstream-visual-prompt-injection/`](data/upstream-visual-prompt-injection/) · 1302 个文件 · 1209.1 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream-purplellama/autonomous_uplift/in/cyber_range_pairs_sample.json`](<data/upstream-purplellama/autonomous_uplift/in/cyber_range_pairs_sample.json>) | 3 | 1 KB |
| [`upstream-purplellama/autonomous_uplift/out/autonomous_prompts_sample.json`](<data/upstream-purplellama/autonomous_uplift/out/autonomous_prompts_sample.json>) | 3 | 9 KB |
| [`upstream-purplellama/autopatch/autopatch_arvo_examples.json`](<data/upstream-purplellama/autopatch/autopatch_arvo_examples.json>) | 1 | 1 KB |
| [`upstream-purplellama/autopatch/autopatch_bench.json`](<data/upstream-purplellama/autopatch/autopatch_bench.json>) | 136 | 1 KB |
| [`upstream-purplellama/autopatch/autopatch_lite.json`](<data/upstream-purplellama/autopatch/autopatch_lite.json>) | 113 | 1 KB |
| [`upstream-purplellama/autopatch/autopatch_samples.json`](<data/upstream-purplellama/autopatch/autopatch_samples.json>) | 20 | 1 KB |
| [`upstream-purplellama/spear_phishing/multiturn_phishing_challenges.json`](<data/upstream-purplellama/spear_phishing/multiturn_phishing_challenges.json>) | 856 | 1.9 MB |
| [`upstream-visual-prompt-injection/test_cases.json`](<data/upstream-visual-prompt-injection/test_cases.json>) | 1,000 | 574 KB |

成组目录：

- [`upstream-visual-prompt-injection/images/`](<data/upstream-visual-prompt-injection/images/>) · 1,000 张视觉提示注入图片 · 1000 个文件
- [`upstream-purplellama/autopatch/arvo_meta/`](<data/upstream-purplellama/autopatch/arvo_meta/>) · AutoPatch 148 例元数据与补丁 · 293 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　8 个风险领域，各自按子项计数

**任务与判分设置**　扩展企业与终端风险，涵盖代码助手、终端和自主能力评测等

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
