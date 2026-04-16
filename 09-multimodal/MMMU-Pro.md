# MMMU-Pro — Enhanced Multi-Discipline Multimodal Reasoning Evaluation

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | MMMU-Pro: A More Robust Multi-discipline Multimodal Understanding Benchmark |
| Creator | NYU, CMU, UW-Madison, etc. (MMMU team) |
| Release Year | 2025 (ACL 2025) |
| Number of Questions | 1,730 (Standard mode) + 1,730 (Vision mode) = 3,460 |
| Question Type | Multiple-choice questions (10 options, with images) |
| Dataset Link | https://huggingface.co/datasets/MMMU/MMMU_Pro |
| Paper Link | https://arxiv.org/abs/2409.02813 |
| Status | ✅ High discriminative power, still challenging |

## Overview

MMMU-Pro is the enhanced version of MMMU, published at ACL 2025, systematically addressing key deficiencies in the original MMMU. Core issue: many questions in the original MMMU could be correctly answered by pure language models (without seeing the images), meaning the evaluation may have been testing language reasoning rather than multimodal understanding capabilities.

MMMU-Pro significantly improves evaluation robustness through a three-step enhancement pipeline: **filtering language shortcuts → expanding options → vision input mode**, reducing model performance by 16.8%–26.9% compared to the original MMMU, more accurately reflecting true multimodal reasoning capabilities.

This benchmark has been adopted by technical reports for frontier models such as Claude Opus 4.6 and GPT-5, becoming one of the core metrics for measuring multimodal reasoning capabilities.

## Dataset Composition

### Three-Step Construction Pipeline

#### Step 1: Filter Language Shortcut Questions

4 strong open-source language models (without images) were used to answer each original MMMU question 10 times:

| Filter Model | Parameters |
|---------|--------|
| Llama3-70B-Instruct | 70B |
| Qwen2-72B-Instruct | 72B |
| Yi-1.5-34B-Chat | 34B |
| Mixtral-8x22B-Instruct | 141B |

- If a model correctly answers >5 out of 10 times, the question is marked as "language shortcut solvable"
- If ≥3/4 models mark a question as language shortcut solvable, it is excluded
- 60 questions/discipline × 30 disciplines = 1,800 questions were randomly sampled from the remaining questions

#### Step 2: Expand Options (4 → 10)

- Expand 4 options to 10 options
- Use GPT-4o to generate distractors → filter with Claude 3.5 → 2 rounds of human review
- Human review simultaneously removes questions with weak image associations
- Final retention: **1,730 questions**

#### Step 3: Vision Input Mode

- Embed question text into screenshots/photos, requiring the model to "read" the question from the image
- Human annotators captured screens in diverse display environments (different backgrounds, fonts, font sizes)
- Produces **1,730 vision mode questions**

### Final Dataset

| Mode | Number of Questions | Options | Input Method |
|------|--------|--------|----------|
| Standard | 1,730 | 10 | Image + question text |
| Vision | 1,730 | 10 | Image only (question embedded in image) |
| **Total** | **3,460** | — | — |

### Discipline Distribution

Same 6 major discipline groups and 30 disciplines as original MMMU, approximately 58 questions per discipline.

## Evaluation Method

### Evaluation Metrics

- **Overall score** = **Average** of Standard mode accuracy and Vision mode accuracy
- Reported separately for 6 major discipline groups
- Supports both Direct and Chain-of-Thought (CoT) evaluation modes, taking the higher score

### CoT Evaluation Findings

| Discipline Type | CoT Effect | Example |
|----------|----------|------|
| Reasoning-intensive (Technology & Engineering) | Significant improvement | GPT-4o +14.5% |
| Subjective disciplines (Art & Design) | May decrease | LLaVA-OV-72B -17.1% |
| Perception tasks | Little impact | — |

### Difficulty Comparison with Original MMMU

| Model | MMMU (Val, 4 options) | MMMU-Pro Standard (10 options) | MMMU-Pro Vision | Performance Drop |
|------|-------------------|---------------------------|-----------------|----------|
| GPT-4o | 69.1% | 54.0% | 49.7% | -19.4% |
| Claude 3.5 Sonnet | 68.3% | 55.0% | 48.0% | -20.3% |
| Gemini 1.5 Pro | 65.8% | 49.4% | 44.4% | -21.4% |
| Qwen2-VL-72B | 64.5% | 49.2% | 43.3% | -21.2% |
| Human experts (high level) | 88.6% | 85.4% | 85.4% | -3.2% |

> Human experts only drop ~3% on MMMU-Pro, while top AI models drop 16.8%–26.9%, indicating that MMMU-Pro better distinguishes true multimodal reasoning from language shortcuts.

## Model Performance (April 2026)

| Model | MMMU-Pro | Notes |
|------|----------|------|
| GPT-5.4 | 81.2%^1 | Current best |
| Gemini 3 Flash | 81.0%^1 | |
| Gemini 3 Pro | 80.5%^1 | |
| GPT-5.2 | 79.5%^1 | |
| GPT-5 | 78.5%^1 | |
| Claude Opus 4.6 | 77.3%^1 | Cited in Anthropic technical report |
| GPT-5.4 mini | 76.8%^1 | |
| Claude Sonnet 4.6 | 75.6%^1 | |
| Human experts | ~85% | Reference upper bound |

> ^1 Data source: [llm-stats.com MMMU-Pro Leaderboard](https://llm-stats.com/benchmarks/mmmu-pro); different evaluation configurations may cause slight differences.

> Note: Different leaderboards (llm-stats vs BenchLM) may have different values, possibly due to different evaluation configurations (Standard vs Vision mode weights, number of options, etc.). Some BenchLM data shows higher scores, possibly using different settings.

**Trend assessment**: MMMU-Pro remains significantly challenging for current top models, with human experts leading the best AI models by approximately 4-7 percentage points. With the rapid advancement of model reasoning capabilities, this benchmark may face some saturation pressure within the next year.

## Example Questions

### Standard Mode

```
[Image: A circuit schematic with resistors and capacitors]
In the circuit shown, if R1 = 100Ω and C1 = 10μF, what is the time constant?
A) 0.1ms  B) 1ms  C) 10ms  D) 100ms  E) 1s  F) 0.01ms  G) 50ms  H) 5ms  I) 0.5ms  J) 20ms

Answer: B
```

### Vision Mode

```
[Image: A screenshot photo with question text embedded in the image, surrounded by different backgrounds and font styles]

The model must simultaneously: (1) OCR the question text from the image, (2) understand the professional charts/diagrams in the image, (3) perform multi-step reasoning
```

### Comparison with Original MMMU

```
Original MMMU:
  - 4 options, random guessing baseline 25%
  - Some questions can be answered by pure language models

MMMU-Pro:
  - 10 options, random guessing baseline 10%
  - All questions filtered for language shortcuts
  - Added Vision mode, forcing models to read information from images
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|------|------|------|
| **MMMU** | Original version (4 options, includes language shortcuts) | See MMMU.md |
| **MMMU-Pro with Tools** | Variant allowing models to use image cropping tools | https://huggingface.co/datasets/MMMU/MMMU_Pro |
| **MME-CoT** | Specifically evaluates multimodal chain-of-thought reasoning quality | https://github.com/MME-Benchmarks/MME-CoT |
| **MathVista** | Mathematical visual reasoning | https://arxiv.org/abs/2310.02255 |
| **VQAv2** | Classic visual QA benchmark | See VQAv2.md |
| **MVBench** | Video understanding evaluation | See MVBench.md |

## Limitations and Controversies

1. **Reduced question count**: Reduced from 11,500+ questions in original MMMU to 1,730, reducing statistical power
2. **10-option distractor quality**: GPT-4o-generated distractors may be too similar to the correct answer or too obviously wrong
3. **Vision mode OCR bias**: Vision mode is essentially a joint test of OCR + reasoning, which may over-emphasize OCR capability
4. **Filtering pipeline model dependency**: Using 4 specific open-source models for filtering may introduce systematic bias (different model combinations would retain different question sets)
5. **Human evaluator level variance**: There is a significant gap between high-level human experts (85.4%) and average individuals, making the reference line's representativeness questionable
6. **Saturation trend**: GPT-5.4 has reached 81.2%, only ~4 percentage points from human experts at 85.4%, and the discrimination window is narrowing

## Data Sources/References

- Yue et al., "MMMU-Pro: A More Robust Multi-discipline Multimodal Understanding Benchmark", ACL 2025 — https://arxiv.org/abs/2409.02813
- MMMU-Pro project page — https://mmmu-benchmark.github.io
- MMMU-Pro leaderboard — https://llm-stats.com/benchmarks/mmmu-pro
- BenchLM MMMU-Pro leaderboard — https://benchlm.ai/benchmarks/mmmuPro
- MMMU (original version) — See MMMU.md