# B11　SafeArena

## 本包材料

**数据收录**　上游访问受限

**实收规模**　论文全文

harm.json/safe.json 在 HF 设为需登录同意的 gated 数据集，匿名下载返回 401；网站环境镜像约 100 GB 亦未收。需作者许可后下载。

**论文**　[SafeArena - Evaluating the Safety of Autonomous Web Agents](<paper/SafeArena - Evaluating the Safety of Autonomous Web Agents.pdf>) · 完整原件 38 页（含附录） · [上游 PDF](https://github.com/mlresearch/v267/blob/main/assets/tur25a/tur25a.pdf) · [发布页 1](https://proceedings.mlr.press/v267/tur25a.html)

**上游入口**　[项目或数据 1](https://huggingface.co/datasets/McGill-NLP/safearena)


## 测试集

**状态**　上游访问受限。harm.json/safe.json 在 HF 设为需登录同意的 gated 数据集，匿名下载返回 401；网站环境镜像约 100 GB 亦未收。需作者许可后下载。

**已核查入口**　[HF McGill-NLP/safearena](https://huggingface.co/datasets/McGill-NLP/safearena)

## 基准口径

**公开资料规模**　250 安全任务＋250 有害任务；4 类网站环境

**任务与判分设置**　按网站和伤害类型评分，跟踪有害任务响应与正常任务过度拒绝

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
