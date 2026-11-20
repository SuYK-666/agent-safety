---
license: mit
language:
- en
---

Agent-SafetyBench is a comprehensive agent safety evaluation benchmark that introduces a diverse array of novel environments that are previously unexplored, and offers broader and more systematic coverage of various risk categories and failure modes.

Please visit our [Github](https://github.com/thu-coai/Agent-SafetyBench) or check our [paper](https://arxiv.org/abs/2412.14470) for more details.

## Load the Data

```python
from datasets import load_dataset

dataset = load_dataset("thu-coai/Agent-SafetyBench")
```

More details about loading the data and evaluating LLMs could be found at our [Github Repository](https://github.com/thu-coai/Agent-SafetyBench).

Please kindly cite our paper if you use our dataset.

## Citation
If you find our work helpful, please kindly cite our paper.
```
@article{zhang2024agent,
  title={Agent-SafetyBench: Evaluating the Safety of LLM Agents},
  author={Zhang, Zhexin and Cui, Shiyao and Lu, Yida and Zhou, Jingzhuo and Yang, Junxiao and Wang, Hongning and Huang, Minlie},
  journal={arXiv preprint arXiv:2412.14470},
  year={2024}
}
```