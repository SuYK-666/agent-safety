# B36　SOCBench（Detection）

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　检测 v0 757,641 条、CIC2018 示例 72 条

本包原有，无需补充。

**论文**　经核查无对应论文，仅有项目网页与仓库文档。 · [发布页 1](https://socbench.org/) · [发布页 2](https://socbench.org/detection/)

**上游入口**　[项目或数据 1](https://socbench.org/detection/) · [项目或数据 2](https://github.com/DeepTempo/socbench)


## 测试集

**状态**　公开测试集完整。本包原有，无需补充。

**已核查入口**　[GitHub DeepTempo/socbench](https://github.com/DeepTempo/socbench)

## 基准口径

**公开资料规模**　约 75.7 万流记录、8 个来源（检测模块）

**任务与判分设置**　归并带标签的网络流量，按告警跟踪检测质量，关注成本和误报

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 仓库许可
- [`data/benchmark-v0.parquet`](data/benchmark-v0.parquet) · 上游原始数据文件 · 757641
- [`data/sample/cic2018-mini.parquet`](data/sample/cic2018-mini.parquet) · 上游原始数据文件 · 72
- [`materials/schema.json`](materials/schema.json) · 上游数据字典

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
