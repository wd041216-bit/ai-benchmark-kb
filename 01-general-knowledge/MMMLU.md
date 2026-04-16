# MMMLU — Multilingual Comprehensive Knowledge Evaluation

## Basic Information

| Property | Value |
|----------|-------|
| Full Name | Massive Multitask Language Understanding (Multilingual) |
| Creator | OpenAI |
| Release Year | 2024 |
| Number of Questions | ~14,042 / per language |
| Question Type | Four-option multiple choice |
| Number of Languages | 14 |
| Dataset Link | https://huggingface.co/datasets/openai/MMMLU |
| Paper Link | https://arxiv.org/abs/2412.03304 |
| GitHub | https://github.com/openai/simple-evals |
| Status | Active, important benchmark for multilingual model evaluation |

## Overview

MMMLU is the multilingual version of MMLU, released by OpenAI. It translates MMLU's test questions into 14 languages through **professional human translation**, maintaining the same 57 subjects and four-option structure as the original MMLU. MMMLU enables models' multilingual knowledge capabilities to be compared within a unified framework, serving as a core benchmark for evaluating cross-lingual knowledge transfer capabilities.

Unlike machine-translated datasets, MMMLU uses human translation to ensure semantic accuracy and cultural adaptation of questions, reducing translation noise interference with evaluation results.

## Dataset Composition

### Language Coverage

| Language Code | Language | Resource Category |
|--------------|----------|-------------------|
| AR_XY | Arabic | Medium-resource |
| BN_BD | Bengali | Low-resource |
| DE_DE | German | High-resource |
| ES_LA | Spanish | High-resource |
| FR_FR | French | High-resource |
| HI_IN | Hindi | Medium-resource |
| ID_ID | Indonesian | Medium-resource |
| IT_IT | Italian | High-resource |
| JA_JP | Japanese | High-resource |
| KO_KR | Korean | High-resource |
| PT_BR | Brazilian Portuguese | High-resource |
| SW_KE | Swahili | Low-resource |
| YO_NG | Yoruba | Low-resource |
| ZH_CN | Simplified Chinese | High-resource |

### Subject Structure

Consistent with the original MMLU, covering 57 subjects divided into four major categories:
- **STEM**: Mathematics, Physics, Chemistry, Biology, Computer Science, etc.
- **Humanities**: History, Philosophy, Religion, etc.
- **Social Sciences**: Politics, Economics, Psychology, Sociology, etc.
- **Other Professional Fields**: Law, Medicine, Accounting, Engineering, etc.

## Evaluation Method

- **Primary metric**: Accuracy, reported per language
- **Scoring method**: Percentage of correct answers out of total questions for that language
- **Few-shot setting**: Typically uses 5-shot
- **Random baseline**: 25% (four options)
- **Aggregate metric**: Average accuracy across 14 languages

## Model Performance (April 2026)

### Frontier Model Comparison

| Model | MMMLU Average Accuracy | Notes |
|-------|----------------------|-------|
| Gemini 3.1 Pro | ~92.6% | Current highest |
| Gemini 3 Pro | ~91.8% | — |
| Gemini 3 Flash | ~91.8% | — |
| Claude Opus 4.6 | ~91.1% | — |
| Claude Opus 4.5 | ~90.8% | — |
| GPT-5.2 | ~89.6% | — |
| Claude Sonnet 4.6 | ~89.3% | — |
| o3-high | ~88.8% | OpenAI reasoning model |
| GPT-4.5 | ~85.1% | — |
| GPT-4.1 | ~83.7% | — |

Note: Values with ~ are approximations from unofficial sources or estimates.

Data sources: llm-stats.com MMMLU Leaderboard, OpenAI simple-evals, company technical reports

### Low-Resource vs High-Resource Language Performance Gap (using o3-high as example)

| Language Category | Representative Language | o3-high Accuracy |
|-------------------|------------------------|-----------------|
| High-resource | Italian | 91.2% |
| High-resource | Spanish | 91.1% |
| High-resource | French | 90.6% |
| Medium-resource | Arabic | 90.4% |
| Medium-resource | Hindi | 89.8% |
| Low-resource | Swahili | 86.0% |
| Low-resource | Yoruba | 78.0% |

The gap between high-resource and low-resource languages can reach 10-13 percentage points, reflecting language imbalance in model training data.

## Example Questions

### Chinese (ZH_CN) Math Category
```
Question: If f(x) = x^2 + 3x + 2, then f(x+1) =
A) x^2 + 5x + 6
B) x^2 + 5x + 4
C) x^2 + 3x + 6
D) x^2 + 3x + 4
Answer: A
```

### Japanese (JA_JP) Law Category
```
Question: Which of the following is a necessary element for a valid contract?
A) Written documentation
B) Consideration
C) Notarization
D) Witness signatures
Answer: B
```

### Arabic (AR_XY) Computer Science Category
```
Question: What is the worst-case time complexity of quicksort?
A) O(n)
B) O(n log n)
C) O(n^2)
D) O(2^n)
Answer: C
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|---------|-------------|------|
| MMLU | Original English version | [MMLU.md](MMLU.md) |
| MMLU-Pro | High-difficulty ten-option version | [MMLU-Pro.md](MMLU-Pro.md) |
| Global-MMLU | Released by Cohere For AI, focused on cultural bias | https://huggingface.co/datasets/CohereForAI/Global-MMLU |
| C-Eval | Chinese-specific evaluation | [C-Eval.md](C-Eval.md) |

## Limitations and Controversies

1. **Cultural bias**: Global-MMLU research found that ~28% of MMLU questions contain culturally sensitive content, and 84.9% of geography questions focus on North America or Europe; translated versions may not accurately reflect non-Western knowledge systems
2. **Translation quality**: Although human translation is used, the equivalence of certain subject terminology across languages remains debated
3. **Saturation trend**: Top models have reached 90%+ on high-resource languages, and discriminative power is beginning to decline
4. **Only evaluates multiple choice**: Does not reflect open-ended Q&A, long text generation, and other capabilities
5. **Unstable low-resource language evaluation**: Evaluation variance for low-resource languages like Yoruba is relatively high
6. **Data contamination**: Shares the same questions as MMLU (only translated), original English questions may have appeared in training data

## Data Sources / References

- OpenAI. "MMMLU Dataset." https://huggingface.co/datasets/openai/MMMLU
- OpenAI simple-evals: https://github.com/openai/simple-evals
- MMMLU paper: https://arxiv.org/abs/2412.03304
- Global-MMLU (Cohere For AI, 2025): Cultural bias analysis
- llm-stats.com MMMLU Leaderboard: https://llm-stats.com/benchmarks/mmmlu