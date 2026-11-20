# B14　MMA-SafetyBench

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　Web GUI 42 张原始截图、209 条投毒前端及攻击 JSON；文档分析 2×100 条攻击与 11 张底图

上游仓库中的攻击生成脚本（scripts/）未收。

**论文**　[MMA-SafetyBench - A Benchmark for Multimodal Agent Safety Evaluation](<paper/MMA-SafetyBench - A Benchmark for Multimodal Agent Safety Evaluation.pdf>) · 完整原件 19 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2610.19384) · [发布页 1](https://arxiv.org/abs/2610.19384)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/Alibaba-YuFeng/MMA-SafetyBench)


## 测试集

**来源**　[HF Alibaba-YuFeng/MMA-SafetyBench](https://huggingface.co/datasets/Alibaba-YuFeng/MMA-SafetyBench)

**位置**　[`data/upstream/`](data/upstream/) · 515 个文件 · 149.3 MB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/02_Document_Analysis/GEPA_FULL_DIMENSION_ATTACK_V3.json`](<data/upstream/02_Document_Analysis/GEPA_FULL_DIMENSION_ATTACK_V3.json>) | 100 | 118 KB |
| [`upstream/02_Document_Analysis/GEPA_WEB_STYLE_DIVERSE.json`](<data/upstream/02_Document_Analysis/GEPA_WEB_STYLE_DIVERSE.json>) | 100 | 150 KB |

成组目录：

- [`upstream/01_Web_GUI_Testing/`](<data/upstream/01_Web_GUI_Testing/>) · Web GUI：原始截图 42、GUI 元数据 42、投毒前端截图 209、攻击 JSON 209 · 502 个文件
- [`upstream/02_Document_Analysis/base_receipts/`](<data/upstream/02_Document_Analysis/base_receipts/>) · 文档分析底图 11 张 · 11 个文件

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　1,083 多模态对抗轨迹

**任务与判分设置**　网页、桌面、移动端、文档、视频；以可见视觉语义、输出与行为意图判断，预测动作与执行效果分开

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
