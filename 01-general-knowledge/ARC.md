# ARC — AI2 Reasoning Challenge

## Basic Information

| Property | Value |
|----------|-------|
| Full Name | AI2 Reasoning Challenge |
| Creator | Allen Institute for AI (Peter Clark et al.) |
| Release Year | 2018 |
| Number of Questions | 7,787 (Challenge) + 5,197 (Easy) |
| Question Type | Multiple choice (3-5 options) |
| Dataset Link | https://huggingface.co/datasets/allenai/ai2_arc |
| Paper Link | https://arxiv.org/abs/1803.05457 |
| Status | Approaching saturation |

## ARC-Easy vs ARC-Challenge

### ARC-Easy
- 5,197 easier science questions
- Random baseline: ~25%
- Top models: ~95%

### ARC-Challenge
- 7,787 more difficult science reasoning questions
- Requires multi-step reasoning
- Random baseline: ~25%
- Top models: ~85%

## Evaluation Dimensions

- Scientific knowledge (physics, chemistry, biology, earth science)
- Logical reasoning
- Multi-step reasoning
- Commonsense reasoning

## Example Question

```
Question: A student wants to test whether a certain type of soil is good for growing plants.
Which of the following is the best way to conduct this experiment?
A) Plant one type of plant in the soil and observe it for one day
B) Plant several types of plants in the soil and observe them for several weeks
C) Plant one type of plant in the soil and compare it with a plant grown in different soil
D) Add water to the soil and observe whether the soil changes color

Answer: C
```

## Model Performance (April 2026)

| Model | ARC-Challenge |
|-------|---------------|
| GPT-5 | ~96% |
| Claude Opus 4.6 | ~95% |
| Gemini 3 Pro | ~95% |
| GPT-4 (2023) | ~90% |

## Note

**ARC-AGI** (covered separately in this knowledge base) is a different benchmark that tests abstract reasoning. ARC (this file) tests scientific reasoning.