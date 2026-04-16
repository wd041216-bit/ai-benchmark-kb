# SIQA — Social Interaction Question Answering

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Social Interaction QA (Social IQa) |
| Creator | Maarten Sap, Ronan Le Bras, Emily Dinan et al. (AI2/University of Washington) |
| Release Year | 2019 |
| Number of Problems | ~35,000 (training) + ~2,000 (validation) + ~6,000 (test) |
| Problem Type | Three-choice questions |
| Dataset Link | https://huggingface.co/datasets/social_i_qa |
| Paper Link | https://arxiv.org/abs/1904.09728 |
| GitHub | https://github.com/allenai/socialiqa |
| Status | ⚠️ Moderate discriminability (frontier models ~78-85%, humans ~84-87%) |

## Overview

Social IQa (SIQA) is the first large-scale **social commonsense reasoning** evaluation benchmark, testing models' understanding of human social interaction situations. Problems cover emotional reactions, motivations for social behavior, and consequences of interpersonal interactions, evaluating whether models possess "social intelligence" — the ability to understand how people think, feel, and act in social situations.

SIQA is built on the ATOMIC commonsense knowledge graph, converting structured knowledge into natural language questions through crowdsourcing, ensuring diversity and coverage of problems.

### Core Evaluation Dimensions

1. **Emotional Reasoning**: Inferring people's emotional reactions in social situations
2. **Motivational Reasoning**: Understanding why people engage in social behaviors
3. **Consequence Reasoning**: Predicting possible outcomes of social behaviors
4. **Social Norms**: Understanding the appropriateness and norms of social behavior

## Dataset Composition

SIQA is organized around three types of social cognition questions:

| Question Type | Description | Proportion |
|---------|------|---------|
| Emotional Reaction | How would someone feel in this situation? | ~33% |
| Behavioral Motivation | Why did someone do this? | ~33% |
| Behavioral Consequence | What happens after someone does this? | ~33% |

### Problem Sources

1. **ATOMIC Knowledge Graph**: Starting from social interaction events in the commonsense knowledge graph
2. **Crowdsourced Rewriting**: Converting structured knowledge into natural language Q&A
3. **Quality Control**: Multiple rounds of human review to ensure problem quality

### Dataset Size

| Subset | Number of Problems | Purpose |
|------|---------|------|
| Training set | ~35,000 | Model training |
| Validation set | ~2,000 | Development and debugging |
| Test set | ~6,000 | Final evaluation (labels not public) |
| Validation set (with labels) | ~2,000 | Standard evaluation subset |

## Evaluation Method

- **Primary metric**: Accuracy
- **Evaluation subset**: Validation set (with labels, ~2,000 problems) is the commonly used evaluation set
- **Scoring method**: Percentage of correct answers out of total problems
- **Standard evaluation**: Both 0-shot and few-shot are used
- **Human baseline**: Approximately 84-87% (original paper reports ~87% on validation set, ~84% on test set)
- **Random baseline**: 33.3% (three choices)

### Evaluation Considerations

SIQA evaluation has methodological challenges:
- Different evaluation methods (0-shot vs few-shot, direct generation vs multiple-choice format) produce significant differences
- Research has shown that the same model can have score differences of over 15 percentage points under different evaluation methods
- The test set with non-public labels requires submission to an official server for scoring

## Model Performance (April 2026)

### Frontier Models

| Model | SIQA Accuracy | Notes |
|------|-----------|------|
| GPT-5 | ~89% | Unofficial estimate |
| Claude Opus 4.6 | ~88% | Unofficial estimate |
| Gemini 2.5 Pro | ~89% | Unofficial estimate |
| Llama 4 | ~87% | Unofficial estimate |
| Phi-3.5-MoE-instruct | ~78.0% | airank.dev leaderboard |
| Phi-3.5-mini-instruct | ~74.7% | airank.dev leaderboard |
| Gemma 2 27B | ~53.7% | airank.dev leaderboard |
| Humans | ~84-87% | Original paper |

Note: Values with ~ are approximate, from unofficial sources or estimates. SIQA is no longer included in standard evaluations by most frontier model technical reports.

Data sources: airank.dev leaderboard, AIPRL-LIR community reports, original paper

### Early Models (Comparison)

| Model | SIQA Accuracy | Notes |
|------|-----------|------|
| BERT-large | ~64.5% | Original paper baseline |
| RoBERTa-large | ~68% | After fine-tuning |
| GPT-2 | ~57% | Original paper baseline |
| Random Baseline | 33.3% | Three choices |

## Problem Examples

### Example 1 (Emotional Reaction)

```
Context: Tracy didn't go home that evening and resisted Riley's attacks.
Question: What will Tracy want to do next?
Options: A) go home   B) fight back   C) hide
Answer: A
Reasoning: After resisting an attack, Tracy's most reasonable desire would be to return to the safety of home.
```

### Example 2 (Behavioral Motivation)

```
Context: Robin gave a gift to Sandy for their birthday.
Question: Why did Robin do this?
Options: A) to make Sandy happy   B) to borrow money   C) to show off
Answer: A
Reasoning: The motivation for giving a birthday gift is usually to make the recipient happy.
```

### Example 3 (Behavioral Consequence)

```
Context: Jordan helped Casey study for the exam.
Question: What will happen to Casey?
Options: A) Casey will fail the exam   B) Casey will pass the exam   C) Casey will drop out
Answer: B
Reasoning: After receiving study help, Casey is more likely to pass the exam.
```

### Example 4 (Social Norms)

```
Context: Alex brought cookies to the office for everyone.
Question: How will Alex's coworkers feel?
Options: A) annoyed   B) grateful   C) jealous
Answer: B
Reasoning: Coworkers would feel grateful for receiving free cookies.
```

## Variants and Related Benchmarks

| Variant | Description |
|------|------|
| **SIQA Competition** | New competition version launched in 2025, featuring SIQA-S (structured) and SIQA-U (unstructured) tracks |
| **ATOMIC** | The underlying knowledge graph for SIQA, containing commonsense knowledge about social interactions |
| **ATOMIC-2020** | Extended knowledge graph covering more social concepts |
| **CommonsenseQA** | General commonsense reasoning evaluation (five-choice format) |
| **WinoGrande** | Coreference resolution commonsense reasoning (binary choice format) |
| **PIQA** | Physical commonsense reasoning (binary choice format) |
| **Ethical QA** | Ethical judgment evaluation |

### Differences from CommonsenseQA

- SIQA focuses on social interaction situations, CommonsenseQA covers broader general commonsense
- SIQA uses a three-choice format, CommonsenseQA uses a five-choice format
- SIQA is based on the ATOMIC knowledge graph, CommonsenseQA is based on ConceptNet

### Differences from WinoGrande/PIQA

- WinoGrande tests coreference resolution reasoning, PIQA tests physical intuition, SIQA tests social reasoning
- The three are complementary, forming an important triangle of commonsense reasoning evaluation

## Limitations and Controversies

1. **Evaluation Method Sensitivity**: Different evaluation methods lead to 15+ percentage point score differences, reducing comparability
2. **Non-public Labels**: Test set labels are not public, requiring submission to an official server, reducing ease of use
3. **Cultural Bias**: Problems reflect Western social norms and lack global universality
4. **Approaching Saturation**: Frontier models are approaching or exceeding human-level performance, with declining discriminability
5. **Three-Choice Format**: Random baseline of 33.3% provides limited resistance to random guessing
6. **Data Contamination**: As a public dataset, there is a risk of training data leakage
7. **No Longer Reported by Mainstream**: Most frontier model technical reports no longer include SIQA
8. **Annotation Controversy**: Some problems have culturally dependent correct answers, and different cultural backgrounds may lead to different judgments
9. **SIQA Competition Format Changes**: The 2025 new competition version introduced scoring dimension changes that are not fully comparable with the original version

## Data Sources/References

- Sap et al., "Social IQa: Commonsense Reasoning about Social Interactions," EMNLP 2019. https://arxiv.org/abs/1904.09728
- SIQA official website: https://allenai.org/data/socialiqa
- HuggingFace dataset: https://huggingface.co/datasets/social_i_qa
- airank.dev leaderboard: https://airank.dev/benchmarks/social-iqa
- SIQA Competition: https://siqa-competition.github.io/Leaderboard/