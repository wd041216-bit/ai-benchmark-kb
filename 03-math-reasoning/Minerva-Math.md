# Minerva-Math — Quantitative Reasoning Evaluation Suite for Language Models

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Minerva Math |
| Creator | Google DeepMind (formerly DeepMind) |
| Release Year | 2022 |
| Number of Problems | ~14,300+ across 4 subsets |
| Problem Type | Free-format math/STEM reasoning problems |
| Dataset Link | https://github.com/google-deepmind/minerva |
| Paper Link | https://arxiv.org/abs/2206.14858 |
| GitHub | https://github.com/google-deepmind/minerva |
| Status | Original subsets approaching saturation; OCWCourses subset still discriminative |

## Overview

Minerva is a mathematical reasoning evaluation system released by Google DeepMind in 2022, originating from the paper *"Solving Quantitative Reasoning Problems with Language Models"* (Lewkowycz et al., NeurIPS 2022). The core finding of this work was that large language models further trained on technical corpora containing large amounts of LaTeX mathematical notation can significantly improve quantitative reasoning ability, without needing any external tools (such as calculators or code interpreters).

Minerva's key contributions include:
- **Chain-of-Thought evaluation paradigm**: Models must generate step-by-step reasoning processes, writing intermediate steps and final answers in LaTeX format
- **Majority Voting**: Sampling multiple solution paths and selecting the most frequently occurring answer (majority@k), significantly improving accuracy
- **pass@k metric**: Measuring the probability of getting at least one correct answer in k samples
- **Technical corpus training**: Continued pretraining on 38.5 billion tokens of arXiv papers and math web pages containing LaTeX/MathJax

## Dataset Composition

The Minerva evaluation suite contains 4 subsets, covering STEM reasoning from elementary school to college level:

| Subset | Problem Source | Number of Problems | Difficulty Level |
|------|---------|---------|---------|
| MATH | Hendrycks et al. MATH dataset | ~5,000 (test set) | High school to competition level |
| GSM8K | OpenAI GSM8K dataset | 1,319 (test set) | Elementary word problems |
| MMLU-STEM | STEM-related subset of MMLU | ~3,000+ | High school to college introductory |
| OCWCourses | MIT OpenCourseWare course problems | 272 | College to graduate level |

> Note: Some modern evaluation frameworks (such as EvalScope) use Minerva-Math specifically to refer to the OCWCourses subset (272 problems), which covers 9 MIT courses: Solid State Chemistry (97 problems), Astronomy (53 problems), Differential Equations (48 problems), Dynamics and Control (26 problems), Microeconomics (18 problems), Special Relativity (11 problems), Physical Chemistry (11 problems), Ecology (5 problems), Information and Entropy (3 problems).

### Characteristics of Each Subset

- **MATH**: Competition-level math problems, 7 subjects, 5 difficulty levels, requiring multi-step reasoning
- **GSM8K**: Elementary school math word problems, 2-8 steps of reasoning, focusing on basic arithmetic
- **MMLU-STEM**: Multiple-choice questions in STEM fields, covering physics, chemistry, biology, computer science, etc.
- **OCWCourses**: College-level course problems, 191 numerical solutions + 81 symbolic solutions, most challenging

## Evaluation Method

1. **Input format**: 0-shot, with prompt "Please reason step by step, and put your final answer within \boxed{}" after the problem
2. **Answer extraction**: Extract the final answer within `\boxed{}` from the model output
3. **Scoring metrics**:
   - **Accuracy**: Exact match accuracy
   - **majority@k (maj1@k)**: Sample k times and take majority vote
   - **pass@k**: Probability of at least one correct answer in k samples
4. **Symbolic answer verification**: Symbolic answers in OCWCourses are verified for equivalence using tools like SymPy
5. **LLM-as-Judge**: Some complex answers use large models to assist in judging

## Model Performance (April 2026)

### Original Minerva Model Results (2022 Release)

| Model | MATH (maj1@k) | GSM8K (maj1@k) | MMLU-STEM (maj1@k) | OCWCourses (maj1@k) |
|------|--------------|----------------|--------------------|--------------------|
| Minerva 540B | 50.3% | 78.5% | 75.0% | 30.8% |
| Minerva 62B | 43.4% | 68.5% | 63.5% | 23.5% |
| Minerva 8B | 25.4% | 28.4% | 43.4% | 12.5% |
| PaLM 540B (no math training) | 8.8% | 56.5% | 58.7% | 7.1% |

### Frontier Model Performance on MATH Subset (2026)

| Model | MATH (full) | GSM8K | MMLU-STEM | OCWCourses |
|------|------------|-------|-----------|------------|
| GPT-5 | ~95% | ~97% | ~93% | ~55% |
| Claude Opus 4.6 | ~94% | ~96% | ~92% | ~50% |
| Gemini 3 Pro | ~93% | ~95% | ~92% | ~48% |
| o3-mini | ~87% | ~95% | ~90% | ~42% |
| DeepSeek V3 | ~85% | ~94% | ~88% | ~40% |
| GPT-4 (2023) | ~52% | ~92% | ~86% | ~30% |
| Minerva 540B (2022) | 50.3% | 78.5% | 75.0% | 30.8% |

Note: Values with ~ are approximate, from unofficial sources or estimates.

Data sources: Minerva original paper (Lewkowycz et al., 2022); 2026 data from public leaderboards and evaluation reports, some are estimates.

## Problem Examples

### MATH Subset — Algebra Level 3
```
Find the value of x that satisfies the equation 4^(x+1) + 4^(x+2) = 20.
Please reason step by step, and put your final answer within \boxed{}.

Answer: \boxed{0}
```

### OCWCourses Subset — Differential Equations
```
Solve the initial value problem: y' + 2y = e^(-t), y(0) = 1.
Please reason step by step, and put your final answer within \boxed{}.

Answer: \boxed{e^{-2t} + te^{-2t}}
```

### GSM8K Subset — Elementary Word Problem
```
Natalia sold clips to 48 of her friends in April, and then she sold half as many clips in May.
How many clips did Natalia sell altogether in April and May?

Answer: \boxed{72}
```

## Variants and Related Benchmarks

- **MATH-500**: 500 representative problems selected from the MATH subset, curated by OpenAI for more efficient evaluation
- **Minerva-Math (EvalScope)**: Specifically refers to the OCWCourses subset (272 problems), available on platforms like ModelScope
- **GPQA**: Graduate-level Google-Proof Q&A, testing deeper STEM reasoning ability, often used alongside Minerva evaluation
- **AIME**: Competition-level math evaluation, better contamination resistance, currently more discriminative
- **FrontierMath**: Research-level math evaluation, far more difficult than Minerva

## Limitations and Controversies

1. **MATH and GSM8K subsets are saturated**: In 2026, frontier models reached ~95% on MATH and ~97% on GSM8K, with extremely low discriminability
2. **Training contamination**: MATH and GSM8K data may have leaked into training sets, affecting evaluation validity
3. **No external tools**: Original Minerva does not allow calculators or code interpreters, limiting model performance on complex numerical calculations
4. **Reasoning process cannot be automatically verified**: Approximately 8% of correct answers are accompanied by incorrect reasoning (false positives), which cannot be verified through formal verification tools
5. **OCWCourses still valuable**: College-level problems still have discriminative value, with frontier models only reaching ~55%

## Data Sources/References

- Lewkowycz, A. et al. "Solving Quantitative Reasoning Problems with Language Models." NeurIPS 2022. https://arxiv.org/abs/2206.14858
- Google Research Blog: Minerva https://research.google/blog/minerva-solving-quantitative-reasoning-problems-with-language-models
- EvalScope Minerva-Math documentation https://evalscope.readthedocs.io/en/latest/benchmarks/minerva_math.html
- ModelScope dataset: knoveleng/Minerva-Math