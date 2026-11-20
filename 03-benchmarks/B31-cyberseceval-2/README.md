# B31　CyberSecEval 2

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　PurpleLlama 官方：自动补全 1,916、指令 1,916/1,681、解释器滥用 500、MITRE 1,000、误拒绝 750、提示注入 251，含多语种版；另附 walledai HF 镜像

CSE2 漏洞利用（canary_exploit）由脚本动态生成，上游无静态题库。

**论文**　[CyberSecEval 2 - A Wide-Ranging Cybersecurity Evaluation Suite for Large Language Models](<paper/CyberSecEval 2 - A Wide-Ranging Cybersecurity Evaluation Suite for Large Language Models.pdf>) · 完整原件 21 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2404.13161) · [发布页 1](https://arxiv.org/abs/2404.13161) · [发布页 2](https://github.com/turbobeest/modelspec/blob/main/benchmarks/cyberseceval_2.md)


## 测试集

**来源**　[GitHub meta-llama/PurpleLlama](https://github.com/meta-llama/PurpleLlama) · [HF walledai/CyberSecEval](https://huggingface.co/datasets/walledai/CyberSecEval)

**位置**　[`data/upstream-purplellama/`](data/upstream-purplellama/)、[`data/upstream-walledai/`](data/upstream-walledai/) · 27 个文件 · 24.5 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream-purplellama/autocomplete/autocomplete.json`](<data/upstream-purplellama/autocomplete/autocomplete.json>) | 1,916 | 3.3 MB |
| [`upstream-purplellama/instruct/instruct-v2.json`](<data/upstream-purplellama/instruct/instruct-v2.json>) | 1,681 | 2.9 MB |
| [`upstream-purplellama/instruct/instruct.json`](<data/upstream-purplellama/instruct/instruct.json>) | 1,916 | 3.2 MB |
| [`upstream-purplellama/interpreter/interpreter.json`](<data/upstream-purplellama/interpreter/interpreter.json>) | 500 | 379 KB |
| [`upstream-purplellama/mitre/mitre_benchmark_100_per_category_with_augmentation.json`](<data/upstream-purplellama/mitre/mitre_benchmark_100_per_category_with_augmentation.json>) | 1,000 | 4.3 MB |
| [`upstream-purplellama/mitre/mitre_prompts_multilingual_machine_translated.json`](<data/upstream-purplellama/mitre/mitre_prompts_multilingual_machine_translated.json>) | 700 | 5.5 MB |
| [`upstream-purplellama/mitre_frr/frr_multilingual_machine_translated.json`](<data/upstream-purplellama/mitre_frr/frr_multilingual_machine_translated.json>) | 700 | 1.1 MB |
| [`upstream-purplellama/mitre_frr/mitre_frr.json`](<data/upstream-purplellama/mitre_frr/mitre_frr.json>) | 750 | 410 KB |
| [`upstream-purplellama/prompt_injection/prompt_injection.json`](<data/upstream-purplellama/prompt_injection/prompt_injection.json>) | 251 | 194 KB |
| [`upstream-purplellama/prompt_injection/prompt_injection_multilingual_machine_translated.json`](<data/upstream-purplellama/prompt_injection/prompt_injection_multilingual_machine_translated.json>) | 1,004 | 1.0 MB |
| [`upstream-walledai/autocomplete/c-00000-of-00001.parquet`](<data/upstream-walledai/autocomplete/c-00000-of-00001.parquet>) | 227 | 138 KB |
| [`upstream-walledai/autocomplete/cpp-00000-of-00001.parquet`](<data/upstream-walledai/autocomplete/cpp-00000-of-00001.parquet>) | 259 | 164 KB |
| [`upstream-walledai/autocomplete/csharp-00000-of-00001.parquet`](<data/upstream-walledai/autocomplete/csharp-00000-of-00001.parquet>) | 235 | 131 KB |
| [`upstream-walledai/autocomplete/java-00000-of-00001.parquet`](<data/upstream-walledai/autocomplete/java-00000-of-00001.parquet>) | 229 | 154 KB |

另有 12 个数据文件未逐一列出。

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　常见公开子集：代码解释器滥用 500、提示注入 251、误拒绝 750；随版本变化

**任务与判分设置**　网络安全能力与风险，包括工具化能力、提示注入和代码相关任务，须逐子项比

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
