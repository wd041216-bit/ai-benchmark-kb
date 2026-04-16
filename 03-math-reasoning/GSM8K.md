# GSM8K — Grade School Math 8K

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Grade School Math 8K |
| Creator | OpenAI (Cobbe et al.) |
| Release Year | 2021 |
| Number of Problems | 8,500 (training 7,473 + test 1,319) |
| Problem Type | Free-format math word problems |
| Dataset Link | https://huggingface.co/datasets/openai/gsm8k |
| Paper Link | https://arxiv.org/abs/2110.14168 |
| GitHub | https://github.com/openai/grade-school-math |
| Status | ⚠️ Approaching saturation (top models > 95%) |

## Evaluation Dimensions

- **Multi-step Arithmetic Reasoning**: Each problem requires 2-8 steps of reasoning
- **Basic Arithmetic Operations**: Addition, subtraction, multiplication, division
- **Natural Language Understanding**: Understanding math problems described in text
- **Intermediate Step Verification**: Supports Chain-of-Thought evaluation

## Problem Examples

### Simple (2 steps)
```
Natalia sold clips to 48 of her friends in April, and then she sold half as many clips in May.
How many clips did Natalia sell altogether in April and May?

Answer: 72
Solution:
- April: 48 clips
- May: 48 / 2 = 24 clips
- Total: 48 + 24 = 72 clips
```

### Medium (4 steps)
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

### Complex (6-8 steps)
```
Weng earns $12 an hour for babysitting. Yesterday, she just did 50 minutes of babysitting.
How much did she earn?

Answer: 10
Solution:
- Hourly rate: $12
- Time worked: 50 minutes = 50/60 hours = 5/6 hours
- Earnings: 12 × 5/6 = 60/6 = 10 dollars
```

## Scoring Method

- **Primary metric**: Accuracy
- **Scoring method**: Exact match of the final numeric answer
- **Typical setup**: 3-shot or 8-shot + Chain-of-Thought
- **Answer format**: Model must output the final number

## Model Performance (April 2026)

| Model | GSM8K Accuracy |
|------|------------|
| Claude Opus 4 | 96.2% |
| GPT-5 | ~96% |
| Gemini 3 Pro | ~95% |
| DeepSeek V3 | ~94% |
| Llama 3 70B | ~93% |
| GPT-4 (2023) | ~92% |
| PaLM 540B (few-shot) | 58.1% |
| Humans | ~98% |

## Variants

### GSM8K-Symbolic
- Variant proposed by Apple researchers
- Tests model understanding of mathematical structure rather than memorization
- Paper: "GSM-Symbolic: Understanding the Limitations of Mathematical Reasoning in Large Language Models"

### MGSM (Multilingual GSM8K)
- Multilingual version of GSM8K
- Covers 10 languages

## Limitations

1. **Saturation Issue**: In 2026, top models have reached 96%+, with extremely low discriminability
2. **Only Elementary Math**: Cannot evaluate advanced mathematical ability
3. **Format Sensitivity**: Scoring is sensitive to format
4. **Training Contamination**: Large amounts of GSM8K data may appear in training sets
5. **Recommended Alternatives**: Consider using MATH, AIME, and other harder math benchmarks