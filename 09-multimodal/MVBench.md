# MVBench — Comprehensive Multimodal Video Understanding Evaluation

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | MVBench: A Comprehensive Multi-modal Video Understanding Benchmark |
| Creator | OpenGVLab (Shanghai AI Lab) |
| Release Year | 2024 (CVPR 2024 Highlight) |
| Number of Questions | ~3,200 questions (20 subtasks, ~160 questions per subtask) |
| Question Type | Multiple-choice questions (based on video clips) |
| Dataset Link | https://huggingface.co/datasets/OpenGVLab/MVBench |
| Paper Link | https://arxiv.org/abs/2310.12922 |
| Status | ✅ Still discriminative |

## Overview

MVBench is the first systematic multimodal video understanding benchmark, published at CVPR 2024. Unlike evaluations that rely solely on single-frame image understanding, MVBench focuses on testing models' ability to understand **temporal information** — whether models truly understand dynamic changes, causal sequences, and action progressions in videos, rather than simply extracting information from key frames.

Core design philosophy: Automatically transform existing video task datasets into multiple-choice format, constructing a comprehensive video understanding capability evaluation system spanning from **perception** to **cognition**.

## Dataset Composition

### 20 Subtasks

MVBench divides video understanding capabilities into 6 major capability dimensions and 20 subtasks:

| Capability Dimension | Subtask | Source Dataset |
|----------|--------|------------|
| **Perception: Scene & Objects** | Scene Classification | Kinetics-400 |
| | Object Recognition | ImageNet-V2 |
| **Perception: Action** | Action Recognition | Kinetics-400 |
| | Action Sequence | Something-Something V2 |
| **Perception: Spatial** | Object Shuffle | CLEVRER |
| | Moving Direction | CLEVRER |
| **Perception: Attributes** | Moving Attribute | CLEVRER |
| | State Description | Something-Something V2 |
| **Cognition: Reasoning** | Counterfactual Reasoning | CLEVRER |
| | Future Prediction | CLEVRER |
| | Action Prediction | Something-Something V2 |
| **Cognition: Causality** | Causal Reasoning | CLEVRER |
| | Object Interaction | Something-Something V2 |
| **Cognition: Temporal** | Temporal Localization | Next-QA |
| | Action Order | Next-QA |
| | Fine-grained Action | Perception Test |
| **Cognition: Counting** | Object Count | CLEVRER |
| | Action Count | Something-Something V2 |
| **Cross-modal** | Egocentric Action | EgoSchema |

### Data Format

- Each question contains a video clip + a multiple-choice question
- Videos come from public datasets (Kinetics-400, Something-Something V2, CLEVRER, Next-QA, etc.)
- Random baseline accuracy is approximately 27.3% (approximately 25% for 4-option questions)

## Evaluation Method

### Evaluation Process

1. Input video clip + question text
2. Model outputs the option letter (A/B/C/D)
3. Calculate accuracy for each subtask, final score is the **uniform average across all 20 subtasks**

### Evaluation Metrics

- **Overall accuracy**: Uniform average accuracy across 20 subtasks
- **Per-dimension accuracy**: Aggregated by 6 major capability dimensions
- **Temporal understanding gain**: Comparison of performance with/without temporal information

### Key Design: Temporal vs Static

MVBench's core value lies in verifying whether models truly utilize temporal information:

- **Action Sequence**: Must understand the temporal order of actions
- **Temporal Localization**: Must locate the time point when an event occurs
- **Action Order**: Must distinguish the sequential relationship of actions
- Single-frame models perform close to random on these subtasks

## Model Performance (April 2026)

| Model | MVBench Overall | Notes |
|------|-------------|------|
| Qwen3 VL 32B Thinking | 76.6%^1 | Current best |
| Qwen3 VL 32B Instruct | 74.8%^1 | |
| Qwen3 VL 30B A3B Instruct | 74.6%^1 | |
| Qwen2.5 VL 72B Instruct | 70.4%^1 | |
| Gemini 2.5 Pro | ~69%^2 | Closed-source model |
| GPT-4o | ~62%^2 | Closed-source model |
| VideoChat2 HD (Mistral) | 62.3% | Original paper baseline |
| VideoChat2 (Mistral) | 60.4% | Original paper baseline |
| Human level | ~85%+ | Reference |

> ^1 Data source: llm-stats.com MVBench leaderboard (2025-2026)
> ^2 Values marked with ~ are approximate, from different evaluation configurations

**Trend assessment**: MVBench still has discriminative power, but the rapid progress of the Qwen3 VL series indicates that open-source models' video understanding capabilities are improving quickly. Thinking variants consistently outperform Instruct variants, suggesting that chain-of-thought reasoning significantly helps video understanding.

## Example Questions

### Action Sequence Understanding

```
[Video: A person sequentially performing the actions "pick up cup → drink water → put down cup"]

What is the correct order of actions shown in the video?
A) Pick up cup → Drink → Put down cup
B) Drink → Pick up cup → Put down cup
C) Put down cup → Pick up cup → Drink
D) Pick up cup → Put down cup → Drink

Answer: A
```

### Causal Reasoning

```
[Video: A ball rolls toward a block tower, hits it, and the tower falls]

What caused the tower to fall?
A) The wind blew it over
B) The ball hit it
C) Someone pushed it
D) It fell on its own

Answer: B
```

### Temporal Localization

```
[Video: A 30-second cooking video, stirring starts at second 18]

At what point in the video does the person start stirring?
A) At the beginning
B) Around the middle
C) Near the end
D) The person never stirs

Answer: B
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|------|------|------|
| **MVBench** | Original version, 20 subtasks | https://huggingface.co/datasets/OpenGVLab/MVBench |
| **VideoChat2** | Video understanding model from the same team | https://huggingface.co/datasets/OpenGVLab/VideoChat2 |
| **EgoSchema** | Egocentric long video understanding | https://huggingface.co/datasets/lmms-lab/EgoSchema |
| **ActivityNet-QA** | Open-ended video QA | https://activitynet.org |
| **Next-QA** | Video causal and temporal reasoning | https://nextqa.github.io |
| **Perception Test** | Fine-grained action perception | https://github.com/deepmind/perception_test |
| **LongVideoBench** | Long video understanding evaluation | https://github.com/longvideobench |
| **MLVU** | Multi-task long video understanding | https://github.com/JUNJIE99/MLVU |

## Limitations and Controversies

1. **Uneven subtask coverage**: Some subtasks have few questions (~160), resulting in large statistical variance
2. **Data source dependency**: Subtasks come from different datasets with varying quality and difficulty
3. **Multiple-choice only**: Cannot evaluate open-ended response capabilities
4. **Short video length**: Most video clips are several seconds to 30 seconds, insufficient for evaluating long video understanding
5. **Qwen dominance on leaderboard**: The 2025 leaderboard is nearly monopolized by the Qwen series, which may reflect evaluation data exposure in training corpora rather than pure capability differences
6. **Gap with real-world applications**: Real video understanding often requires open-ended description and reasoning; the multiple-choice format simplifies task difficulty

## Data Sources/References

- Li et al., "MVBench: A Comprehensive Multi-modal Video Understanding Benchmark", CVPR 2024 — https://arxiv.org/abs/2310.12922
- OpenGVLab/MVBench dataset — https://huggingface.co/datasets/OpenGVLab/MVBench
- MVBench leaderboard — https://llm-stats.com/benchmarks/mvbench