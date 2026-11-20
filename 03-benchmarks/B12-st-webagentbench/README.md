# B12　ST-WebAgentBench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　375 条任务、3,057 条策略记录、Croissant 数据卡

测试集原文件存于 `data/upstream/`，与上游目录结构一致。

**论文**　[ST-WebAgentBench - A Benchmark for Evaluating Safety and Trustworthiness in Web Agents](<paper/ST-WebAgentBench - A Benchmark for Evaluating Safety and Trustworthiness in Web Agents.pdf>) · 完整原件 42 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2410.06703) · [发布页 1](https://research.ibm.com/publications/st-webagentbench-a-benchmark-for-evaluating-safety-and-trustworthiness-in-web-agents--1)

**上游入口**　[项目或数据 1](https://github.com/segev-shlomov/ST-WebAgentBench)


## 测试集

**来源**　[GitHub segev-shlomov/ST-WebAgentBench](https://github.com/segev-shlomov/ST-WebAgentBench)

**位置**　[`data/upstream/`](data/upstream/) · 3 个文件 · 3.9 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/croissant.json`](<data/upstream/croissant.json>) | — | 1 KB |
| [`upstream/stwebagentbench/test.csv`](<data/upstream/stwebagentbench/test.csv>) | 3,057 | 668 KB |
| [`upstream/stwebagentbench/test.raw.json`](<data/upstream/stwebagentbench/test.raw.json>) | 375 | 3.2 MB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　375 任务、3,057 策略实例；3 类企业应用

**任务与判分设置**　网页任务附多条策略，以完成率、遵规完成率、策略风险指标同时观测同意、边界等维度

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
