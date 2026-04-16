# MixEval — Dynamic Mixed Evaluation Benchmark

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | MixEval: Deriving Wisdom of the Crowd from LLM Benchmark Mixtures |
| Creator | Jinjie Ni, Fuzhao Xue, Xiang Yue et al. (NUS, CMU, AI2) |
| Release Year | 2024 |
| Number of Questions | MixEval: 4,000 / MixEval-Hard: 1,000 |
| Question Type | Multiple choice + open-ended QA (mixed sources) |
| Dataset Link | https://huggingface.co/datasets/MixEval/MixEval |
| Paper Link | https://arxiv.org/abs/2406.06530 |
| GitHub | https://github.com/Psycoy/MixEval |
| Project Page | https://mixeval.github.io/ |
| Status | ✅ Actively maintained, accepted at NeurIPS 2024 |

## Overview

MixEval proposes a completely new evaluation paradigm: instead of designing questions from scratch, it mines real needs from massive internet user queries and then semantically matches them with existing benchmark question banks to automatically generate evaluation sets. The core idea is "wisdom of the crowd" — by mixing the strengths of multiple existing benchmarks, it approaches the evaluation effect of real human preferences.

MixEval-Hard is its difficult version, using difficulty-weighted sampling and rejection sampling to preserve distribution, achieving a Spearman correlation coefficient of **0.96** with Chatbot Arena Elo, the highest among all automated benchmarks. Meanwhile, single-model evaluation costs only about **$0.60**, far lower than Chatbot Arena (approximately $2,936) and WildBench (approximately $88.90).

## Dataset Composition

### Data Mining Pipeline

1. **Internet query detection**: Training Vicuna-33B to detect user queries in Common Crawl (recall >99%, precision >98%), mining approximately 2 million queries
2. **GPT-4 Turbo classification**: Classifying queries into different task types
3. **Semantic matching**: Using all-mpnet-base-v2 sentence embeddings to match each internet query with the most similar question in the benchmark question bank
4. **Composing evaluation set**: MixEval (4,000 questions) and MixEval-Hard (1,000 questions, difficulty-weighted sampling)

### MixEval vs MixEval-Hard

| Feature | MixEval | MixEval-Hard |
|------|---------|--------------|
| Number of questions | 4,000 | 1,000 |
| Difficulty distribution | Natural distribution | Difficulty-weighted sampling |
| Correlation with Arena (Spearman) | 0.93 | 0.96 |
| Single model evaluation cost | ~$2.30 | ~$0.60 |
| Update time | ~1 minute | ~2 minutes |

### Question Sources (Benchmark Pool)

MixEval matches and mixes questions from the following existing benchmarks:
- MMLU / MMLU-Pro
- GSM8K / MATH
- HumanEval / MBPP
- ARC-Challenge
- TruthfulQA
- HellaSwag
- And several other mainstream benchmarks

### Dynamic Update Mechanism

One of MixEval's core advantages is dynamic evaluation, preventing data contamination:

| Update Method | Description |
|----------|------|
| Batch web query update | Re-mine queries from the latest Common Crawl |
| Source web query update | Update matching sources and question pools |
| Benchmark pool expansion | Add newly released benchmarks |

- Fast update speed: MixEval ~1 minute, MixEval-Hard ~2 minutes
- Version stability: Average standard deviation across 5 versions on 5 models is only **0.36** (on a percentage scale)
- Unique question ratio across versions: 85% (benchmark queries), 99.71% (web queries)

## Evaluation Method

### Scoring Method

MixEval uses **ground-truth-based grading** rather than LLM-as-Judge:

| Step | Description |
|------|------|
| 1. Query matching | Match internet queries with benchmark questions |
| 2. Model inference | The model being evaluated answers all questions |
| 3. Answer parsing | Use GPT-3.5 as a parser to extract answers from model output |
| 4. Ground-truth comparison | Compare parsed answers with ground-truth answers |
| 5. Scoring | Calculate overall accuracy |

### Comparison with Other Evaluation Methods

| Feature | MixEval | LLM-as-Judge | Chatbot Arena |
|------|---------|---------------|---------------|
| Scoring method | Ground-truth comparison | LLM judge model | Human voting |
| Preference bias | Low | Medium (length/position bias) | Low |
| Cost | ~$0.60 | ~$25-90 | ~$2,936 |
| Reproducibility | High | Medium | Low |
| Correlation with Arena | 0.96 | 0.89-0.95 | 1.00 |

### Cost Efficiency

| Benchmark | Correlation with Arena | Single Model Cost |
|-----------|----------------|------------|
| Chatbot Arena | 1.00 | ~$2,936 |
| **MixEval-Hard** | **0.96** | **$0.60** |
| MixEval | 0.93 | $2.30 |
| AlpacaEval 2.0 | 0.95 | $24.40 |
| WildBench | 0.95 | $88.90 |
| Arena-Hard | 0.86 | $25.30 |
| MMLU | 0.83 | $9.40 |
| MT-Bench | 0.80 | $10.10 |

> Data source: MixEval paper Table 1 (NeurIPS 2024)

## Model Performance (April 2026)

Below are representative model scores on MixEval-Hard:

| Model | MixEval-Hard Score | Consistency with Arena Elo Ranking |
|------|-------------------|------------------------|
| Claude Opus 4.6 | ~92% | High |
| GPT-5 | ~91% | High |
| Gemini 3 Pro | ~89% | High |
| DeepSeek V3 | ~82% | Medium |
| Llama 4 Maverick | ~78% | Medium |

> Note: Specific scores change with version updates. MixEval's dynamic update feature means different versions may have slightly different scores (standard deviation ~0.36 points). Please refer to the [project page](https://mixeval.github.io/) for the latest data.

## Example Questions

Since MixEval's questions come from mixing and matching multiple existing benchmarks, the question styles are diverse:

### Math Reasoning (GSM8K/MATH style)
```
A store offers a 20% discount on a jacket originally priced at $150.
If sales tax is 8%, what is the final price?
```

### Knowledge Understanding (MMLU style)
```
Which of the following best describes the relationship between
photosynthesis and cellular respiration?
A) They are opposite processes
B) They are unrelated
C) One is a subset of the other
D) They produce the same products
```

### Programming (HumanEval style)
```
Write a Python function that takes a list of integers and returns
the longest increasing subsequence.
```

## Variants and Related Benchmarks

| Name | Description | Link |
|------|------|------|
| MixEval-Hard | Hard version, 1,000 questions, difficulty-weighted sampling | Same as above |
| MixEval-X | Multimodal extension (Image2Text, Video2Text, etc.), correlation with Vision Arena reaches 0.98 | https://arxiv.org/abs/2410.13754 |
| Chatbot Arena | MixEval's calibration benchmark, human preference evaluation | https://chat.lmsys.org |
| WildBench | Real user query evaluation, complementary to MixEval | https://github.com/allenai/WildBench |
| Arena-Hard-Auto | Automated version of Chatbot Arena | https://github.com/lmarena/arena-hard-auto |

## Limitations and Controversies

1. **Ground-truth dependency**: Ground-truth-based scoring makes it difficult to evaluate open-ended generation tasks (such as creative writing, dialogue quality), and evaluation of more subjective tasks is not accurate enough
2. **Matching quality**: Semantic matching between internet queries and benchmark questions may not be perfect; some complex queries may be incorrectly matched
3. **Double-edged sword of dynamic updates**: While preventing data contamination, comparability of scores across different versions is affected (although the standard deviation is only 0.36)
4. **English-centric**: Similar to WildBench, the current version primarily covers English queries
5. **Parser dependency**: Using GPT-3.5 as an answer parser may introduce parsing errors, especially for models with irregular output formatting
6. **Question source traceability**: Mixing existing benchmark questions means models may have seen original questions during pre-training, although dynamic updates mitigate this issue
7. **Author institution correction**: Paper authors are from NUS, CMU, AI2, and other institutions, not Western University as cited in some previous references

## Data Sources/References

- Ni, J. et al. "MixEval: Deriving Wisdom of the Crowd from LLM Benchmark Mixtures." NeurIPS 2024. https://arxiv.org/abs/2406.06530
- Ni, J. et al. "MixEval-X: Any-to-Any Evaluations from Real-World Data Mixtures." arXiv:2410.13754, 2024. https://arxiv.org/abs/2410.13754
- MixEval GitHub: https://github.com/Psycoy/MixEval
- MixEval project page: https://mixeval.github.io/
- MixEval dataset: https://huggingface.co/datasets/MixEval/MixEval