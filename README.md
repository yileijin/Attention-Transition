# Attention Transition
Official implementation of paper:[Empower Your Model with Longer and Better Context Comprehension](https://arxiv.org/abs/2307.13365)

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

The xsum dataset is also available at 🤗 Datasets. The data we used to generate has released in file: /evaluation/, as well as 
all generation results together with the gpt4 evaluations

### Generation

The /model_generation.ipynb is for model generation.
Things to remember: set the parameter with True to implement our technique in the line 820 in our modeling_llama.py
```bash
attn_transition: Optional[bool] = True
```
### Evaluation

The evaluation is all conducted on GPT4, with a fixed prompt that defined in our /evaluation/evaluation.ipynb, you can check for detail.
The scores present in paper are all generated from /evaluation/get_scores.ipynb
\Files end with .json are our results

Welcome to post an issue or send me an email if there are any questions.
email: yilei.jin123@gmail.com

### Citation 
```bash
@misc{gao2023empower,
      title={Empower Your Model with Longer and Better Context Comprehension}, 
      author={Yifei Gao and Lei Wang and Jun Fang and Longhua Hu and Jun Cheng},
      year={2023},
      eprint={2307.13365},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```

