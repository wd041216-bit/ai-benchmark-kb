# MATH — Mathematics Problem Solving

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | MATH Dataset |
| 创建者 | Hendrycks et al. (UC Berkeley) |
| 发布年份 | 2021 |
| 题目数量 | 12,500 |
| 题型 | 自由格式数学证明/计算题 |
| 数据集链接 | https://huggingface.co/datasets/HuggingFaceH4/MATH-500 |
| 论文链接 | https://arxiv.org/abs/2103.03874 |
| 状态 | ⚠️ 接近饱和（top 模型 > 90% on MATH-500） |

## 评测维度

覆盖高中到大学水平的数学问题，分为 7 个难度等级和多个学科：

### 学科分类
1. **代数 (Algebra)**: 方程、不等式、多项式
2. **计数与概率 (Counting & Probability)**: 组合、排列、概率
3. **几何 (Geometry)**: 平面几何、立体几何、解析几何
4. **数论 (Number Theory)**: 整除、素数、同余
5. **预代数 (Prealgebra)**: 基础运算、分数、百分比
6. **预微积分 (Precalculus)**: 函数、三角、级数
7. **其他 (IntermAlgebra, etc.)**

### 难度等级
- Level 1: 最简单
- Level 5: 最困难
- Level 5 问题接近 AIME 竞赛难度

## 题目示例

### 代数 Level 3
```
Find the value of x that satisfies the equation 4^(x+1) + 4^(x+2) = 20.

Answer: 0
```

### 几何 Level 4
```
In triangle ABC, AB = 13, BC = 14, and CA = 15. Find the area of the triangle.

Answer: 84
```

### 数论 Level 5
```
Find the remainder when 2^2024 is divided by 1000.

Answer: 976
```

## 评分方式

- **主要指标**: 准确率 (Accuracy)
- **评分方法**: 最终答案的精确匹配
- **典型设置**: 4-shot + Chain-of-Thought
- **MATH-500**: 从 MATH 中精选的 500 道代表性题目

## 各模型表现（2026年4月）

| 模型 | MATH (full) | MATH-500 |
|------|------------|---------|
| GPT-5 | ~95% | ~96% |
| Claude Opus 4.6 | ~94% | ~95% |
| Gemini 3 Pro | ~93% | ~94% |
| o3-mini | ~87% | ~88% |
| DeepSeek V3 | ~85% | ~86% |
| GPT-4 (2023) | ~52% | ~55% |
| 人类竞赛者 | ~40% (Level 5) | - |

## 变体

### MATH-500
- OpenAI 从 MATH 中精选的 500 道题
- 更具代表性，评测更快
- **数据集**: https://huggingface.co/datasets/HuggingFaceH4/MATH-500

### Minerva Math
- Google DeepMind 的数学评测变体
- 包含更多竞赛级别题目
- 使用不同的评分协议

## 与 AIME 的关系

- MATH Level 5 问题难度接近 AIME
- 但 AIME 题目更新、防污染更好
- 推荐同时使用 MATH-500 和 AIME 作为数学能力评测

## 局限性

1. **接近饱和**: 顶级模型在 MATH-500 上已超过 95%
2. **答案格式敏感**: 需要精确匹配
3. **训练污染**: 大量 MATH 数据可能出现在训练集
4. **仅数值答案**: 不评估证明过程