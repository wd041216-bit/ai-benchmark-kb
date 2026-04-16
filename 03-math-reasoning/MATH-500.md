# MATH-500 — Curated Representative Subset of MATH

## Basic Information

| Property | Value |
|------|-----|
| Full Name | MATH-500 |
| Creator | OpenAI |
| Release Year | 2023 |
| Number of Problems | 500 |
| Problem Type | Free-format math reasoning problems |
| Dataset Link | https://huggingface.co/datasets/HuggingFaceH4/MATH-500 |
| Paper Link | https://arxiv.org/abs/2305.20050 |
| GitHub | https://github.com/openai/prm800k |
| Status | ⚠️ Approaching saturation (frontier models > 95%) |

## Overview

MATH-500 is an evaluation subset of 500 math problems selected from Hendrycks et al.'s MATH dataset by OpenAI, first appearing in OpenAI's paper *"Let's Verify Step by Step"* (Lightman et al., 2023). This subset aims to provide a **moderately sized and representative** math reasoning evaluation, making the evaluation process faster and more reproducible.

MATH-500's core design philosophy:
- Selects 500 problems from the MATH test set, preserving the **difficulty distribution** and **subject distribution** of the original dataset
- Difficulty leans toward mid-to-high levels (Level 3-5 accounts for ~73%), so the average difficulty is higher than the full MATH dataset
- Highly correlated with the full MATH evaluation, can be used as a quick proxy evaluation
- Has become one of the standard evaluation benchmarks for OpenAI's o1/o3 series reasoning models

## Dataset Composition

### Basic Fields

Each problem contains the following information:
- **problem**: Math problem statement
- **solution**: Complete solution process
- **answer**: Extracted short final answer
- **subject**: Math subject classification
- **level**: Difficulty level (1-5)
- **unique_id**: Unique identifier in the original dataset

### Subject Distribution

Covers 7 subjects from the MATH dataset:
1. Algebra
2. Counting & Probability
3. Geometry
4. Intermediate Algebra
5. Number Theory
6. Prealgebra
7. Precalculus

### Difficulty Distribution

| Difficulty Level | Number of Problems | Proportion | Average Problem Length |
|---------|---------|------|------------|
| Level 1 (easiest) | 43 | 8.6% | ~193 characters |
| Level 2 | 90 | 18.0% | ~219 characters |
| Level 3 | 105 | 21.0% | ~236 characters |
| Level 4 | 128 | 25.6% | ~277 characters |
| Level 5 (hardest) | 134 | 26.8% | ~337 characters |

> Note: Difficulty distribution leans toward mid-to-high levels (Level 3-5 accounts for ~73%), making MATH-500's average difficulty higher than the full MATH dataset.

## Evaluation Method

1. **Input format**: 0-shot, typically with prompt "Please reason step by step, and put your final answer within \boxed{}"
2. **Answer extraction**: Extract the final answer within `\boxed{}` from the model output
3. **Scoring method**: Exact match of the final answer
4. **Primary metric**: Accuracy (%)
5. **Evaluation advantage**: 500 problems makes evaluation time significantly shorter, suitable for quick iteration and reproducible experiments

## Model Performance (April 2026)

| Model | MATH-500 Accuracy | Reasoning Type |
|------|---------------|---------|
| o3 | ~99% | Reasoning model |
| o3-mini | ~97.9% | Reasoning model |
| DeepSeek R1-0528 | ~97.8% | Reasoning model |
| DeepSeek R1 | ~97.3% | Reasoning model |
| o4-mini | ~97.3% | Reasoning model |
| o1 | ~96.4% | Reasoning model |
| Gemini 3 Pro | ~96% | Standard model |
| GPT-5.4 | ~95.5% | Standard model |
| Gemini 2.5 Pro | ~95.2% | Standard model |
| Grok 4 | ~95% | Standard model |
| Claude Opus 4.6 | ~95% | Standard model |
| o1 Preview | ~94.8% | Reasoning model |
| o1-mini | ~90% | Reasoning model |
| GPT-4 (2023) | ~55% | Standard model |
| Human competitors (Level 5) | ~40% | - |

Note: Values with ~ are approximate, from unofficial sources or estimates.

Data sources: OpenAI o1 technical report; Vals AI leaderboard (archived as of April 2026); LM Market Cap leaderboard; PricePerToken leaderboard. Some data are results under different evaluation conditions and may have minor differences.

## Problem Examples

### Algebra Level 2
```
Find all real solutions to the equation x^2 - 5x + 6 = 0.

Answer: \boxed{2, 3}
```

### Number Theory Level 4
```
Find the remainder when 2^2024 is divided by 1000.

Answer: \boxed{976}
```

### Counting & Probability Level 5
```
A fair 6-sided die is rolled 7 times. What is the probability that the
sum of the rolls is divisible by 7?

Answer: \boxed{\frac{1}{7}}
```

## Variants and Related Benchmarks

- **MATH (Full)**: Original 12,500-problem dataset, MATH-500 is its subset
- **Minerva Math**: Google DeepMind's math evaluation suite, where the MATH subset overlaps with MATH-500
- **AIME**: American Invitational Mathematics Examination evaluation, 15 problems per year, far better contamination resistance than MATH-500
- **FrontierMath**: Research-level math evaluation, extremely high difficulty, currently most discriminative
- **MATH-Hard**: Subset containing only Level 4-5 problems, slightly more discriminative than MATH-500
- **GSM8K**: Elementary school math word problems, fully saturated as of 2026

## Limitations and Controversies

1. **Approaching Saturation**: In 2026, frontier models have reached 95-99%, with extremely low discriminability; Vals AI has archived it as "saturated"
2. **Training Contamination Risk**: Problems are publicly accessible and may have leaked into training data
3. **Leans Toward Mid-High Difficulty**: Level 3-5 accounts for 73%, not fully representative of the full MATH dataset's difficulty distribution
4. **Numeric Answers Only**: Does not evaluate the correctness of proof processes or reasoning steps
5. **Limited Sample Size**: 500 problems, while more than AIME (15 problems), still has limited statistical significance
6. **Recommended Alternatives**: Suggest using AIME and FrontierMath alongside other more discriminative math evaluations

## Data Sources/References

- Lightman, H. et al. "Let's Verify Step by Step." arXiv:2305.20050, 2023. https://arxiv.org/abs/2305.20050
- Hendrycks, D. et al. "Measuring Mathematical Problem Solving with the MATH Dataset." NeurIPS 2021. https://arxiv.org/abs/2103.03874
- HuggingFaceH4/MATH-500 dataset https://huggingface.co/datasets/HuggingFaceH4/MATH-500
- OpenAI PRM800K repository https://github.com/openai/prm800k
- Vals AI MATH-500 leaderboard (archived) https://www.vals.ai/benchmarks/math500