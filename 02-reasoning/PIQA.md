# PIQA — Physical Interaction Question Answering

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Physical Interaction: Question Answering (PIQA) |
| Creator | Yonatan Bisk, Rowan Zellers et al. (UW/Allen AI) |
| Release Year | 2020 |
| Number of Problems | ~16,000 (training 16K, validation 2K, test 3K) |
| Problem Type | Binary choice questions |
| Dataset Link | https://huggingface.co/datasets/piqa |
| Paper Link | https://arxiv.org/abs/1911.11641 |
| GitHub | https://github.com/ybisk worldmodels/tree/master/piqa |
| Status | ⚠️ Frontier models approaching saturation (~90-95%), humans ~95% |

## Overview

PIQA focuses on **physical commonsense reasoning** — evaluating models' understanding of everyday physical world interactions. Problems involve physical properties of objects, their usage, and interaction outcomes, testing whether models possess "intuitive physics" knowledge.

Unlike knowledge-retrieval benchmarks like MMLU, PIQA does not test factual knowledge, but rather commonsense judgments about how the physical world works. For example: which end of a hammer should you use to drive a nail? What happens to an ice cube in hot water? These judgments, which are effortless for humans, pose unique challenges for language models.

### Core Evaluation Dimensions

1. **Physical Commonsense**: Understanding physical properties of objects and how they interact
2. **Causal Reasoning**: Inferring consequences of physical actions
3. **Tool Usage**: Judging correct ways to use tools
4. **Everyday Experience**: Relying on human experience in the physical world

## Dataset Composition

PIQA problems were sourced from ATIS (Amazon Mechanical Turk) crowdsourcing, with strict quality control:

| Subset | Number of Problems | Purpose |
|------|---------|------|
| Training set | 16,114 | Model training |
| Validation set | 1,838 | Development and debugging |
| Test set | 3,084 | Final evaluation |
| Additional test set | 1,838 | Adversarial testing |

### Problem Format

Each PIQA problem contains:
- **Goal**: A sentence describing a physical goal
- **Option 1 (sol1)**: One possible way to achieve it
- **Option 2 (sol2)**: Another possible way to achieve it
- **Label**: Correct answer (0 or 1)

### Problem Categories

PIQA problems cover multiple physical interaction scenarios:

| Category | Example |
|------|------|
| Object Properties | Judging whether objects are soft or hard, hot or cold |
| Tool Usage | Choosing the correct way to use a tool |
| Causal Reasoning | Predicting outcomes of physical actions |
| Alternative Approaches | Choosing more reasonable methods in specific situations |
| Safety Judgment | Judging which approach is safer |

## Evaluation Method

- **Primary metric**: Accuracy
- **Evaluation subset**: Test set (3,084 problems) is the standard evaluation set
- **Scoring method**: Percentage of correct answers out of total problems
- **Standard evaluation**: Both 0-shot and 5-shot are used
- **Human baseline**: Approximately 95.1% (original paper and subsequent evaluations)

### Global PIQA Extension (2025)

Global PIQA, released in 2025, extended the evaluation to 116 languages and 65 countries, involving 335 researchers:
- Found an accuracy gap of up to 37% between high and low resource languages
- Western European languages averaged ~95%, Sub-Saharan African languages averaged ~80%
- 59.9% of problems have cultural specificity

## Model Performance (April 2026)

### Frontier Models

| Model | PIQA Accuracy | Notes |
|------|-----------|------|
| GPT-5 | ~94% | Unofficial estimate, from community reports |
| Claude Opus 4.6 | ~93% | Unofficial estimate |
| Gemini 3 Pro | ~93% | Unofficial estimate |
| Gemini 2.5 Pro | ~91.7% | Global PIQA (116 language average) |
| GPT-4o | ~85-88% | Multi-source estimates |
| DeepSeek-V3 | ~84.7% | LLMdb leaderboard |
| Gemma 3 27B | ~82.4% | Global PIQA (best open-source) |
| Humans | ~95% | Original paper |

Note: Values with ~ are approximate, from unofficial sources or estimates. PIQA is approaching saturation, and most frontier models no longer report this benchmark score in their technical reports.

Data sources: LLMdb leaderboard, Global PIQA paper (arXiv:2510.24081), community reports

### Early Models (Comparison)

| Model | PIQA Accuracy |
|------|-----------|
| RoBERTa-large | ~79% |
| BERT-large | ~77% |
| GPT-2 | ~70% |
| Random Baseline | 50% |

## Problem Examples

### Example 1 (Tool Usage)

```
Goal: To separate egg whites from yolks you can use
Option 1: a plastic bottle to suck up the yolk
Option 2: a plastic bag to push out the yolk
Answer: Option 1
Reasoning: Using a plastic bottle to suck up the yolk is a common and effective separation method.
```

### Example 2 (Physical Causality)

```
Goal: To make a room darker during the day you can
Option 1: close the blinds
Option 2: open the blinds
Answer: Option 1
Reasoning: Closing the blinds blocks light, making the room darker.
```

### Example 3 (Object Properties)

```
Goal: To keep from getting cold while sleeping you can
Option 1: wrap yourself in a thin sheet
Option 2: wrap yourself in a thick blanket
Answer: Option 2
Reasoning: A thick blanket provides better insulation and warmth.
```

### Example 4 (Alternative Approaches)

```
Goal: To make a fire without matches you can
Option 1: rub two sticks together
Option 2: rub two ice cubes together
Answer: Option 1
Reasoning: Rubbing wooden sticks generates heat that can start a fire, but ice cubes cannot.
```

## Variants and Related Benchmarks

| Variant | Description |
|------|------|
| **Global PIQA** | Extended version covering 116 languages and cultures (2025) |
| **PIQA-Adversarial** | Adversarial subset, filtered for statistical shortcut problems |
| **HellaSwag** | Also a commonsense reasoning benchmark, but focused on sentence continuation |
| **WinoGrande** | Coreference resolution commonsense reasoning |
| **SIQA** | Social interaction commonsense reasoning |
| **CommonsenseQA** | General commonsense reasoning Q&A |

### Differences from HellaSwag

- PIQA focuses on intuitive knowledge about the physical world, HellaSwag focuses on event continuation
- PIQA uses a binary choice format, HellaSwag uses a four-choice format
- PIQA emphasizes causal reasoning more, HellaSwag emphasizes script knowledge more

## Limitations and Controversies

1. **Approaching Saturation**: Frontier models have reached ~90-95%, with extremely low discriminability
2. **Binary Choice Format**: Random baseline is 50%, weak resistance to guessing
3. **Cultural Bias**: Problems are based on Western physical life experiences and lack global universality (Global PIQA quantified this issue)
4. **Data Contamination**: As a public dataset, there is a risk of training data leakage
5. **Evaluation Method Differences**: Different evaluation methods (0-shot vs 5-shot) produce different scores
6. **No Longer Reported by Mainstream**: Most frontier model technical reports no longer include PIQA
7. **Limited Concept Coverage**: Only tests physical commonsense, not other reasoning types such as social or logical
8. **Quality Annotation Issues**: Some problems have disputed correct answers

## Data Sources/References

- Bisk et al., "PIQA: Reasoning about Physical Commonsense in Natural Language," AAAI 2020. https://arxiv.org/abs/1911.11641
- Global PIQA: https://arxiv.org/abs/2510.24081
- PIQA official website: https://yonatanbisk.com/piqa/
- HuggingFace dataset: https://huggingface.co/datasets/piqa
- LLMdb leaderboard: https://llmdb.com/benchmarks/piqa