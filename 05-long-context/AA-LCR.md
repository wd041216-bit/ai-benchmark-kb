# AA-LCR — Long Context Reasoning

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | Artificial Analysis Long Context Reasoning |
| Creator | Artificial Analysis |
| Release Year | 2025 |
| Number of Questions | 100 |
| Question Type | Multi-document multi-step reasoning QA |
| Dataset Link | https://huggingface.co/datasets/ArtificialAnalysis/AA-LCR |
| Paper Link | No formal paper yet |
| GitHub | None yet |
| Status | Active leaderboard with continuous updates |

Note: Values marked with ~ are approximations from unofficial sources or estimates.

## Overview

AA-LCR (Artificial Analysis Long Context Reasoning) is a long context reasoning benchmark released by Artificial Analysis in August 2025, designed to address the overestimation of models' true long-context capabilities by simple retrieval benchmarks (such as Needle-in-a-Haystack). Each question in AA-LCR requires models to perform **cross-document, multi-step reasoning** across a multi-document corpus of approximately 100K tokens (cl100k_base tokenizer) — answers cannot be directly found in the text; they must be inferred and synthesized from information scattered across different documents.

All questions have been human-verified: human evaluators achieved only 40–60% accuracy on first attempts, confirming the benchmark's difficulty.

## Dataset Composition

### Document Category Distribution

| Category | Number of Questions | Number of Document Sets |
|------|--------|---------|
| Company Reports | 63 | 16 |
| Industry Reports | 8 | 4 |
| Government Consultations | 11 | 3 |
| Academia | 5 | 2 |
| Legal | 6 | 2 |
| Marketing Materials | 6 | 2 |
| Survey Reports | 1 | 1 |

### Core Features

- **Multi-document reasoning**: Each question spans multiple documents and cannot be answered from a single document
- **Multi-step reasoning**: Answers require synthesizing information from multiple sources through inference, not simple retrieval
- **Real-world scenarios**: Simulates daily tasks of knowledge workers such as analysts, researchers, and lawyers
- **Input length**: Approximately 10K–100K tokens (measured by cl100k_base), covering different scales

## Evaluation Method

1. **Scoring metric**: Accuracy, as a percentage
2. **Answer format**: Each question has a clear ground-truth answer, verified by human evaluators
3. **Evaluation process**: The model receives the complete document set + question and generates an answer directly
4. **Human baseline**: Human evaluators achieve 40–60% accuracy on first attempts
5. **Independent evaluation**: Conducted independently by Artificial Analysis, results are reproducible

## Model Performance (April 2026)

| Model | AA-LCR Accuracy |
|------|-------------|
| GPT-5.2 Codex | 75.7% |
| GPT-5 | 75.6% |
| GPT-5.1 | 75.0% |
| Claude Opus 4.5 | 74.0% |
| Gemini 3.0 Pro Preview | ~71% |
| Claude Sonnet 4.6 | ~71% |
| MiniMax M2.5 | ~69.5% |
| Qwen3.5-397B-A17B | 68.7% |
| Gemini 2.5 Pro | 66% |
| Claude Sonnet 4.5 | 66% |
| Claude Sonnet 4 | ~65% |
| Kimi K2.5 | ~65% |
| GLM-5 | ~63% |
| o3 (first attempt, August 2025) | 69.3% |
| Human first attempt | 40–60% |

Data source: [Artificial Analysis AA-LCR Leaderboard](https://artificialanalysis.ai/evaluations/artificial-analysis-long-context-reasoning), [DataLearnerAI AA-LCR](https://www.datalearner.com/en/benchmarks/aa-lcr)

## Example Questions

### Typical Question Format

```
Based on the following company annual reports and industry analyses, answer the question:

[Document 1: Company 2024 annual report, ~15K tokens]
[Document 2: Same company 2023 annual report, ~12K tokens]
[Document 3: Industry competitive analysis report, ~8K tokens]
...

Question: What three main factors drove the company's revenue growth in 2024?
Compared to 2023, how has the share of overseas business changed? Is this change consistent with the overall industry trend?

The answer requires extracting and cross-referencing information from at least 3 different documents.
```

### Difficulty Characteristics

- Information is scattered across multiple documents; no single "answer paragraph" exists
- Requires numerical comparison, trend judgment, and cross-document synthesis
- Models cannot rely on retrieval alone — they must understand and reason

## Variants and Related Benchmarks

- **Needle-in-a-Haystack (NIAH)**: A simple retrieval benchmark; AA-LCR was motivated as a complement to NIAH — high NIAH scores do not indicate strong real long-context capabilities
- **MRCR v2**: Focuses on coreference resolution and content reproduction; AA-LCR focuses on cross-document reasoning
- **RULER**: NVIDIA's synthetic retrieval benchmark, includes NIAH variants and aggregation tasks
- **LongBench v2**: Chinese long-context benchmark, focused on Chinese scenarios

## Limitations and Controversies

1. **Limited question count**: Only 100 questions, resulting in high statistical variance and potentially unstable rankings with small samples
2. **No formal paper**: Currently lacks a peer-reviewed paper; evaluation methodology details rely on website descriptions
3. **Document type skew**: Company reports account for 63% of questions, with fewer questions in other categories, limiting coverage breadth
4. **Primarily English**: The current version is mainly oriented toward English scenarios
5. **Token counting depends on cl100k_base**: Different models use different tokenizers, so actual input lengths may vary
6. **Huge output token variance**: Different models produce output ranging from 22K to 2.7M tokens for the same question, creating significant cost and efficiency differences

## Data Sources/References

- Artificial Analysis AA-LCR release announcement: https://artificialanalysis.ai/articles/announcing-aa-lcr
- AA-LCR Leaderboard: https://artificialanalysis.ai/evaluations/artificial-analysis-long-context-reasoning
- HuggingFace dataset: https://huggingface.co/datasets/ArtificialAnalysis/AA-LCR