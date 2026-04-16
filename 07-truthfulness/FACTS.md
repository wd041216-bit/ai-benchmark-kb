# FACTS — Multi-Dimensional Factuality Evaluation Suite

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | FACTS Benchmark Suite |
| Creator | Google DeepMind & Kaggle |
| Release Year | 2024 (Grounding), 2025 (Suite) |
| Number of Questions | 3,513 (total across four sub-benchmarks) |
| Question Type | Factuality QA (multiple choice + open-ended) |
| Website Link | https://www.kaggle.com/benchmarks/google/facts |
| Paper Link | FACTS Grounding (2024), FACTS Suite (2025) |
| Status | ✅ Still discriminative (top models < 70%) |

## Four Sub-Benchmarks

### 1. FACTS Grounding v2 (Document Grounding)
- **What it tests**: Given a long document, answer questions and ensure answers are fully grounded in the document
- **Number of questions**: 860 (public) + 859 (private)
- **Document length**: Up to 32,000 tokens
- **Domain coverage**: Finance, technology, retail, healthcare, legal
- **Task types**: Summarization, QA, rewriting

### 2. FACTS Parametric (Parametric Knowledge)
- **What it tests**: Answer factual questions using only the model's internal knowledge, without any external tools
- **Number of questions**: 1,052 (public) + 1,052 (private)
- **Question type**: Encyclopedia-style QA
- **Feature**: Tests the accuracy of the model's "memorized knowledge"

### 3. FACTS Search (Search-Augmented)
- **What it tests**: Models can use a web search API to answer factual questions
- **Number of questions**: 890 (public) + 994 (private)
- **Feature**: Requires multi-step search and information integration
- **Search tool**: Provided uniformly to ensure fair comparison

### 4. FACTS Multimodal (Multimodal Factuality)
- **What it tests**: Image-based factual QA
- **Number of questions**: 711 (public) + 811 (private)
- **Image types**: Photos, charts, maps, etc.
- **Feature**: Tests the combination of visual understanding and factual knowledge

## Scoring Method

- **Automated scoring**: Uses three frontier LLMs as judges
  - Gemini 1.5 Pro
  - GPT-4o
  - Claude 3.5 Sonnet
- **FACTS Score**: Average accuracy across four sub-benchmarks (public + private)
- **Private set**: Managed by Kaggle to prevent data contamination

## Model Performance (December 2025)

| Model | FACTS Score | Grounding | Multimodal | Parametric | Search |
|------|------------|-----------|------------|------------|--------|
| Gemini 3 Pro | 68.8 | 69.0 | 46.1 | 76.4 | 83.8 |
| Gemini 2.5 Pro | 62.1 | 74.2 | 46.9 | 63.2 | 63.9 |
| GPT 5 | 61.8 | 69.6 | 44.1 | 55.8 | 77.7 |
| Grok 4 | 53.6 | 54.7 | 25.7 | 58.6 | 75.3 |
| GPT o3 | 52.0 | 36.2 | 39.9 | 57.1 | 74.8 |
| Claude 4.5 Opus | 51.3 | 62.1 | 39.2 | 30.6 | 73.2 |
| GPT 4.1 | 50.5 | 45.6 | 40.1 | 51.5 | 64.6 |

## Key Findings

1. **Search augmentation significantly improves performance**: All models perform best on the Search sub-benchmark
2. **Multimodal is the hardest**: All models score lowest on the Multimodal sub-benchmark (< 50%)
3. **Large differences in parametric knowledge**: Gemini 3 Pro leads GPT o3 by nearly 20% on Parametric
4. **Varied grounding capabilities**: Gemini 2.5 Pro is strongest on Grounding

## Example Questions

### FACTS Grounding
```
Document: [30-page financial report]
Question: What was the company's revenue growth rate in Q3 2024?
Instructions: Answer based ONLY on the provided document.
```

### FACTS Parametric
```
Question: What is the chemical symbol for the element with atomic number 79?
Answer: Au (Gold)
```

### FACTS Search
```
Question: Who won the Nobel Prize in Physics in 2024?
Instructions: Use the provided search API to find the answer.
```

### FACTS Multimodal
```
[Image: A complex scientific diagram]
Question: What does the y-axis represent in this figure?
```

## Why FACTS Matters

1. **Comprehensiveness**: The only benchmark that simultaneously evaluates parametric knowledge, search augmentation, document grounding, and multimodal factuality
2. **Contamination prevention**: Public + private dual sets
3. **Automated scoring**: Multiple LLM judges reduce bias
4. **Real-time rankings**: Kaggle continuously updates the leaderboard

## Relationship with SimpleQA

- SimpleQA (OpenAI) only evaluates short-answer factuality
- SimpleQA Verified (Google DeepMind) improved SimpleQA's annotation quality issues
- FACTS is a more comprehensive factuality evaluation