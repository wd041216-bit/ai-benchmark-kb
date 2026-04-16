# HellaSwag — Commonsense Reasoning Evaluation

## Basic Information

| Property | Value |
|----------|-------|
| Full Name | HellaSwag: Can a Machine Really Finish Your Sentence? |
| Creator | University of Washington (Rowan Zellers et al.) |
| Release Year | 2019 (ACL 2019) |
| Number of Questions | 10,042 (test set); ~70,000 (full including train/validation) |
| Question Type | Four-option sentence completion |
| Dataset Link | https://huggingface.co/datasets/Rowan/hellaswag |
| Paper Link | https://arxiv.org/abs/1905.07830 |
| GitHub | https://rowanzellers.com/hellaswag |
| Status | Saturated (top models > 95%, exceeding human baseline) |

## Overview

HellaSwag is a commonsense natural language inference benchmark that requires models to choose the most reasonable continuation from four options given a context describing everyday activities. Its core innovation is the **Adversarial Filtering** method: using language models to generate distractors, then iteratively training discriminators to identify and replace questions that are easily solved by pattern matching, thereby constructing an evaluation set that is robust against statistical shortcuts.

The name HellaSwag comes from "Harder Endings, Longer contexts, and Low-shot Activities for Situations With Adversarial Generations." Although adversarial filtering made it far more difficult than its predecessor SWAG at release, with the advancement of large language models, HellaSwag has become largely saturated, with frontier models exceeding the human baseline.

## Dataset Composition

### Data Sources

| Source | Description |
|--------|-------------|
| ActivityNet | Video description captions, covering everyday activity scenarios |
| WikiHow | How-to articles, covering various life skills |

### Dataset Splits

| Split | Count |
|-------|-------|
| Training set | ~40,000 |
| Validation set | ~10,000 |
| Test set | 10,042 |

### Evaluation Dimensions

Testing commonsense reasoning and physical world understanding:
- **Event continuation**: Given a description, choose the most reasonable continuation
- **Physical commonsense**: Understanding how objects move and interact
- **Social commonsense**: Understanding behavior in social situations

## Evaluation Method

### Adversarial Filtering Method

The core construction method of HellaSwag, with the following iterative process:

1. **Candidate generation**: Use language models (GPT series) to generate distractor candidates for each context
2. **Discriminator training**: Train a BERT-Large discriminator to distinguish correct endings from distractors
3. **Distractor replacement**: Replace weak distractors that the discriminator can easily identify with more difficult adversarial distractors
4. **Iterative refinement**: Repeat steps 2-3 until discriminator accuracy converges
5. **Human verification**: Crowdsourced workers remove adversarial endings that sound too plausible (false negatives), ensuring high human agreement

**"Goldilocks zone"**: Two-sentence generated endings are long enough to contain detectable errors yet short enough that the discriminator cannot reliably distinguish true from false.

**Important limitation**: Adversarial filtering only guarantees that the discriminator model used during construction cannot solve questions through known patterns, but does not guarantee protection against unknown shortcuts. More powerful models may discover entirely new reasoning strategies or data artifacts.

### Scoring Method

- **Primary metric**: Accuracy
- **Scoring method**: Percentage of correct answers out of total test set questions
- **Random baseline**: 25% (four options)
- **Human baseline**: ~95.6%
- **Comparison with SWAG**: The same model achieves ~80% on SWAG but only ~35% on HellaSwag (at release), quantifying the effect of adversarial filtering

## Model Performance (April 2026)

| Model | HellaSwag | Notes |
|-------|-----------|-------|
| GPT-5 | ~98% | Exceeds human baseline |
| Claude Opus 4.6 | ~97% | Exceeds human baseline |
| Gemini 3 Pro | ~97% | Exceeds human baseline |
| GPT-4 (2023) | ~94.2% | Approaching human baseline |
| GPT-3 (few-shot, 2020) | 78.9% | — |
| BERT-Large (2019) | 47.3% | SOTA at release |
| Human | ~95.6% | Baseline |

Note: Values with ~ are approximations from unofficial sources or estimates.

Data sources: Company technical reports, HellaSwag leaderboard

## Example Questions

### ActivityNet Source
```
A woman is seen walking into a room with a broom. She...
A) starts sweeping the floor with the broom (correct)
B) drives a car down the highway (incorrect)
C) cooks a meal in the kitchen (incorrect)
D) swims in the ocean (incorrect)
```

### WikiHow Source
```
How to make a paper airplane. First, take a rectangular piece of paper and...
A) fold it in half lengthwise (correct)
B) crumple it into a ball and throw it (incorrect)
C) cut it into small pieces with scissors (incorrect)
D) soak it in water until it dissolves (incorrect)
```

### Adversarial Distractor Example
```
A man is seen standing in a field with a soccer ball. He...
A) kicks the ball into the goal (correct)
B) picks up the ball and walks away (simple distractor, easy to identify)
C) begins dribbling and then kicks the ball into the net (adversarial distractor, harder to distinguish)
D) throws the ball into a nearby lake (simple distractor, easy to identify)
```

## Variants and Related Benchmarks

### Commonsense Reasoning Benchmark Family

| Benchmark | Description | Relationship |
|-----------|-------------|-------------|
| SWAG | HellaSwag predecessor, no adversarial filtering, deprecated | Predecessor |
| PIQA | Physical intuition Q&A, testing method selection for goal achievement | Related commonsense reasoning |
| ARC | Science reasoning challenge, testing multi-step scientific reasoning | Related commonsense reasoning |
| WinoGrande | Pronoun disambiguation, uses adversarial filtering | Related commonsense reasoning |
| CSQA (CommonsenseQA) | Multiple-choice commonsense Q&A | Related commonsense reasoning |

### Relationship with PIQA and ARC

HellaSwag, PIQA, and ARC form the core family of commonsense reasoning evaluation:

- **HellaSwag**: Focuses on **activity continuation**, understanding how events naturally proceed in everyday scenarios
- **PIQA**: Focuses on **physical intuition**, understanding object properties and behavioral constraints (given a goal, select the best implementation method)
- **ARC**: Focuses on **scientific reasoning**, requiring multi-step logical reasoning to solve scientific problems

Together they evaluate models' understanding of the physical world and social situations, but each has a different focus. HellaSwag's adversarial filtering methodology also influenced the construction of PIQA and WinoGrande.

## Limitations and Controversies

1. **Saturated**: Top models exceed the human baseline (95.6%), HellaSwag has lost the ability to distinguish frontier models
2. **Simple format**: Four-option choices give a 25% random baseline, and questions are relatively short
3. **Adversarial filtering is imperfect**: Only effective against the discriminator used during construction, does not guarantee no shortcuts for more powerful models
4. **English only**: Original version only covers English
5. **Recommended alternatives**: Use GPQA, HLE (Humanity's Last Exam), ARC-AGI-2 and other more difficult reasoning benchmarks
6. **Data contamination risk**: As a public dataset, may have been included in training corpora

## Data Sources / References

- Zellers, R., Holtzman, A., Bisk, Y., Farhadi, A., & Choi, Y. "HellaSwag: Can a Machine Really Finish Your Sentence?" ACL 2019. https://aclanthology.org/P19-1472/
- Paper PDF: https://arxiv.org/pdf/1905.07830
- HellaSwag project page: https://rowanzellers.com/hellaswag
- HuggingFace dataset: https://huggingface.co/datasets/Rowan/hellaswag
- Adversarial filtering methodology analysis: https://mbrenndoerfer.com/writing/hellaswag-adversarial-filtering-commonsense-benchmark