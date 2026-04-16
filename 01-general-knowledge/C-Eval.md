# C-Eval — Chinese Comprehensive Evaluation

## Basic Information

| Property | Value |
|----------|-------|
| Full Name | C-Eval: A Multi-Level Multi-Discipline Chinese Evaluation |
| Creator | Shanghai Jiao Tong University et al. (Huang et al.) |
| Release Year | 2023 |
| Number of Questions | 13,948 (52 subjects) |
| Question Type | Four-option multiple choice |
| Dataset Link | https://huggingface.co/datasets/ceval/ceval-exam |
| Paper Link | https://arxiv.org/abs/2305.08322 |
| GitHub | https://github.com/SJTU-LIT/C-Eval |
| Status | No longer maintained (July 2025), test set publicly released |

## Overview

C-Eval is the first large-scale Chinese multi-subject evaluation benchmark, covering 52 subjects across four difficulty levels, designed to assess large language models' Chinese knowledge and reasoning capabilities. As the Chinese version of MMLU, C-Eval enables quantitative comparison of models' Chinese and English capability differences. The C-Eval Hard subset specifically focuses on high-difficulty subjects, maintaining discriminative power for top-tier models.

In July 2025, C-Eval officially announced that the leaderboard would no longer be maintained, and the test set has been publicly released on HuggingFace. This means C-Eval's data contamination risk has further increased, and it is gradually being replaced by other benchmarks such as the MMMLU Chinese subset for frontier model evaluation.

## Dataset Composition

### Four Difficulty Levels

Covering 52 Chinese university subjects, divided into four difficulty levels:

1. **Middle School**: Basic subjects, 9 subjects total
   - Mathematics, Chinese, English, Politics, History, Geography, Physics, Chemistry, Biology
2. **High School**: Advanced subjects, 14 subjects total
   - Mathematics, Chinese, English, Physics, Chemistry, Biology, History, Politics, Geography, Information Technology, General Technology, etc.
3. **College**: Professional subjects, 21 subjects total
   - Computer Science, Electrical Engineering, Mathematics, Physics, Chemistry, Clinical Medicine, Basic Medicine, Economics, Management, Accounting, Law, Marxism, Education, Psychology, etc.
4. **Graduate**: Advanced subjects, 8 subjects total
   - Computer Science, Electrical Engineering, Mathematics, Physics, Clinical Medicine, Management, Economics, Marxism

### C-Eval Hard Subset

C-Eval Hard is a high-difficulty subset selected from the 52 subjects, containing the most challenging subjects for both humans and models:
- Mathematics (High School/College/Graduate)
- Physics (High School/College/Graduate)
- Chemistry (College/Graduate)
- Clinical Medicine (College/Graduate)
- Computer Science (College/Graduate)
- Electrical Engineering (College/Graduate)

C-Eval Hard is the key subset for distinguishing top-tier models, maintaining some discriminative power even after regular C-Eval saturates.

## Evaluation Method

- **Primary Metric**: 5-shot accuracy
- **Scoring Method**: Percentage of correct answers out of total questions per subject, reported by difficulty level
- **Few-shot Setting**: 5-shot (examples selected from dev set)
- **Random Baseline**: 25% (four options)
- **Difficulty-Level Reporting**: Accuracy calculated separately for middle school, high school, college, and graduate levels
- **Hard Subset Reporting**: C-Eval Hard accuracy reported separately

### Scoring Details

| Difficulty Level | Example Subjects | Typical Baseline | Typical Model Performance |
|-----------------|------------------|------------------|--------------------------|
| Middle School | Middle School Math, Middle School Chinese | 25% | High, frontier models > 90% |
| High School | High School Math, High School Physics | 25% | Moderate, frontier models 80-90% |
| College | College Computer Science, Clinical Medicine | 25% | Lower, frontier models 70-85% |
| Graduate | Graduate Math, Graduate Physics | 25% | Lowest, frontier models 50-70% |

## Model Performance (April 2026)

### Full C-Eval

| Model | C-Eval Average | C-Eval Hard | Notes |
|-------|---------------|-------------|-------|
| Qwen3.6 Plus | ~93.3% | — | Chinese-specific optimization |
| Qwen3.5 397B | ~93.0% | — | Chinese-specific optimization |
| Spark4.0 Max (iFLYTEK) | ~91.8% | 80.0% | Chinese-specific optimization |
| Claude Opus 4.5 | ~92.2% | — | — |
| YAYI-Ultra | ~87.7% | 74.0% | — |
| DeepSeek V3 | ~86% | — | — |
| GPT-4 (2023) | 68.7% | 54.9% | Early baseline |
| GPT-4 (2023, Chinese optimized) | ~74% | ~58% | — |

Note: Values with ~ are approximations from unofficial sources or estimates. After July 2025, frontier Western models have rarely submitted formal C-Eval evaluations.

Data sources: C-Eval official leaderboard (cevalbenchmark.com), BenchLM.ai, company technical reports

### Difficulty-Level Performance (GPT-4 as example)

| Difficulty | GPT-4 Accuracy |
|-----------|---------------|
| Middle School | ~72% |
| High School | ~62% |
| College | ~54% |
| Graduate | ~42% |

## Example Questions

### Middle School Math
```
Question: A square has an area of 49 square centimeters. What is its perimeter in centimeters?
A) 14
B) 28
C) 49
D) 7
Answer: B
```

### High School Physics
```
Question: An object with mass 2kg starts from rest and free falls. After 2 seconds, the velocity of the object is (g = 10m/s²)
A) 10 m/s
B) 20 m/s
C) 30 m/s
D) 40 m/s
Answer: B
```

### College Computer Science
```
Question: In a sorted array of length n, the worst-case time complexity of binary search is
A) O(1)
B) O(log n)
C) O(n)
D) O(n log n)
Answer: B
```

### Graduate Mathematics
```
Question: Let A be an n×n real symmetric matrix. Which of the following statements is false?
A) All eigenvalues of A are real
B) Eigenvectors corresponding to different eigenvalues of A are orthogonal
C) A is always diagonalizable
D) The eigenvectors of A are always linearly independent
Answer: D
```

### Clinical Medicine
```
Question: The most common ECG finding in acute myocardial infarction is
A) ST segment elevation
B) T wave inversion
C) QRS complex widening
D) PR interval prolongation
Answer: A
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|---------|-------------|------|
| MMLU | Original English version, 57 subjects | [MMLU.md](MMLU.md) |
| MMMLU | Multilingual version (includes Chinese subset) | [MMMLU.md](MMMLU.md) |
| MMLU-Pro | High-difficulty ten-option version | [MMLU-Pro.md](MMLU-Pro.md) |
| CMMLU | Another Chinese multi-subject evaluation (52 subjects, more focus on Chinese culture) | https://huggingface.co/datasets/haoruiiiii/CMMLU |
| AGIEval | Chinese + English civil service / college entrance exams | https://huggingface.co/datasets/nej/AGIEval |
| Xiezhi | Chinese law-specific evaluation | — |

## Limitations and Controversies

1. **No longer maintained**: Official leaderboard updates stopped in July 2025, test set is publicly released, extremely high data contamination risk
2. **Chinese bias**: Questions are designed around the Chinese mainland education system, not suitable for evaluating knowledge levels in other Chinese-speaking regions (Hong Kong, Taiwan, Singapore, etc.)
3. **Approaching saturation for frontier models**: Chinese-specific optimized models have reached 90%+, discriminative power has significantly decreased
4. **Missing evaluations from Western models**: After 2025, frontier models such as GPT-5, Claude Opus 4.6, Gemini 3 Pro have mostly not formally submitted C-Eval evaluations
5. **Only evaluates multiple choice**: Does not reflect open-ended Q&A, long text generation, and other capabilities
6. **Hard subset still valuable**: Although full C-Eval is saturated, C-Eval Hard still has discriminative power for top-tier models
7. **Overlap with MMMLU Chinese subset**: MMMLU provides an alternative Chinese evaluation within a multilingual framework

## Data Sources / References

- Huang, Y. et al. "C-Eval: A Multi-Level Multi-Discipline Chinese Evaluation Suite for Foundation Models." arXiv 2305.08322, 2023. https://arxiv.org/abs/2305.08322
- C-Eval official leaderboard: https://cevalbenchmark.com/static/leaderboard.html
- C-Eval GitHub: https://github.com/SJTU-LIT/C-Eval
- HuggingFace dataset: https://huggingface.co/datasets/ceval/ceval-exam
- BenchLM C-Eval: https://benchlm.ai/benchmarks/cEval