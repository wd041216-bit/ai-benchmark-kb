# GSM8K — Grade School Math 8K

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | Grade School Math 8K |
| 创建者 | OpenAI (Cobbe et al.) |
| 发布年份 | 2021 |
| 题目数量 | 8,500（训练 7,473 + 测试 1,319） |
| 题型 | 自由格式数学应用题 |
| 数据集链接 | https://huggingface.co/datasets/openai/gsm8k |
| 论文链接 | https://arxiv.org/abs/2110.14168 |
| GitHub | https://github.com/openai/grade-school-math |
| 状态 | ⚠️ 接近饱和（top 模型 > 95%） |

## 评测维度

- **多步算术推理**: 每道题需要 2-8 步推理
- **基础四则运算**: 加减乘除
- **自然语言理解**: 理解文字描述的数学问题
- **中间步骤验证**: 支持思维链 (Chain-of-Thought) 评测

## 题目示例

### 简单题（2步）
```
Natalia sold clips to 48 of her friends in April, and then she sold half as many clips in May.
How many clips did Natalia sell altogether in April and May?

Answer: 72
Solution:
- April: 48 clips
- May: 48 / 2 = 24 clips
- Total: 48 + 24 = 72 clips
```

### 中等题（4步）
```
A baker made 125 pounds of dough. After baking, the total weight of the bread was 95 pounds.
The baker sold 60 pounds of bread. How many pounds of bread were left?

Answer: 35
Solution:
- Dough made: 125 pounds
- Bread after baking: 95 pounds
- Bread sold: 60 pounds
- Bread left: 95 - 60 = 35 pounds
```

### 复杂题（6-8步）
```
Weng earns $12 an hour for babysitting. Yesterday, she just did 50 minutes of babysitting.
How much did she earn?

Answer: 10
Solution:
- Hourly rate: $12
- Time worked: 50 minutes = 50/60 hours = 5/6 hours
- Earnings: 12 × 5/6 = 60/6 = 10 dollars
```

## 评分方式

- **主要指标**: 准确率 (Accuracy)
- **评分方法**: 最终数字答案的精确匹配
- **典型设置**: 3-shot 或 8-shot + Chain-of-Thought
- **答案格式**: 模型需输出最终数字

## 各模型表现（2026年4月）

| 模型 | GSM8K 准确率 |
|------|------------|
| Claude Opus 4 | 96.2% |
| GPT-5 | ~96% |
| Gemini 3 Pro | ~95% |
| DeepSeek V3 | ~94% |
| Llama 3 70B | ~93% |
| GPT-4 (2023) | ~92% |
| PaLM 540B (few-shot) | 58.1% |
| 人类 | ~98% |

## 变体

### GSM8K-Symbolic
- 由 Apple 研究者提出的变体
- 测试模型对数学结构的理解而非死记硬背
- 论文: "GSM-Symbolic: Understanding the Limitations of Mathematical Reasoning in Large Language Models"

### MGSM (Multilingual GSM8K)
- GSM8K 的多语言版本
- 覆盖 10 种语言

## 局限性

1. **饱和问题**: 2026年顶级模型已达 96%+，区分度极低
2. **仅小学数学**: 无法评估高级数学能力
3. **格式依赖**: 分数对格式敏感
4. **训练污染**: 大量 GSM8K 数据可能出现在训练集
5. **替代基准**: 推荐使用 MATH、AIME 等更难的数学基准