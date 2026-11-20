# B35　Cyber Defense Benchmark

## 本包材料

**数据收录**　公开样例集

**实收规模**　作者仓库唯一公开数据 sample.zip（1 套日志+标签）与参考表

完整 106 套基准需邮件向作者申请，未公开。

**论文**　[Cyber Defense Benchmark - Agentic Threat Hunting Evaluation for LLMs in SecOps](<paper/Cyber Defense Benchmark - Agentic Threat Hunting Evaluation for LLMs in SecOps.pdf>) · 完整原件 16 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2604.19533) · [发布页 1](https://arxiv.org/abs/2604.19533) · [发布页 2](https://simbian.ai/research/cyber-defense-benchmark)

**上游入口**　[项目或数据 1](https://simbian.ai/research/cyber-defense-benchmark) · [项目或数据 2](https://github.com/simbianai/cyber_defense_benchmark)


## 测试集

**来源**　[GitHub simbianai/cyber_defense_benchmark](https://github.com/simbianai/cyber_defense_benchmark)

**位置**　[`data/upstream/`](data/upstream/) · 7 个文件 · 10.9 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/datasets/sample.zip`](<data/upstream/datasets/sample.zip>) | — | 10.9 MB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　106 套已记录过程；86 个子技术、12 战术

**任务与判分设置**　从 Windows 事件日志定位事件时间，依据检测规则形成参考标签，首要观察召回和误报

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
