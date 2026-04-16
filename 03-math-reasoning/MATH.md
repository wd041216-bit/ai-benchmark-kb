# MATH — Mathematics Problem Solving

## Basic Information

| Property | Value |
|------|-----|
| Full Name | MATH Dataset |
| Creator | Hendrycks et al. (UC Berkeley) |
| Release Year | 2021 |
| Number of Problems | 12,500 |
| Problem Type | Free-format math proof/calculation problems |
| Dataset Link | https://huggingface.co/datasets/HuggingFaceH4/MATH-500 |
| Paper Link | https://arxiv.org/abs/2103.03874 |
| Status | ⚠️ Approaching saturation (top models > 90% on MATH-500) |

## Evaluation Dimensions

Covers high school to college-level math problems, divided into 7 difficulty levels and multiple subjects:

### Subject Categories
1. **Algebra**: Equations, inequalities, polynomials
2. **Counting & Probability**: Combinatorics, permutations, probability
3. **Geometry**: Plane geometry, solid geometry, analytic geometry
4. **Number Theory**: Divisibility, primes, congruences
5. **Prealgebra**: Basic operations, fractions, percentages
6. **Precalculus**: Functions, trigonometry, series
7. **Other (IntermAlgebra, etc.)**

### Difficulty Levels
- Level 1: Easiest
- Level 5: Hardest
- Level 5 problems approach AIME competition difficulty

## Problem Examples

### Algebra Level 3
```
Find the value of x that satisfies the equation 4^(x+1) + 4^(x+2) = 20.

Answer: 0
```

### Geometry Level 4
```
In triangle ABC, AB = 13, BC = 14, and CA = 15. Find the area of the triangle.

Answer: 84
```

### Number Theory Level 5
```
Find the remainder when 2^2024 is divided by 1000.

Answer: 976
```

## Scoring Method

- **Primary metric**: Accuracy
- **Scoring method**: Exact match of the final answer
- **Typical setup**: 4-shot + Chain-of-Thought
- **MATH-500**: 500 representative problems selected from MATH

## Model Performance (April 2026)

| Model | MATH (full) | MATH-500 |
|------|------------|---------|
| GPT-5 | ~95% | ~96% |
| Claude Opus 4.6 | ~94% | ~95% |
| Gemini 3 Pro | ~93% | ~94% |
| o3-mini | ~87% | ~88% |
| DeepSeek V3 | ~85% | ~86% |
| GPT-4 (2023) | ~52% | ~55% |
| Human competitors | ~40% (Level 5) | - |

## Variants

### MATH-500
- 500 problems selected from MATH by OpenAI
- More representative, faster evaluation
- **Dataset**: https://huggingface.co/datasets/HuggingFaceH4/MATH-500

### Minerva Math
- Google DeepMind's math evaluation variant
- Includes more competition-level problems
- Uses a different scoring protocol

## Relationship with AIME

- MATH Level 5 problems have difficulty approaching AIME
- But AIME problems are newer and better protected against contamination
- It is recommended to use both MATH-500 and AIME for math ability evaluation

## Limitations

1. **Approaching Saturation**: Top models have exceeded 95% on MATH-500
2. **Answer Format Sensitivity**: Requires exact matching
3. **Training Contamination**: Large amounts of MATH data may appear in training sets
4. **Numeric Answers Only**: Does not evaluate proof processes