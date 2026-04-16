# GPQA — Graduate-Level Google-Proof Q&A

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Graduate-Level Google-Proof Question Answering Benchmark |
| Creator | NYU, Cohen et al. |
| Release Year | 2023 |
| Number of Problems | 448 (Diamond subset) |
| Problem Type | Multiple-choice questions with four options |
| Dataset Link | https://huggingface.co/datasets/ankner/gpqa |
| Paper Link | https://arxiv.org/abs/2311.12022 |
| Status | ✅ Still discriminative (top models < 95%) |

## Evaluation Dimensions

GPQA specifically tests doctoral-level expert knowledge, with problems distributed across three major domains:

### Physics
- Quantum mechanics, particle physics, condensed matter physics, astrophysics, etc.
- ~150 problems

### Chemistry
- Organic chemistry, inorganic chemistry, physical chemistry, biochemistry, etc.
- ~150 problems

### Biology
- Molecular biology, genetics, cell biology, ecology, etc.
- ~150 problems

## Core Feature: Google-Proof

**Key Innovation**: Problems are designed so that answers are difficult to find even with internet search

1. **Expert-authored**: Each problem is written by a doctoral-level expert in the relevant field
2. **Peer verification**: Experts in other fields attempt to answer, averaging only 34% correct
3. **Search-resistant design**: Problems are not simple knowledge retrieval; they require reasoning and integration
4. **High discriminability**: Random guessing 25%, non-domain experts 34%, domain experts 65%

## Problem Examples

### Physics
```
Question: In quantum mechanics, which of the following is true about the energy eigenstates of a particle in a one-dimensional infinite potential well?
A) The energy levels are equally spaced
B) The ground state energy is zero
C) The energy spacing increases with quantum number
D) All eigenstates have the same energy
Answer: C
```

### Chemistry
```
Question: Which of the following statements about the Diels-Alder reaction is correct?
A) It requires a Lewis acid catalyst
B) It proceeds through a concerted [4+2] cycloaddition mechanism
C) It can only occur with electron-rich dienes
D) The endo product is always the thermodynamic product
Answer: B
```

## Scoring Method

- **Primary metric**: Accuracy
- **Subset**: Diamond (448 problems) is the most commonly used, with additional screening to ensure problem quality
- **Scoring method**: Percentage of correct answers out of total problems

## Model Performance (April 2026)

| Model | GPQA Diamond |
|------|-------------|
| GPT-5.4 | 92.0% |
| Gemini 3 Pro | 94.3% |
| Claude Opus 4.6 | 92.8% |
| GPT-5 | ~88% |
| DeepSeek R1 | ~72% |
| Non-domain Expert Humans | 34% |
| Domain Expert Humans | 65% |
| Random Guessing | 25% |

## Variants

### GPQA Extended
- Full dataset, containing more problems
- ~544 problems

### GPQA Diamond
- The most widely used subset
- 448 problems, strictly quality-filtered
- Each problem has a correct answer annotated by domain experts

## Why GPQA is Important

1. **Contamination-resistant**: Google-Proof design makes it impossible to get answers through simple search
2. **High discriminability**: In 2026, top models are at 90-94%, still room for improvement
3. **Genuine Difficulty**: Problems require real domain knowledge and reasoning ability
4. **Has Replaced MMLU**: Has become a replacement or supplement for MMLU in many technical reports

## Limitations

1. **Narrow Domain Coverage**: Only covers physics, chemistry, and biology
2. **Limited Problem Count**: Diamond has only 448 problems
3. **Unstable Scoring**: Small sample size leads to wide confidence intervals
4. **High Expert Annotation Cost**: Difficult to scale