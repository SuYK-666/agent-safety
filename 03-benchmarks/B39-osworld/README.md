# B39　OSWorld

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　368 个 Ubuntu 任务配置、49 个 Windows 任务、全部索引与 HF 补丁

固定提交 5123bfdb。VM 镜像与外置文件未收。

**论文**　[OSWorld - Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments](<paper/OSWorld - Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments.pdf>) · 完整原件 51 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2404.07972) · [发布页 1](https://arxiv.org/abs/2404.07972) · [发布页 2](https://github.com/xlang-ai/OSWorld/blob/main/evaluation_examples/test_all.json) · [发布页 3](https://github.com/xlang-ai/OSWorld/blob/main/evaluation_examples/README.md)

**上游入口**　[项目或数据 1](https://github.com/xlang-ai/OSWorld)


## 测试集

**来源**　[GitHub xlang-ai/OSWorld](https://github.com/xlang-ai/OSWorld)

**位置**　[`data/upstream/`](data/upstream/) · 444 个文件 · 1.0 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/evaluation_examples/test_all.json`](<data/upstream/evaluation_examples/test_all.json>) | 368 | 16 KB |
| [`upstream/evaluation_examples/test_infeasible.json`](<data/upstream/evaluation_examples/test_infeasible.json>) | 25 | 1 KB |
| [`upstream/evaluation_examples/test_nogdrive.json`](<data/upstream/evaluation_examples/test_nogdrive.json>) | 360 | 16 KB |
| [`upstream/evaluation_examples/test_small.json`](<data/upstream/evaluation_examples/test_small.json>) | 39 | 1 KB |

成组目录：

- [`upstream/evaluation_examples/examples/`](<data/upstream/evaluation_examples/examples/>) · 368 个 Ubuntu 任务配置 JSON（按应用分目录） · 369 个文件
- [`upstream/evaluation_examples/examples_windows/`](<data/upstream/evaluation_examples/examples_windows/>) · 49 个 Windows 任务配置 JSON · 49 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　原论文 369；所核对上游现行任务索引 368

**任务与判分设置**　真实桌面与多应用任务，按虚拟机环境、动作观测与终态判定；索引可用于抽样

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/`](data/) · 444 个文件（含 `data/upstream*/` 测试集），逐文件地址、计数与校验值见[文件清单](../file-manifest.csv)。

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
