# WinoGrande — Large-Scale Adversarial Coreference Resolution Reasoning

## Basic Information

| Property | Value |
|------|-----|
| Full Name | WinoGrande: An Adversarial Winograd Schema Challenge at Scale |
| Creator | Allen AI (Sakaguchi et al.) |
| Release Year | 2019 |
| Number of Problems | 44K (full), 1,263 (standard test set) |
| Problem Type | Binary choice cloze (coreference resolution) |
| Dataset Link | https://huggingface.co/datasets/winogrande |
| Paper Link | https://arxiv.org/abs/1907.10641 |
| GitHub | https://github.com/allenai/winogrande |
| Status | ⚠️ Frontier models approaching saturation (~88-92%), humans 94% |

## Overview

WinoGrande is a large-scale extension of the classic Winograd Schema Challenge (WSC), expanding the original WSC's hundreds of problems to 44K, and introducing the Adversarial Filtering (AfLite) algorithm to eliminate statistical shortcuts in the dataset. Its core task is **coreference resolution** — determining which noun a pronoun refers to in a sentence.

Unlike the original WSC, WinoGrande collects a large number of new problems through crowdsourcing, then uses an algorithm to filter out "easy problems" that can be solved by statistical patterns, ensuring that only problems requiring genuine commonsense reasoning are retained.

### Core Evaluation Dimensions

1. **Commonsense Reasoning**: Using world knowledge to determine pronoun reference
2. **Language Understanding**: Understanding sentence structure and semantic relationships
3. **Resistance to Statistical Shortcuts**: Adversarial debiasing ensures models cannot answer through surface patterns
4. **Robustness**: Performance significantly drops on paraphrased versions (WinoWhat)

## Dataset Composition

WinoGrande provides multiple subsets covering different scale requirements:

| Subset | Number of Problems | Purpose |
|------|---------|------|
| winogrande_xl | 40,928 | Large-scale training/evaluation |
| winogrande_l | 8,988 | Medium scale |
| winogrande_m | 2,981 | Medium scale |
| winogrande_s | 1,621 | Small scale |
| winogrande_xs | 1,263 | Standard test set (most commonly used) |
| winogrande_debiased | 1,263 | Debiased version |

Each problem contains:
- A sentence containing a pronoun
- Two candidate nouns
- A correct answer label

### Adversarial Debiasing (AfLite)

WinoGrande's key innovation is the AfLite (Adversarial Filtering of Length-conflicting Attributes) algorithm:
1. Train multiple shallow classifiers to identify statistical shortcuts in the data
2. Remove problems that can be exploited by shallow models
3. Retain problems that require deep reasoning
4. Ensure the two options have balanced positional distribution in the sentence

## Evaluation Method

- **Primary metric**: Accuracy
- **Evaluation subset**: winogrande_xs (1,263 problems) is the most commonly used standard test set
- **Scoring method**: Percentage of correct answers out of total problems
- **AUC metric**: The official leaderboard also reports AUC scores across different-sized subsets
- **Standard evaluation**: 5-shot evaluation is most commonly used
- **Human baseline**: 94.0% (reported in original paper)

### Considerations

Different evaluation methods produce significant differences:
- Standard 5-shot evaluation: Frontier models typically reach ~88-92%
- Open-ended Q&A (OSQ-Bench) method: Scores significantly lower (~63-72%)
- Paraphrased version (WinoWhat): All models show significantly degraded performance

## Model Performance (April 2026)

### Frontier Models (Standard 5-shot Evaluation)

| Model | WinoGrande | Notes |
|------|-----------|------|
| GPT-4 | ~87.5% | From OpenAI technical report |
| Claude 3 Opus | ~88.5% | From Anthropic model card |
| GPT-4o mini | ~88.7% | BAUS.AI leaderboard |
| Qwen 3.5 397B-A17B | ~85.3% | BAUS.AI leaderboard |
| GPT-4o | ~84.6% | BAUS.AI leaderboard |
| Llama 3.1 405B | ~83.8% | BAUS.AI leaderboard |
| Gemini 1.5 Pro | ~81.8% | BAUS.AI leaderboard |
| Humans | 94.0% | Original paper |

Note: Values with ~ are approximate, from unofficial sources or estimates.

Data sources: Allen AI official leaderboard, Anthropic model card, BAUS.AI leaderboard

### Early Models (Official Leaderboard, AUC Metric)

| Model | AUC | Acc (XS) | Acc (S) | Acc (M) | Acc (L) | Acc (XL) |
|------|-----|----------|---------|---------|---------|----------|
| NUDT NLP | 0.8829 | 0.8342 | 0.8546 | 0.8930 | 0.9111 | 0.9111 |
| T5-XXL | 0.8773 | 0.8240 | 0.8478 | 0.8947 | 0.8998 | 0.9100 |
| UNICORN | 0.8664 | 0.7923 | 0.8359 | 0.8732 | 0.9038 | 0.9128 |

Data source: Allen AI official leaderboard (leaderboard.allenai.org/winogrande)

### Saturation Note

WinoGrande is approaching saturation:
- Between 2024-2025, frontier model reported scores have approached human level (94%)
- Most frontier models (GPT-5, Claude Opus 4.6, Gemini 3 Pro, etc.) no longer report WinoGrande scores in their technical reports
- Research shows models perform significantly worse on paraphrased versions, questioning whether high scores reflect genuine reasoning ability

## Problem Examples

### Example 1 (Simple)

```
Sentence: The trophy didn't fit into the brown suitcase because **it** was too large.
Question: What does "it" refer to?
Options: A) the trophy   B) the suitcase
Answer: A
Reasoning: If something is too large to fit, then the large one is the trophy.
```

### Example 2 (Requires Social Commonsense)

```
Sentence: Susan gave Lisa a gift because **she** was grateful.
Question: Who does "she" refer to?
Options: A) Susan   B) Lisa
Answer: A
Reasoning: The person expressing gratitude is the gift giver (Susan), not the recipient.
```

### Example 3 (Requires Physical Commonsense)

```
Sentence: The heavy ball broke the table because **it** was fragile.
Question: What does "it" refer to?
Options: A) the ball   B) the table
Answer: B
Reasoning: The object that was broken is the fragile one, which is the table.
```

## Variants and Related Benchmarks

| Variant | Description |
|------|------|
| **WSC (Winograd Schema Challenge)** | Original 285 problems, proposed by Winograd (1972) and Levesque et al. (2012) |
| **WinoGender** | Coreference resolution subset focused on gender bias |
| **WinoWhat** | Paraphrased version of WinoGrande, used to test robustness |
| **DPR (Deterministic Predictive Reading)** | Related reading comprehension evaluation |
| **SuperGLUE-WSC** | General language understanding evaluation suite including WSC |

### Relationship with WSC

- WinoGrande is a direct extension of WSC, but approximately 150 times larger
- WinoGrande addresses the statistical shortcut issues present in WSC through adversarial debiasing
- Models achieving ~90% on WSC may score significantly lower on WinoGrande
- WinoGrande can serve as a transfer learning resource for WSC

## Limitations and Controversies

1. **Approaching Saturation**: Frontier model scores have reached ~88-92%, with limited discriminability
2. **Paraphrase Fragility**: Research shows models perform significantly worse on WinoWhat (paraphrased version), suggesting high scores may depend on dataset-specific patterns rather than genuine reasoning
3. **Evaluation Method Sensitivity**: Different evaluation methods (5-shot vs open-ended) produce widely varying scores
4. **Cultural Bias**: Problems reflect commonsense from English-speaking cultural backgrounds and may lack cross-cultural universality
5. **Binary Choice Format**: Only two options, random baseline of 50%, reduced resistance to random guessing
6. **Data Contamination Risk**: As a public dataset, there is a possibility of training data leakage
7. **No Longer Reported by Frontier Models**: Major model vendors have shifted to more difficult benchmarks (GPQA, HLE, etc.)

## Data Sources/References

- Sakaguchi et al., "WinoGrande: An Adversarial Winograd Schema Challenge at Scale," AAAI 2021. https://arxiv.org/abs/1907.10641
- Allen AI official leaderboard: https://leaderboard.allenai.org/winogrande/submissions/public
- WinoGrande official website: https://winogrande.allenai.org/
- BAUS.AI leaderboard: https://baus.ai/benchmarks/winogrande
- Gevers et al., "WinoWhat: Rethinking Winograd Schema Evaluation," CoNLL 2025