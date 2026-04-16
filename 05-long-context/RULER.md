# RULER — Long Text Retrieval and Reasoning

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | Retrieval Under Long-Extensive Requirements |
| Creator | NVIDIA (Ni et al.) |
| Release Year | 2024 |
| Number of Questions | Synthetically generated, configurable and scalable |
| Question Type | Information retrieval, multi-hop tracing, aggregation, and QA in long texts |
| Dataset Link | https://huggingface.co/datasets/tonychenxyz/ruler-full |
| Paper Link | https://arxiv.org/abs/2404.06654 |
| GitHub | https://github.com/NVIDIA/RULER |
| Status | Active, RULER v1 + v2 both available |

Note: Values marked with ~ are approximations from unofficial sources or estimates.

## Overview

RULER is a synthetic long-context evaluation benchmark released by NVIDIA, designed to reveal the gap between models' **claimed context length and their actual effective length**. It goes beyond simple Needle-in-a-Haystack (NIAH) tests by comprehensively evaluating models across 4 major categories and 13 tasks at different context lengths. Experiments found that nearly all models score near-perfect on simple NIAH but degrade sharply on RULER's more complex tasks as context grows.

## Dataset Composition

### 4 Major Task Categories and 13 Subtasks

#### 1. Retrieval — 8 subtasks

Extended NIAH testing evaluating retrieval capability under different needle types and quantities:

| Subtask | Description |
|--------|------|
| S-NIAH Subtask-1 (Passkey) | Retrieve a number from repeated noise sentences |
| S-NIAH Subtask-2 (Vanilla) | Retrieve a number from Paul Graham essays |
| S-NIAH Subtask-3 (UUID) | Retrieve a 32-character UUID from essays |
| MK-NIAH Subtask-1 (Multi-Key) | Identify the target from 4 needles, 3 are distractors |
| MK-NIAH Subtask-2 (Line) | Full text filled with distractor needles, line-level retrieval |
| MK-NIAH Subtask-3 (KV) | UUID-UUID key-value pair retrieval with all distractors |
| MV-NIAH (Multi-Value) | Same key with multiple values, must retrieve all 4 values |
| MQ-NIAH (Multi-Query) | Multiple queries, must return all 4 key-value pairs |

#### 2. Multi-hop Tracing — 1 subtask

| Subtask | Description |
|--------|------|
| VT (Variable Tracking) | Track variable binding chains (X2=X1, X3=X2...) and return all variable names pointing to the same value |

#### 3. Aggregation — 2 subtasks

| Subtask | Description |
|--------|------|
| CWE (Common Words Extraction) | Find the 10 most frequent words from text sampled from uniform distribution |
| FWE (Frequent Words Extraction) | Find the 3 most frequent words from text following a Zeta distribution (similar to Zipf's law) |

#### 4. Question Answering — 2 subtasks

| Subtask | Description |
|--------|------|
| QA-SQuAD | Single-hop QA: gold paragraph embedded in distractor paragraphs |
| QA-HotpotQA | Multi-hop QA: requires cross-document reasoning |

### Context Length Configuration

Incremental testing from **4K to 128K tokens** (4K, 8K, 16K, 32K, 64K, 128K), with flexible configuration support.

## Evaluation Method

1. **Scoring metric**: Weighted average accuracy across subtasks (wAvg)
2. **Effective length threshold**: Uses Llama-2-7B performance at 4K length (85.6%) as the baseline for "effective context"; performance below this is considered failure
3. **Evaluation pipeline**: Synthetically generate test data → model inference → automatic scoring
4. **Open-source tools**: Both RULER v1 and v2 evaluation pipelines are open-source on GitHub

## Model Performance (April 2026)

| Model | Claimed Length | Effective Length | 4K | 8K | 16K | 32K | 64K | 128K | Weighted Average |
|------|---------|---------|-----|-----|------|------|------|------|---------|
| Jamba-1.5-Large | 256K | >128K | 96.7 | 96.6 | 96.4 | 96.0 | 95.4 | 95.1 | 95.7 |
| Gemini-1.5-Pro | 1M | >128K | 96.7 | 95.8 | 96.0 | 95.9 | 95.9 | 94.4 | 95.5 |
| Qwen3-235B | 128K | >128K | 97.7 | 97.2 | 96.4 | 95.1 | 93.3 | 90.6 | ~95.0 |
| Qwen2.5-14B-1M | 1M | >128K | 97.5 | 97.1 | 94.6 | 94.9 | 94.9 | 92.2 | ~95.7 |
| GPT-4-1106 | 128K | 64K | 96.6 | 96.3 | 95.2 | 93.2 | 87.0 | 81.2 | 89.0 |
| Llama3.1-70B | 128K | 64K | 96.5 | 95.8 | 95.4 | 94.8 | 88.4 | 66.6 | 85.5 |

Data source: [NVIDIA/RULER GitHub](https://github.com/NVIDIA/RULER), [arXiv:2404.06654](https://arxiv.org/abs/2404.06654)

### Key Findings

- **Significant gap between claimed and actual performance**: e.g., GPT-4 claims 128K context but has an effective length of only 64K; Llama3.1-70B similarly claims 128K but degrades sharply after 64K
- **High NIAH scores don't indicate real capability**: Nearly all models score near-perfect on simple NIAH but degrade significantly on complex tasks like multi-hop tracing and aggregation
- **Only 2 models maintain >94% throughout**: Jamba-1.5-Large and Gemini-1.5-Pro sustain >94% within 128K
- **Non-Transformer architectures lag behind**: RWKV, Mamba, and other architectures are significantly weaker than Transformers

## Example Questions

### S-NIAH (Vanilla NIAH)

```
[Extensive Paul Graham essays as "haystack"]

The magic number is: 47291

[More essay content]

Question: What is the magic number?
Answer: 47291
```

### VT (Variable Tracking)

```
X1 = 42
X2 = X1
X3 = X2
... (numerous distractor variable bindings)
X50 = X49
Question: What is the value of X50?
Answer: 42
```

### CWE (Common Words Extraction)

```
[Text composed of common and uncommon words, common words appear ~30 times, uncommon words appear ~3 times]
Question: What are the 10 most common words in the text?
```

## Variants and Related Benchmarks

- **RULER v2**: Updated evaluation pipeline with improved scoring and configuration
- **Needle-in-a-Haystack (NIAH)**: RULER includes multiple variants of NIAH, making it a superset of NIAH
- **MRCR v2**: Google DeepMind's coreference resolution benchmark, focused on reasoning rather than retrieval
- **AA-LCR**: Artificial Analysis' long context reasoning benchmark using real documents
- **LongBench v2**: Chinese long-context benchmark
- **InfiniteBench**: A framework supporting infinite-length context evaluation

## Limitations and Controversies

1. **Synthetic data limitations**: All tasks are synthetically generated, creating a gap with real long-document processing scenarios
2. **128K upper limit**: The original evaluation only goes up to 128K, making it unable to assess 1M+ context capabilities (requires custom configuration)
3. **Lagging data for newer models**: Many models released in 2025–2026 (GPT-5, Claude Opus 4.6, etc.) lack official RULER evaluation data
4. **English only**: Does not support multilingual long-context evaluation, including Chinese
5. **Relatively simple aggregation tasks**: CWE/FWE tasks are relatively simple with limited discriminative power
6. **Difficult to unify evaluation conditions across architectures**: Non-Transformer models have different tokenization and context processing methods, making comparability questionable

## Data Sources/References

- Ni et al., "RULER: What's the Real Context Size of Your Long-Context Language Models?", arXiv:2404.06654, 2024
- NVIDIA RULER GitHub: https://github.com/NVIDIA/RULER
- HuggingFace dataset: https://huggingface.co/datasets/tonychenxyz/ruler-full