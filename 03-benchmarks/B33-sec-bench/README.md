# B33　SEC-bench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　eval-cve 200 条、eval-oss 100 条

复现所需 Docker 镜像未收。

**论文**　[SEC-bench - Automated Benchmarking of LLM Agents on Real-World Software Security Tasks](<paper/SEC-bench - Automated Benchmarking of LLM Agents on Real-World Software Security Tasks.pdf>) · 完整原件 30 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2506.11791) · [发布页 1](https://arxiv.org/abs/2506.11791) · [发布页 2](https://huggingface.co/datasets/SEC-bench/SEC-bench)


## 测试集

**来源**　[HF SEC-bench/SEC-bench](https://huggingface.co/datasets/SEC-bench/SEC-bench)

**位置**　[`data/upstream/`](data/upstream/) · 4 个文件 · 3.7 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/eval-cve.jsonl`](<data/upstream/data/eval-cve.jsonl>) | 200 | 2.5 MB |
| [`upstream/data/eval-oss.jsonl`](<data/upstream/data/eval-oss.jsonl>) | 100 | 1.2 MB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　公开数据卡 600 行；按漏洞实例及 PoC／修补任务分别计

**任务与判分设置**　真实风格安全工程任务，补丁侧核对修复及正常行为保持，勿把补丁成绩视为部署防护成绩

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
