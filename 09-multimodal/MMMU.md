# MMMU — Multi-Discipline Multimodal Understanding Evaluation

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | A Massive Multi-discipline Multimodal Understanding and Reasoning Benchmark |
| Creator | NYU, CMU, UW-Madison, etc. |
| Release Year | 2024 (CVPR 2024) |
| Number of Questions | 11,500+ (30 disciplines) |
| Question Type | Multiple-choice questions (with images, 4 options) |
| Dataset Link | https://huggingface.co/datasets/MMMU/MMMU |
| Paper Link | https://arxiv.org/abs/2311.16502 |
| Status | ✅ Still discriminative |

## Overview

MMMU is the first benchmark to systematically evaluate multimodal large language models' **university-level** cross-disciplinary reasoning capabilities. Unlike previous VQA benchmarks focused on everyday visual understanding, MMMU focuses on high-difficulty questions requiring **domain expertise + visual reasoning**, spanning 30 disciplines from art history to quantum physics.

Core design philosophy: True artificial general intelligence (AGI) needs to integrate visual perception and deep reasoning like human experts — relying solely on language priors or simple image captioning is far from sufficient.

## Dataset Composition

### 6 Major Discipline Groups and 30 Disciplines

| Discipline Group | Included Disciplines |
|--------|----------|
| **Art & Design** | Art History, Design Theory |
| **Business** | Accounting, Economics, Finance, Management, Marketing |
| **Science** | Biology, Chemistry, Geography, Physics |
| **Health & Medicine** | Clinical Medicine, Public Health |
| **Humanities & Social Sciences** | History, Sociology, Psychology |
| **Technology & Engineering** | Computer Science, Electrical Engineering, Mechanical Engineering |

### Image Type Distribution

MMMU contains 30 highly heterogeneous image types, reflecting the visual diversity of university-level exams:

| Major Image Type | Count | Description |
|-------------|------|------|
| Diagrams | ~3,184 | Largest category |
| Tables | ~2,267 | Data and statistics |
| Plots & Charts | ~840 | Bar/line/pie charts |
| Photographs | ~770 | Real-world scenes |
| Chemical Structures | ~573 | Molecular formulas |
| Paintings | ~453 | Artworks |
| Geometric Shapes | ~336 | Math/physics diagrams |
| Sheet Music | ~335 | Music theory |
| Medical Images | ~272 | Clinical images |
| Pathological Images | ~253 | Histology |
| Microscopic Images | ~226 | Biology/materials |
| MRI/CT/X-ray | ~198 | Radiology images |
| Other | ~600+ | Including maps, blueprints, sheet music, etc. |

> Note: A single image can belong to multiple types, so the total exceeds the number of questions.

### Key Features

- All questions are from university-level exams and textbooks
- Each question must rely on an image to be answered correctly (though some questions in the original MMMU have language shortcuts, see MMMU-Pro)
- 4-option multiple-choice format

## Evaluation Method

### Standard Evaluation Process

1. Input image + question text + 4 options
2. Model outputs the option letter (A/B/C/D)
3. Calculate accuracy for each discipline and overall

### CoT vs Non-CoT Evaluation

MMMU supports two evaluation modes:

- **Direct**: Model directly outputs the option letter
- **CoT (Chain-of-Thought)**: Model first outputs reasoning process, then gives the final answer

**Key Findings**:

| Evaluation Mode | Effect |
|----------|------|
| CoT on reasoning-intensive disciplines | Significant improvement (Technology & Engineering +14.5%) |
| CoT on subjective disciplines | May decrease (Art & Design -17.1%) |
| CoT on perception tasks | Little or negative impact |

CoT evaluation takes the **higher score** between Direct and CoT as the reported result, but the two modes perform differently across disciplines, so reporting by discipline is recommended.

### Scoring Metrics

- **Overall accuracy**: Correct rate across all questions
- **Discipline-level accuracy**: Calculated separately for 30 disciplines
- **Discipline group accuracy**: Aggregated performance across 6 major discipline groups

## Model Performance (April 2026)

| Model | MMMU | Notes |
|------|------|------|
| o4 Mini High | 79.2% | Current best |
| GPT-5 | 79.1% | |
| Qwen3.5-122B-A10B | 78.1% | Best open-source |
| Claude Opus 4.5 | 76.3%^1 | |
| Claude Sonnet 4.6 | 75.3% | |
| Gemini 2.0 Flash | 69.0% | |
| GPT-4o | 59.1% | Reference baseline |
| Human experts | ~85% | Reference upper bound |

> ^1 Claude Opus 4.5 scores the same (76.3%) on MMMU with and without the Thinking variant, indicating that reasoning mode does not provide additional benefit on this benchmark.

> Data source: [pricepertoken.com MMMU Leaderboard](https://pricepertoken.com/leaderboards/benchmark/mmmu), March 2026 data.

## Example Questions

### Chemistry
```
[Image: A molecular structure diagram of a chemical reaction]
Based on the molecular structure shown, which functional group is highlighted?
A) Hydroxyl  B) Carbonyl  C) Carboxyl  D) Amino

Answer: C
```

### Medicine
```
[Image: A chest X-ray]
This chest X-ray most likely shows which of the following conditions?
A) Pneumonia  B) Pleural effusion  C) Normal  D) Lung cancer

Answer: A
```

### Engineering
```
[Image: A circuit diagram]
In the circuit shown, what is the current through resistor R2?
A) 0.5A  B) 1.0A  C) 1.5A  D) 2.0A

Answer: B
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|------|------|------|
| **MMMU-Pro** | Enhanced version: filtered language shortcuts, 10 options, vision input mode | See MMMU-Pro.md |
| **VQAv2** | Classic visual QA standard benchmark | See VQAv2.md |
| **MVBench** | Video understanding evaluation (20 subtasks) | See MVBench.md |
| **MME** | Multimodal evaluation (perception + cognition) | https://arxiv.org/abs/2306.13394 |
| **MathVista** | Mathematical visual reasoning | https://arxiv.org/abs/2310.02255 |
| **AI2D** | Science diagram understanding | https://allenai.org/data/ai2d |
| **MMLU** | Text-only multi-discipline benchmark (MMMU's language control) | https://arxiv.org/abs/2009.03300 |

## Limitations and Controversies

1. **Language shortcut problem**: Some questions in the original MMMU can be correctly answered by pure language models (without looking at images), which is the core motivation for MMMU-Pro's improvements
2. **4-option guessing baseline**: Random guessing achieves 25% accuracy; after expanding to 10 options (MMMU-Pro), this drops to 10%
3. **Discipline coverage bias**: Image types are predominantly charts and tables (>50%), with fewer natural photographs
4. **Large performance gap across professional image types**: Models perform better on photographs and paintings, but close to random guessing on sheet music, chemical structures, and geometric shapes
5. **Cultural bias**: Questions are primarily from English textbooks and exams, with insufficient coverage of non-English cultural contexts
6. **Varying expertise of human evaluators**: The human expert reference line (~85%) is based on PhD-level evaluators, which differs from the general population's level

## Data Sources/References

- Yue et al., "MMMU: A Massive Multi-discipline Multimodal Understanding and Reasoning Benchmark for Expert AGI", CVPR 2024 — https://arxiv.org/abs/2311.16502
- MMMU project page — https://mmmu-benchmark.github.io
- MMMU GitHub — https://github.com/MMMU-Benchmark/MMMU
- MMMU dataset — https://huggingface.co/datasets/MMMU/MMMU
- MMMU-Pro (enhanced version) — See MMMU-Pro.md