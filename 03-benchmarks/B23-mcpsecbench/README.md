# B23　MCPSecBench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　17 类攻击的用例定义（data.json）与实验结果表

MCPSecBench 为可运行 playground，攻击服务器与客户端代码未收。

**论文**　[MCPSecBench - A Systematic Security Benchmark and Playground for Testing Model Context Protocols](<paper/MCPSecBench - A Systematic Security Benchmark and Playground for Testing Model Context Protocols.pdf>) · 完整原件 20 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2508.13220) · [发布页 1](https://arxiv.org/abs/2508.13220)

**上游入口**　[项目或数据 1](https://github.com/AIS2Lab/MCPSecBench)


## 测试集

**来源**　[GitHub AIS2Lab/MCPSecBench](https://github.com/AIS2Lab/MCPSecBench)

**位置**　[`data/upstream/`](data/upstream/) · 4 个文件 · 15 KB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/data.json`](<data/upstream/data/data.json>) | 11 | 4 KB |
| [`upstream/data/experiments.csv`](<data/upstream/data/experiments.csv>) | 45 | 2 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　17 类攻击形式，分属 4 类攻击面，测试 3 类 MCP 平台

**任务与判分设置**　同客户端、服务与工具条件对比；区分技术类别数和采用不同配置时的运行次数

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
