# B07　AgentHarm

## 本包材料

**数据收录**　公开测试集（作者部分发布）

**实收规模**　有害 176+良性 176+对话 44 条公开测试，另有验证集 32/32/8

作者目前只公开 66 个基础行为中的 44 个（扩增后 176）；其余为私有保留集。许可为 MIT 附加条款：仅限用于提升 AI 安全。

**论文**　[AgentHarm - A Benchmark for Measuring Harmfulness of LLM Agents](<paper/AgentHarm - A Benchmark for Measuring Harmfulness of LLM Agents.pdf>) · 完整原件 36 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2410.09024) · [发布页 1](https://proceedings.iclr.cc/paper_files/paper/2025/hash/c493d23af93118975cdbc32cbe7323f5-Abstract-Conference.html) · [发布页 2](https://www.aisi.gov.uk/research/agentharm-a-benchmark-for-measuring-harmfulness-of-llm-agents)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/ai-safety-institute/AgentHarm/tree/main/benchmark)


## 测试集

**来源**　[HF ai-safety-institute/AgentHarm](https://huggingface.co/datasets/ai-safety-institute/AgentHarm)

**位置**　[`data/upstream/`](data/upstream/) · 8 个文件 · 339 KB

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　110 原始任务；扩增后 440；11 类伤害

**任务与判分设置**　用户直接发起有害请求，模拟多工具任务；评分区分拒绝、部分完成与完成，公开划分及良性对照见项目

## 本地文件

- [`LICENSE-UPSTREAM.txt`](LICENSE-UPSTREAM.txt) · 许可

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
