# Grading Models for GradeMate

## Project Overview

The purpose of this project is to expand on the [GradeMate app](https://www.grade-mate.app/) by replacing proprietary models with open-source models. This involves prompting, fine-tuning, evaluating, and orchestrating open-source Large Language Models (LLMs). The project is conducted in collaboration with the [Columbia University QMSS Innovation Lab](https://qmss.columbia.edu/content/how-does-qmss-innovation-lab-work).

## Requirements

Python version: 3.10.12
PyTorch version: 2.5.0+cu121
CUDA version: 12.1

For the first stage of this project, access to a GPU with 15 GB VRAM is needed (for models based on Llama-3.2-1B-Instruct and Llama-3.2-3B-Instruct). Google Colab meets in this requirement. For a later stage, where we will be fine-tuning a larger models, more than 35 GB RAM will be needed.

## Models Info

- **Model Used**: Llama-3.1-8B-Instruct
- **Model Card**: [Llama-3.1-8B-Instruct](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct)
- **Llama Models GitHub**: [meta-llama/llama-models](https://github.com/meta-llama/llama-models)
- **Meta Release**: [Meta LLaMA 3.1 Performance](https://ai.meta.com/blog/meta-llama-3-1/)

### Key Features

- **Multi-lingual Support**: Supports English, German, French, Italian, Portuguese, Hindi, Spanish, and Thai.
- **Model Selection**: Selected for its multi-lingual capabilities and suitability for fine-tuning within the resource limits of Colab Pro's GPUs.

## Modeling Strategy: Use Criterion-Specific LLMs

To streamline fine-tuning, we are building a separate LLM for each individual grading criterion. This allows for targeted fine-tuning based on the complexity of the writing criterion. Also, since each criterion may appear across multiple rubrics, organizing fine-tuning by criterion rather than by rubric simplifies the process, addressing each assessment dimension independently.

### Writing Assessment Criteria

| Writing Criteria Type          | Model Complexity (Parameters) | Fine-Tuning Required? |
|----------------------------|-------------------------------|------------------------|
| Grammar                    | Low (100M - 500M)            | No                     |
| Language Appropriateness    | Medium (500M - 1B)           | Yes                    |
| Writing Cohesiveness and Context-Sensitive Tasks       | High (1B - 6B)               | Yes                    |
| Content        | Very High (6B +)               | Yes                    |

Note: Justifying assessments can be more complex than generating a score alone. Decide whether to handle justification independently.

## Steps

1. **Set-Up**
2. **Prompting**
3. **Fine-tuning**: Refer to [Fine-Tuning Guide](https://www.llama.com/docs/how-to-guides/fine-tuning/)
4. **Orchestration**: Use LangChain to orchestrate LLM calls.
5. **Deploy**: Follow deployment guidelines from [NLP Cloud](https://nlpcloud.com/how-to-install-and-deploy-llama-3-into-production.html)
