---
task_categories:
- text-generation
language:
- en

extra_gated_prompt: "You must agree to the terms of use described in the dataset card and complete relevant fields"
extra_gated_fields:
 Full Name: text
 Affiliation: text
 Country: text
 Academic or Work Email Address: text
 I agree to follow the terms of use: checkbox

size_categories:
- n<1K
---

<div align="center">
  
<h1>SafeArena</h1>

| [**💾Code**](https://github.com/McGill-NLP/safearena) | [**📄Paper**](https://arxiv.org/abs/2503.04957) | [**🌐Website**](https://safearena.github.io) | [**🏆Leaderboard**](https://huggingface.co/spaces/McGill-NLP/safearena-leaderboard)
| :--: | :--: | :--: | :--: |

</div>

## Instructions

First, request access to the SafeArena dataset on the Hugging Face Hub. Once you have access, you can log in using the huggingface_hub CLI:

```bash
pip install huggingface-hub
huggingface-cli login
```

Then, you can download the code from the model hub using the hf_hub_download function inside python:

```python
from huggingface_hub import hf_hub_download

# Download the safe.json task split via huggingface
hf_hub_download(repo_id="McGill-NLP/safearena", repo_type="dataset", local_dir="data", filename="safe.json")
# Download the harm.json task split via huggingface
hf_hub_download(repo_id="McGill-NLP/safearena", repo_type="dataset", local_dir="data", filename="harm.json")
```

You now have the required task splits in the relative data/ directory. 

### Versions

If you want to access a specific version, e.g. [an older version of the dataset](https://huggingface.co/datasets/McGill-NLP/safearena/tree/0.1), you can run:

```python
# specify your revision:
hf_hub_download(repo_id="McGill-NLP/safearena", repo_type="dataset", revision="0.1")
```



## Terms of Use

By downloading this Dataset, you agree to comply with the following terms of use:
- Restrictions: You agree not to use the Dataset in any way that is unlawful or would infringe upon the rights of others.
- Acknowledgment: By using the Dataset, you acknowledge that the Dataset may contain data derived from third-party sources, and you agree to abide by any additional terms and conditions that may apply to such third-party data.
- Fair Use Declaration: The Dataset may be used for research if it constitutes "fair use" under copyright laws within your jurisdiction. You are responsible for ensuring your use complies with applicable laws.

Derivatives must also include the terms of use above.