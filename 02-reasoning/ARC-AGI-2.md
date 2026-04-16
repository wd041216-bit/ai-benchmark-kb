# ARC-AGI-2 — Abstraction and Reasoning Corpus Version 2

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Abstraction and Reasoning Corpus for Artificial General Intelligence, Version 2 |
| Creator | François Chollet / ARC Prize Foundation |
| Release Year | March 2025 |
| Number of Problems | 1,000 (training) + 360 (evaluation, split into three subsets of 120 each) |
| Problem Type | Visual pattern recognition and reasoning (grid transformation) |
| Dataset Link | https://github.com/fchollet/ARC-AGI |
| Paper Link | https://arcprize.org/blog/announcing-arc-agi-2-and-arc-prize-2025 |
| GitHub | https://github.com/fchollet/ARC-AGI |
| Website | https://arcprize.org |
| Status | ✅ Highly discriminative (frontier models pure LLM 0%, with reasoning ~4%, humans 100%) |

## Overview

ARC-AGI-2 is a new version of ARC-AGI released in March 2025, and is currently the **most important new reasoning evaluation benchmark**. It inherits ARC-AGI's core philosophy of testing abstract reasoning ability, but through significant improvements in evaluation design, it makes frontier models (including GPT-5, Claude Opus 4.5, Gemini 3, etc.) fail almost completely (0%) in pure LLM mode, and even with reasoning and search tools they can only reach about 4%. Meanwhile, human testers perform nearly perfectly (100%).

ARC-AGI-2 is designed to test **general abstract reasoning ability** — the ability to discover patterns from a small number of examples and apply them to new situations. This ability is a core component of human intelligence, but current AI systems still severely lack it.

### Key Differences from ARC-AGI-1

| Feature | ARC-AGI-1 (2019) | ARC-AGI-2 (2025) |
|------|-----------------|-----------------|
| Evaluation set size | 400 (training) + 400 (evaluation) | 1,000 (training) + 360 (evaluation) |
| Evaluation subsets | Single evaluation set | Three subsets of 120 each (public/semi-private/private) |
| Brute-force search resistance | Partial | Complete (removed easily brute-forced problems) |
| Human calibration | None | Yes (400+ human testers verified) |
| Frontier model performance | ~5% | Pure LLM 0%, reasoning ~4% |
| Human performance | ~98% | 100% (with ≥2 person groups) |
| Knowledge exploitation risk | Low | Medium (discovered models may "overfit" through knowledge) |

### Three Key AI Weaknesses Identified by ARC-AGI-2

1. **Symbolic Interpretation**: AI cannot assign semantic meaning to symbols themselves
2. **Compositional Reasoning**: AI struggles to simultaneously apply multiple rules or handle interactions between rules
3. **Contextual Rule Application**: AI tends to capture surface patterns rather than understanding underlying selection principles

## Dataset Composition

ARC-AGI-2's dataset went through a rigorous calibration process:

| Dataset | Number of Problems | Calibration | Visibility | Purpose |
|--------|---------|------|--------|------|
| Training set | 1,000 | Uncalibrated | Public | Teaching core knowledge priors |
| Public evaluation set | 120 | Calibrated | Public | Evaluation |
| Semi-private evaluation set | 120 | Calibrated | Private | Kaggle live leaderboard |
| Private evaluation set | 120 | Calibrated | Private | Kaggle final ranking |

### Human Calibration Process

- **400+ human testers** participated in calibration
- Each problem must satisfy: ≥2 human testers solving correctly within 2 attempts
- Ensures problem distribution meets IID (independent and identically distributed) conditions
- Calibration results show human accuracy of **100%** (under ≥2 person group conditions)

### Problem Format

Each problem contains:
- 2-5 input-output example pairs (demonstration examples)
- 1 test input
- The model must predict the correct test output

All inputs and outputs are integer grids (typically using 0-9 to represent 10 colors).

## Evaluation Method

- **Primary metric**: pass@2 accuracy (2 submissions allowed, best result taken)
- **Evaluation subset**: Semi-private evaluation set (120 problems) for Kaggle leaderboard
- **Scoring method**: Correctly passing all test cases counts as 1 point, total score = correct problems / total problems
- **Human rules**: 2 attempts allowed, consistent with AI evaluation conditions
- **Efficiency metric**: Inference cost per task (USD/task) is also reported

### Calibration and Comparability

The three calibrated evaluation sets (public/semi-private/private) have problem distributions that meet IID conditions, meaning **non-overfitted scores should be directly comparable across the three sets**, resolving the issue in ARC-AGI-1 where scores across different subsets were not comparable.

## Model Performance (April 2026)

### Commercial Models

| Model | ARC-AGI-1 | ARC-AGI-2 | Cost/Task |
|------|----------|----------|----------|
| Gemini 3 Pro + Poetiq refinement | ~75% | **54%** | $30 |
| Claude Opus 4.5 (thinking mode, 64k) | ~60% | **37.6%** | $2.20 |
| Gemini 3 Pro (baseline) | ~50% | **31%** | $0.81 |
| o3-preview-low (CoT + search) | ~75% | **~4%** | $200 |
| o1-pro (CoT + search) | ~50% | **~1%** | ~$200 |
| o3-mini-high (single CoT) | ~35% | **0.0%** | $0.41 |
| r1 / r1-zero (single CoT) | ~15% | **0.3%** | $0.08 |
| GPT-4.5 (pure LLM) | ~10% | **0.0%** | $0.29 |
| **Humans (≥2)** | **98%** | **100%** | **$17** |
| **Humans (average)** | **64.2%** | **60%** | **$17** |

Note: Values with ~ are approximate, from unofficial sources or estimates. Pure LLM scores 0% on ARC-AGI-2.

Data sources: ARC Prize official blog (arcprize.org), ARC Prize 2025 competition results

### Competition Rankings (ARC Prize 2025)

| Rank | Team | ARC-AGI-2 Score | Cost/Task |
|------|------|---------------|----------|
| 1 | NVARC | **24.03%** | $0.20 |
| 2 | the ARChitects | **16.53%** | — |
| 3 | MindsAI & Tufa Labs | **12.64%** | — |
| 4 | Lonnie | **6.67%** | — |
| 5 | G. Barbadillo | **6.53%** | — |

Data source: Kaggle ARC Prize 2025 competition leaderboard

### Paper Awards (2025)

| Award | Paper | Core Method | ARC-AGI-1 | ARC-AGI-2 | Parameters |
|------|------|---------|----------|----------|--------|
| First Prize ($50K) | TRM (Jolicoeur-Martineau) | Recursive fine-tuning of small models | ~45% | ~8% | 7M |
| Second Prize ($20K) | SOAR (Pourcel et al.) | Self-improving evolutionary program synthesis | ~52% | — | — |
| Third Prize ($5K) | CompressARC (Liao & Gu) | MDL neural system | ~20-34% | ~4% | 76K |

## Problem Examples

### Example 1 (Simple Transformation)

```
Demo Example 1:
Input:           Output:
[0,0,0]        [0,1,0]
[0,1,0]   →    [1,1,1]
[0,0,0]        [0,1,0]

Demo Example 2:
Input:           Output:
[0,0,0,0]      [0,0,1,0]
[0,1,1,0]  →   [0,1,1,0]
[0,0,0,0]      [0,0,1,0]

Test Input:
[0,0,0,0,0]
[0,0,0,1,0]
[0,0,0,0,0]
[0,1,0,0,0]

(The model must predict the correct output)
```

Rule: The cell represented by 1 is expanded into a cross shape (3×3 plus pattern)

### Example 2 (Compositional Reasoning — Key Focus of ARC-AGI-2)

```
Demo Example 1:
Input:              Output:
[0,0,2,0,0]       [0,0,3,0,0]
[0,0,0,0,0]  →    [0,3,3,3,0]
[0,0,0,0,0]       [0,0,3,0,0]

Rule: Expand each single pixel of each color into a shape of corresponding size,
while preserving original color relationships.
```

### Example 3 (Contextual Rule Application — Key Focus of ARC-AGI-2)

```
This type requires the model to understand the selection principles for rules
in specific contexts, rather than mechanically applying surface patterns.
In multiple demonstration examples, seemingly identical patterns may require
different transformation rules depending on the situational context.
```

## Variants and Related Benchmarks

| Variant | Description |
|------|------|
| **ARC-AGI-1** | Original version (2019), 400+400 problems, see [ARC-AGI.md](ARC-AGI.md) |
| **ARC-AGI-3** | Expected release in early 2026, will shift to interactive reasoning (exploration, planning, memory, goal acquisition) |
| **ARC Prize Competition** | Annual competition, $1M+ prize pool, see below |
| **ConceptARC** | ARC subset organized by concept type |
| **1D-ARC** | One-dimensional version of ARC tasks |

### ARC Prize Competition

- **Total Prize**: $1,000,000+
- **Grand Prize**: $700,000 (requires >85% within Kaggle efficiency limits)
- **Highest Score Prize**: $75,000
- **Paper Prize**: $50,000
- **2025 Competition**: 1,455 teams, 15,154 submissions
- **Grand Prize Status**: Still unclaimed (highest score in 2025 was 24.03%)
- **2025 Key Finding**: "Refinement loops" became the mainstream approach

## Why ARC-AGI-2 is the Most Important New Reasoning Benchmark in 2025

1. **Largest AI-Human Gap**: Frontier AI ~0-4%, humans 100% — one of the largest capability gaps across all benchmarks
2. **Pure LLM Completely Fails**: GPT-4.5, GPT-4o and other pure language models score 0%, proving ARC-AGI-2 successfully avoids knowledge retrieval shortcuts
3. **Contamination-Resistant**: Private evaluation set + human calibration ensures reliability of evaluation results
4. **Measures General Intelligence**: Tests the core ability to learn new rules from few examples
5. **Cannot Be Cheated**: Each problem is an entirely new pattern, unsolvable through memorizing training data
6. **AGI Indicator**: If AI reaches human level on ARC-AGI-2, it signifies a major intelligence breakthrough
7. **Industry Consensus**: All four major AI labs (OpenAI, Anthropic, Google DeepMind, xAI) report ARC-AGI scores in their model cards
8. **Efficiency Gap**: Humans solve at $17/task, AI needs at minimum $2.20/task but still cannot reach human accuracy

### Key Trends in 2025

1. **Refinement Loop**: Mainstream approach shifted from single-pass reasoning to iterative refinement (explore → verify → repeat)
2. **Zero-Pretraining Deep Learning**: Methods like CompressARC prove that some ARC tasks can be solved without pretraining
3. **Knowledge Overfitting Risk**: Discovered that models may "overfit" ARC through broad domain knowledge rather than genuine reasoning
4. **Efficiency Still Limited by Scientific Breakthroughs**: Capability gap is mainly narrowed through engineering, while the efficiency gap requires scientific innovation

## Limitations and Controversies

1. **Limited Problem Count**: The evaluation set has only 360 problems (three 120-problem subsets), small sample size leads to wide confidence intervals
2. **Special Format**: Grid transformation tasks have a debatable direct correspondence to real-world tasks
3. **Purely Visual**: Does not involve language understanding, some argue it is not comprehensive enough
4. **Knowledge Overfitting**: In 2025, it was discovered that models may use pretraining knowledge to solve some problems rather than true abstract reasoning
5. **Refinement Loop Controversy**: Adding refinement loops significantly boosts scores (31%→54%), some argue this is more like engineering optimization than intelligence improvement
6. **Cost Asymmetry**: Humans solve at $17/task, while top AI solutions need $2.20-$30/task with lower accuracy
7. **Evaluation Condition Controversy**: Different prompting strategies and tool usage methods produce widely varying scores

## Data Sources/References

- ARC Prize official announcement: https://arcprize.org/blog/announcing-arc-agi-2-and-arc-prize-2025
- ARC Prize 2025 competition results: https://arcprize.org/blog/arc-prize-2025-results-analysis
- ARC-AGI-2 dataset: https://github.com/fchollet/ARC-AGI
- Chollet, "On the Measure of Intelligence," arXiv 2019. https://arxiv.org/abs/1911.01547
- Kaggle ARC Prize 2025: https://www.kaggle.com/c/arc-prize-2025