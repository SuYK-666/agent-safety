# B09　ToolEmu

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　144 条测试案例、38 个工具包规格

测试集原文件存于 `data/upstream/`，与上游目录结构一致。

**论文**　[Identifying the Risks of LM Agents with an LM-Emulated Sandbox](<paper/Identifying the Risks of LM Agents with an LM-Emulated Sandbox.pdf>) · 完整原件 68 页（含附录） · [上游 PDF](https://proceedings.iclr.cc/paper_files/paper/2024/file/7274ed909a312d4d869cc328ad1c5f04-Paper-Conference.pdf) · [发布页 1](https://proceedings.iclr.cc/paper_files/paper/2024/hash/7274ed909a312d4d869cc328ad1c5f04-Abstract-Conference.html)

**上游入口**　[项目或数据 1](https://github.com/ryoungj/ToolEmu)


## 测试集

**来源**　[GitHub ryoungj/ToolEmu](https://github.com/ryoungj/ToolEmu)

**位置**　[`data/upstream/`](data/upstream/) · 3 个文件 · 784 KB

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　144 案例、36 工具包、311 工具

**任务与判分设置**　按工具规格由语言模型模拟状态与响应，用裁判识别风险和任务质量；仿真结果取决于模拟器的忠实度

## 本地文件

- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/cases-benign-input-view.json`](data/cases-benign-input-view.json) · 从上游原始案例投影字段 · 144
- [`metadata/toolkit-inventory.json`](metadata/toolkit-inventory.json) · 工具数据字典 · 38

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
