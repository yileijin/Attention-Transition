# Attention Transition

Official implementation of [DiffusionBERT: Improving Generative Masked Language Models with Diffusion Models](https://arxiv.org/abs/2211.15029).

### Abstract
Recently, with the emergence of numerous Large Language Models (LLMs), the implementation of AI has entered a new era. Irrespective of these models' own capacity and structure, there is a growing demand for LLMs to possess enhanced comprehension of longer and more complex contexts with relatively smaller sizes. Models often encounter an upper limit when processing sequences of sentences that extend beyond their comprehension capacity and result in off-topic or even chaotic responses. While several recent works attempt to address this issue in various ways, they rarely focus on "why models are unable to compensate or strengthen their capabilities on their own". In this paper, we thoroughly investigate the nature of information transfer within LLMs and propose a novel technique called Attention Transition. This technique empowers models to achieve longer and better context comprehension with minimal additional training or impact on generation fluency. Our experiments are conducted in XSum and achieve substantial improvement compared with the original generation results.

### Preparing the technique

We have provided the modified llama that satisfies our technique, just load the llama-7b model from 🤗 hugging face and replace
the modeling_llama.py in your environment with ours. Path of modeling_llama: $your_env$/lib/python3.11/site-packages/transformers/models/llama/modeling_llama.py

```bash
from transformers import AutoTokenizer, AutoModelForCausalLM
tokenizer = AutoTokenizer.from_pretrained("huggyllama/llama-7b")
model = AutoModelForCausalLM.from_pretrained("huggyllama/llama-7b").cuda().eval().half()
```

The xsum dataset is also available at 🤗 Datasets. The data we used to generate has released in file: /generation_results/, as well as 
all generation results together with the gpt4 evaluations

### Generation

The /model_generation.ipynb is for model generation.
Things to remember: set the parameter with True to implement our technique in the line 820 in our modeling_llama.py
```bash
attn_transition: Optional[bool] = True
```
### Evaluation

The evaluation is all conducted on GPT4, with a fixed prompt that defined in our /evaluation/evaluation.ipynb, you can check for detail.

Welcome to post an issue or send me an email if there are any questions
email: yilei.jin123@gmail.com

### Citation

```
@article{he2022diffusionbert,
  title={DiffusionBERT: Improving Generative Masked Language Models with Diffusion Models},
  author={He, Zhengfu and Sun, Tianxiang and Wang, Kuanning and Huang, Xuanjing and Qiu, Xipeng},
  journal={arXiv preprint arXiv:2211.15029},
  year={2022}
}
