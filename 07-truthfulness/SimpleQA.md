# SimpleQA — Short-Answer Factual QA Evaluation

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | SimpleQA |
| Creator | OpenAI |
| Release Year | 2024 |
| Number of Questions | 1,000 |
| Question Type | Short-answer factual QA |
| Dataset Link | https://huggingface.co/datasets/openai/simpleqa |
| Paper Link | https://arxiv.org/abs/2411.00336 |
| Leaderboard | https://www.kaggle.com/benchmarks/openai/simpleqa |
| Status | Active standard for factuality evaluation |

## Overview

SimpleQA is a factual QA benchmark released by OpenAI in 2024, designed to concisely measure language models' ability to answer short factual questions. Each question has a clear, verifiable short answer, and the evaluation focuses on two dimensions: **answer accuracy** (whether the answer is correct) and **hallucination resistance** (whether the model can avoid fabricating uncertain answers).

Unlike TruthfulQA, which focuses on "common human misconceptions," SimpleQA focuses on the correctness of objective factual knowledge without adversarial design. Compared to the multi-dimensional evaluation of the FACTS Suite, SimpleQA has a narrower but more focused scope, specifically assessing factual accuracy within a model's parametric knowledge.

## Dataset Composition

- **Scale**: 1,000 short-answer factual questions
- **Answer format**: Each question has a clear, concise correct answer (e.g., a person's name, date, number, etc.)
- **Difficulty distribution**: Covers difficulty levels from common knowledge to specialized knowledge
- **Topic distribution**: Covers history, geography, science, culture, sports, and other domains
- **Annotation quality**: Human-annotated and cross-validated, but some annotation errors exist (see SimpleQA Verified variant)

## Evaluation Method

### Core Metrics

- **Correctness**: The proportion of model answers that match the ground-truth answer
- **Hallucination Rate**: The proportion of questions where the model gives a wrong answer instead of acknowledging uncertainty
- **Calibration**: The degree of match between the model's confidence in its answers and the actual correctness rate

### Scoring Process

1. The model generates a short answer for each question
2. An LLM judge compares the model's output with the ground-truth answer
3. Composite metrics of correctness and hallucination rate are calculated

### SimpleQA Verified Variant

Google DeepMind released **SimpleQA Verified** in 2025, addressing known issues in the original SimpleQA:

| Improvement | Description |
|--------|------|
| Annotation error correction | Fixed approximately 5% of annotation errors in the original dataset |
| Topic bias reduction | Reduced over-concentration in certain topics |
| Redundant question cleanup | Removed semantically duplicate questions |
| Leaderboard migration | Migrated to Kaggle leaderboard hosting |

## Model Performance (April 2026)

| Model | SimpleQA Verified Correctness |
|------|------------------------|
| Gemini 3 Pro | 72.1% |
| GPT-5 | ~65% [^1] |
| Claude Opus 4.6 | ~55% [^1] |
| GPT-4o (2024) | ~40% [^2] |
| Claude 3.5 Sonnet (2024) | ~30% [^2] |

[^1]: Approximate values, estimated from public technical reports and leaderboard data
[^2]: Approximate values, from the original SimpleQA paper and subsequent evaluations

## Example Questions

```
Question: What is the chemical symbol for the element with atomic number 14?
Correct Answer: Si
```

```
Question: Who was the Prime Minister of the United Kingdom in 1979?
Correct Answer: Margaret Thatcher
```

```
Question: What is the largest desert in the world by area?
Correct Answer: Antarctic Desert
(Note: Antarctica is the largest desert by area, not the Sahara — a common misconception)
```

## Variants and Related Benchmarks

| Variant/Benchmark | Relationship |
|----------------|------|
| **SimpleQA Verified** | Google DeepMind's corrected version, fixing annotation errors and reducing topic bias |
| **FACTS Suite** | Google DeepMind's more comprehensive factuality evaluation, includes Parametric sub-benchmark that overlaps with SimpleQA's functionality, but extends to search-augmented, document-grounded, and multimodal dimensions |
| **TruthfulQA** | Focuses on "common human misconceptions" rather than purely factual knowledge, complementary to SimpleQA |
| **TriviaQA** | Larger-scale QA dataset, but lacks SimpleQA's hallucination detection dimension |

## Limitations and Controversies

1. **Limited question scale**: Only 1,000 questions, limited statistical discriminative power
2. **Annotation quality concerns**: The original version has approximately 5% annotation errors, requiring the Verified variant for correction
3. **Topic bias**: The original version is not uniformly distributed across topics, leaning toward certain knowledge domains
4. **Only covers parametric knowledge**: Does not evaluate factuality in search-augmented scenarios, while the FACTS Suite Search sub-benchmark has shown that search significantly improves performance
5. **LLM judging bias**: Using an LLM as judge may introduce systematic bias
6. **Short-answer limitation**: Only evaluates short-answer facts, not longer text factual consistency

## Data Sources/References

- OpenAI SimpleQA paper: https://arxiv.org/abs/2411.00336
- Google DeepMind SimpleQA Verified correction notes
- FACTS Suite (2025): https://www.kaggle.com/benchmarks/google/facts
- Kaggle SimpleQA leaderboard: https://www.kaggle.com/benchmarks/openai/simpleqa
- Various model official technical reports (Gemini 3, GPT-5, Claude Opus 4.6)