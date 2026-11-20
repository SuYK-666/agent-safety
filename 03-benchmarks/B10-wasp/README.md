# B10　WASP

## 本包材料

**数据收录**　公开测试集完整

**实收规模**　21 条攻击任务+37 条效用任务（WebArena 格式）、实验配置、系统提示、Croissant 数据卡

运行需 WebArena GitLab/Reddit 环境，环境镜像未收。

**论文**　[WASP - Benchmarking Web Agent Security Against Prompt Injection Attacks](<paper/WASP - Benchmarking Web Agent Security Against Prompt Injection Attacks.pdf>) · 完整原件 22 页（含附录） · [上游 PDF](https://arxiv.org/pdf/2504.18575) · [发布页 1](https://proceedings.neurips.cc/paper_files/paper/2025/hash/1c9818387f5dd0a0bc151214660f059d-Abstract-Datasets_and_Benchmarks_Track.html)

**上游入口**　[项目或数据 1](https://github.com/facebookresearch/wasp)


## 测试集

**来源**　[GitHub facebookresearch/wasp](https://github.com/facebookresearch/wasp)

**位置**　[`data/upstream/`](data/upstream/) · 13 个文件 · 159 KB

| 文件 | 条数 | 大小 |
| --- | ---: | ---: |
| [`upstream/webarena_prompt_injections/configs/croissant/attacks_in_webarena_format.jsonl`](<data/upstream/webarena_prompt_injections/configs/croissant/attacks_in_webarena_format.jsonl>) | 21 | 28 KB |
| [`upstream/webarena_prompt_injections/configs/croissant/croissant_metadata.json`](<data/upstream/webarena_prompt_injections/configs/croissant/croissant_metadata.json>) | — | 5 KB |
| [`upstream/webarena_prompt_injections/configs/croissant/utility_in_webarena_format.jsonl`](<data/upstream/webarena_prompt_injections/configs/croissant/utility_in_webarena_format.jsonl>) | 37 | 43 KB |
| [`upstream/webarena_prompt_injections/configs/experiment_config.raw.json`](<data/upstream/webarena_prompt_injections/configs/experiment_config.raw.json>) | 21 | 30 KB |
| [`upstream/webarena_prompt_injections/configs/system_prompts/claude_35_agent.json`](<data/upstream/webarena_prompt_injections/configs/system_prompts/claude_35_agent.json>) | — | 1 KB |
| [`upstream/webarena_prompt_injections/configs/system_prompts/claude_35_agent_generic_defense.json`](<data/upstream/webarena_prompt_injections/configs/system_prompts/claude_35_agent_generic_defense.json>) | — | 1 KB |
| [`upstream/webarena_prompt_injections/configs/system_prompts/claude_37_agent.json`](<data/upstream/webarena_prompt_injections/configs/system_prompts/claude_37_agent.json>) | — | 1 KB |
| [`upstream/webarena_prompt_injections/configs/system_prompts/claude_37_agent_generic_defense.json`](<data/upstream/webarena_prompt_injections/configs/system_prompts/claude_37_agent_generic_defense.json>) | — | 1 KB |
| [`upstream/webarena_prompt_injections/configs/system_prompts/wa_p_cot_id_actree_3s.json`](<data/upstream/webarena_prompt_injections/configs/system_prompts/wa_p_cot_id_actree_3s.json>) | 3 | 5 KB |
| [`upstream/webarena_prompt_injections/configs/system_prompts/wa_p_cot_id_actree_3s_generic_defense.json`](<data/upstream/webarena_prompt_injections/configs/system_prompts/wa_p_cot_id_actree_3s_generic_defense.json>) | 3 | 6 KB |
| [`upstream/webarena_prompt_injections/configs/system_prompts/wa_p_som_cot_id_actree_3s.json`](<data/upstream/webarena_prompt_injections/configs/system_prompts/wa_p_som_cot_id_actree_3s.json>) | 3 | 6 KB |
| [`upstream/webarena_prompt_injections/configs/system_prompts/wa_p_som_cot_id_actree_3s_generic_defense.json`](<data/upstream/webarena_prompt_injections/configs/system_prompts/wa_p_som_cot_id_actree_3s_generic_defense.json>) | 3 | 7 KB |

文件保持上游原始字节与相对路径，任务目录、图片等成组文件未逐一列出；逐文件来源与 SHA-256 见[文件清单](../file-manifest.csv)。

## 基准口径

**公开资料规模**　42 测试场景 × 2 工具能力配置＝84 项（论文计分分母）

**任务与判分设置**　浏览器环境中分别观测中途偏移、端到端达成；记录是否有完成合法任务及访问相关页面的能力

版本与哈希请查阅 [Benchmark 总目录](../README.md)。
