# B18　PrivacyLens

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　493 条主数据，另有 ConfAIde 32 条、CultureBank 24 条扩展子集

main_data.json 在本包原有，扩展子集本次补入 data/upstream/。

**论文**　[PrivacyLens - Evaluating Privacy Norm Awareness of Language Models in Action](<paper/PrivacyLens - Evaluating Privacy Norm Awareness of Language Models in Action.pdf>) · 完整原件 35 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2409.00138) · [发布页 1](https://papers.nips.cc/paper/2024/hash/a2a7e58309d5190082390ff10ff3b2b8-Abstract-Datasets_and_Benchmarks_Track.html)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/SALT-NLP/PrivacyLens)


## 测试集

**来源**　[GitHub SALT-NLP/PrivacyLens](https://github.com/SALT-NLP/PrivacyLens)

**位置**　[`data/upstream/`](data/upstream/) · 2 个文件 · 270 KB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/data/extensibility/confide_subset.json`](<data/upstream/data/extensibility/confide_subset.json>) | 32 | 156 KB |
| [`upstream/data/extensibility/culturebank_subset.json`](<data/upstream/data/extensibility/culturebank_subset.json>) | 24 | 114 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　493 条隐私规范种子（公开数据主表 493 行）

**任务与判分设置**　按发送者、接收者、信息属性及传输条件组织，包含问答核查与行动情境；种子数不是行动轨迹数

## 本地文件

- [`DATA-LICENSE.md`](DATA-LICENSE.md) · 许可说明
- [`LICENSE.txt`](LICENSE.txt) · 许可
- [`data/main_data.json`](data/main_data.json) · 上游原文件 · 493

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
