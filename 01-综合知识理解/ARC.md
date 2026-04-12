# ARC — AI2 Reasoning Challenge

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | AI2 Reasoning Challenge |
| 创建者 | Allen Institute for AI (Peter Clark et al.) |
| 发布年份 | 2018 |
| 题目数量 | 7,787 (Challenge) + 5,197 (Easy) |
| 题型 | 多项选择题（3-5个选项） |
| 数据集链接 | https://huggingface.co/datasets/allenai/ai2_arc |
| 论文链接 | https://arxiv.org/abs/1803.05457 |
| 状态 | ⚠️ 接近饱和 |

## ARC-Easy vs ARC-Challenge

### ARC-Easy
- 5,197 道较简单的科学题
- 随机基线: ~25%
- top 模型: ~95%

### ARC-Challenge
- 7,787 道较困难的科学推理题
- 需要多步推理
- 随机基线: ~25%
- top 模型: ~85%

## 评测维度

- 科学知识（物理、化学、生物、地球科学）
- 逻辑推理
- 多步推理
- 常识推理

## 题目示例

```
Question: A student wants to test whether a certain type of soil is good for growing plants.
Which of the following is the best way to conduct this experiment?
A) Plant one type of plant in the soil and observe it for one day
B) Plant several types of plants in the soil and observe them for several weeks
C) Plant one type of plant in the soil and compare it with a plant grown in different soil
D) Add water to the soil and observe whether the soil changes color

Answer: C
```

## 各模型表现（2026年4月）

| 模型 | ARC-Challenge |
|------|---------------|
| GPT-5 | ~96% |
| Claude Opus 4.6 | ~95% |
| Gemini 3 Pro | ~95% |
| GPT-4 (2023) | ~90% |

## 注意

**ARC-AGI**（本知识库单独介绍）是与此不同的 benchmark，测试抽象推理能力。ARC（本文件）测试科学推理。