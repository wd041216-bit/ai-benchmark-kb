# AIME — 美国数学邀请赛评测

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | American Invitational Mathematics Examination |
| 创建者 | MAA (Mathematical Association of America) |
| 适配为 Benchmark | 2024 |
| 题目数量 | 15 题/年 (AIME 2024), 15 题/年 (AIME 2025) |
| 题型 | 自由格式数学题（0-999整数答案） |
| 数据集链接 | https://huggingface.co/datasets (搜索 AIME 2024/2025) |
| 状态 | ✅ 极具区分度（top 模型 < 50%） |

## 评测维度

AIME 是美国高中数学竞赛的二级赛事，难度远超 AMC：

1. **深度数学推理**: 需要多步、创造性推理
2. **竞赛级数学**: 覆盖代数、数论、组合、几何
3. **精确计算**: 答案为 0-999 之间的整数
4. **无选择题**: 纯自由格式答案

## 题目示例

### AIME 2024 Problem 1
```
Find the number of positive integers less than 1000 that can be expressed as the sum
of consecutive positive integers in exactly two different ways.

Answer: 6
```

### AIME 2025 Problem 8
```
A convex hexagon with area 2025 is inscribed in a circle. The hexagon has exactly
one pair of parallel sides. Find the maximum possible value of the product of the
lengths of the three diagonals of the hexagon that do not share endpoints.

Answer: TBD
```

## 各模型表现（2026年4月）

| 模型 | AIME 2024 | AIME 2025 |
|------|-----------|-----------|
| GPT-5.2 Pro | ~99% | ~97% |
| Gemini 3 Flash Preview | ~97% | ~94% |
| DeepSeek V3.2 Speciale | ~90% | ~89% |
| Claude Opus 4.6 (Thinking) | ~85% | ~80% |
| o3-mini High | ~80% | ~75% |
| DeepSeek R1 | ~79% | ~72% |
| GPT-4 (2023) | ~12% | ~8% |

## 为何 AIME 重要

1. **高区分度**: 即使 2026年的前沿模型，在 AIME 2025 上也未达到 100%
2. **防污染**: 每年新题目，训练数据中不可能有
3. **数学推理金标准**: 测试真正的数学推理能力
4. **简单评分**: 答案为整数，无歧义

## 与其他数学 Benchmark 的比较

| Benchmark | 难度 | 区分度(2026) | 题目数 |
|-----------|------|-------------|--------|
| GSM8K | 小学 | ⚠️ 已饱和 | 8,500 |
| MATH | 高中-竞赛 | ⚠️ 接近饱和 | 12,500 |
| AIME 2025 | 竞赛 | ✅ 高区分度 | 15 |
| FrontierMath | 研究级 | ✅ 极高区分度 | ~800 |

## 局限性

1. **题目数量少**: 每年仅 15 题，统计意义有限
2. **仅整数答案**: 不测试证明能力
3. **覆盖面窄**: 不包含大学数学