# MRCR v2 — Multi-Round Coreference Resolution

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | Multi-Round Coreference Resolution v2 |
| Creator | Google DeepMind (Vodrahalli et al.) |
| Release Year | 2024 |
| Number of Questions | Synthetically generated, scalable on demand |
| Question Type | Coreference resolution and content reproduction in long texts |
| Dataset Link | https://github.com/google-deepmind/eval_hub/tree/master/eval_hub/mrcr_v2 |
| Paper Link | https://arxiv.org/abs/2409.12640 |
| GitHub | https://github.com/google-deepmind/eval_hub |
| Status | Active, widely used in long-context evaluation |

Note: Values marked with ~ are approximations from unofficial sources or estimates.

## Overview

MRCR v2 is a long-context reasoning benchmark released by Google DeepMind under the Michelangelo benchmark framework. Unlike simple Needle-in-a-Haystack (NIAH) tests, MRCR requires models to **track referential relationships and precisely reproduce specific content** in lengthy multi-turn conversations, rather than simply retrieving a single hidden piece of information.

The model receives a long conversation consisting of alternating user and assistant turns, where the user repeatedly requests text generation in specific formats/styles/topics. After the conversation ends, the model must reproduce the correct assistant response based on a description (e.g., "the 2nd poem about penguins") and prefix it with a unique random string to prove it actually followed the instructions.

## Dataset Composition

MRCR v2 provides three difficulty variants, distinguished by the number of "needles":

| Variant | Number of Needles | Random Baseline (random selection from relevant responses only) |
|------|--------|----------------------------------|
| 2-needle | 2 | ~51% |
| 4-needle | 4 | ~27% |
| 8-needle | 8 | ~15% |

Each "needle" is identified by a triple **(format, topic, style)**, with multiple requests sharing overlapping topics or formats, creating adversarial similarity that makes it difficult for models to distinguish based on keywords alone.

### Context Length Stratification

| Subset | Context Range | Evaluation Method |
|------|-----------|---------|
| upto_32K | 0–32K tokens | Cumulative average |
| upto_128K | 0–128K tokens | Cumulative average |
| at_1M | 1M tokens | Point value |

The dataset supports context lengths up to **8M** tokens.

## Evaluation Method

1. **Scoring metric**: Uses Python `difflib.SequenceMatcher` to compute string similarity ratio (0–1), normalized to percentage
2. **Input format**: Few-shot setting (2 short-context examples) + complete long-context conversation + final query
3. **Output requirement**: The model must first output the specified unique random string, then output the correct text
4. **Important constraint**: If the model is given access to code tools, the task difficulty drops significantly. Any MRCR report must clearly state whether tools were provided

## Model Performance (April 2026)

### 8-needle variant

| Model | 128K (Cumulative Average) | 1M (Point Value) |
|------|----------------|----------|
| Claude Opus 4.6 | ~70% | 76% |
| Gemini 3 Pro | ~77% | ~26% |
| GPT-5.2 High | ~65% | — |
| Gemini 2.5 Pro | 58.0% | 16.4% |
| Claude Sonnet 4.5 | ~39% | 18.5% |

### 4-needle variant (256K tokens)

| Model | 4-needle 256K |
|------|-------------|
| GPT-5.2 | 98% |
| Claude Opus 4.6 | ~90% |
| Gemini 3 Pro | ~85% |
| Claude Sonnet 4.6 | ~82% |
| GPT-4.1 | ~80% |

Data source: [llm-stats.com](https://llm-stats.com/benchmarks/mrcr-v2), [LLM Registry](https://llm-registry.com/benchmark/mrcr-v2), [Google DeepMind eval_hub](https://github.com/google-deepmind/eval_hub/tree/master/eval_hub/mrcr_v2)

## Example Questions

### Input Excerpt

```
User: Please write a poem about penguins in a classical style.
Assistant: [1st classical poem about penguins — ~500 words]

User: Please write an essay about penguins in a modern style.
Assistant: [1st modern essay about penguins]

... (extensive intermediate dialogue covering penguins, seals, polar bears, and other topics)

User: Please write a poem about penguins in a classical style.
Assistant: [2nd classical poem about penguins — ~500 words]
```

### Final Query

```
Please reproduce the 2nd classical poem about penguins. Prefix your answer with the string "X7KQ2M".
```

### Expected Output

```
X7KQ2M [Complete text of the 2nd classical poem about penguins]
```

## Variants and Related Benchmarks

- **Michelangelo suite**: MRCR is part of the Michelangelo benchmark, which also includes other LSQ framework evaluations such as LAT (Latent Association Test)
- **MRCR v1**: The original 2-needle version, with lower difficulty
- **Context Arena**: An online interactive evaluation platform [contextarena.ai](https://contextarena.ai) for real-time comparison of model long-context performance
- **RULER**: NVIDIA's long-context retrieval benchmark, complementary to MRCR (RULER focuses on retrieval, MRCR focuses on reasoning and coreference resolution)

## Limitations and Controversies

1. **Only tests coreference resolution**: MRCR does not cover all capability dimensions of long-context processing (such as aggregation reasoning, multi-hop QA); it should be used alongside other benchmarks
2. **Synthetic data bias**: Conversation content is synthetically generated, which differs from real user interaction scenarios
3. **Tool access significantly affects results**: Allowing code tools drastically reduces difficulty; evaluation conditions must be strictly unified
4. **Inconsistent evaluation conditions across models**: Scores from different sources may use different thinking configurations or tool settings, so direct comparisons require caution
5. **Scarce 1M+ evaluation data**: Most models only have reliable evaluation data at 128K and below

## Data Sources/References

- Vodrahalli et al., "Michelangelo: Long Context Evaluations Beyond Haystacks via Latent Structure Queries," arXiv:2409.12640, 2024
- Google DeepMind eval_hub: https://github.com/google-deepmind/eval_hub