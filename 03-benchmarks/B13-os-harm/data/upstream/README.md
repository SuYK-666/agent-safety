---
language:
- en
pretty_name: OS-Harm
size_categories:
- n<1K
dataset_info:
  features:
  - name: osharm_category
    dtype: string
  - name: osworld_source_task
    dtype: string
  - name: software_category
    dtype: string
  - name: task_instruction
    dtype: string
  - name: explanation
    dtype: string
  - name: task_id
    dtype: string
  - name: jailbreak
    dtype: bool
  - name: injection_vector
    dtype: string
  - name: injection_goal
    dtype: string
  splits:
  - name: test
    num_bytes: 46092
    num_examples: 149
  download_size: 18328
  dataset_size: 46092
configs:
- config_name: default
  data_files:
  - split: test
    path: data/test-*
license: cc-by-sa-4.0
---

The OS-Harm benchmark of 150 safety-focused tasks for computer use agents, split across 3 categories (deliberate user misuse, prompt injection attacks, and agent misbehavior) and based on the OSWorld environment.

Some of the tasks are derived from [OSWorld](https://github.com/xlang-ai/OSWorld/): the ones named with a UUID or that have a `derived_from` field pointig to the original task in OSWorld.