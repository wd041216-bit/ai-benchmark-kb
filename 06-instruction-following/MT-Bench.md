# MT-Bench — Multi-Turn Instruction Following Evaluation

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | Multi-Turn Benchmark (MT-Bench) |
| Creator | LMSYS (UC Berkeley) |
| Release Year | 2023 |
| Number of Questions | 80 (multi-turn prompts, 160 dialogue turns total) |
| Question Type | Multi-turn open-ended dialogue |
| Dataset Link | https://huggingface.co/datasets/HuggingFaceH4/mt_bench_prompts |
| Paper Link | https://arxiv.org/abs/2306.05685 |
| GitHub | https://github.com/lm-sys/FastChat |
| Status | ✅ Still widely used, but limited by question scale |

## Overview

MT-Bench was developed by LMSYS (the same team behind Chatbot Arena) to evaluate large language models' instruction following capabilities in multi-turn dialogue scenarios. The benchmark contains 80 multi-turn dialogue prompts covering 8 categories, requiring models to demonstrate coherent, high-quality performance across two consecutive dialogue turns. Evaluation uses the LLM-as-Judge method, initially using GPT-4 as the judge model to score each turn (1-10 scale), and reporting the average score.

MT-Bench's core contribution is proposing and validating the LLM-as-Judge paradigm, demonstrating that scores from strong LLMs (such as GPT-4) are highly consistent with human preferences, laying the foundation for subsequent large-scale automated evaluation.

## Dataset Composition

MT-Bench's 80 prompts are distributed across 8 categories, with 10 prompts per category:

| Category | English Name | Example Direction |
|------|--------|---------|
| Writing | writing | Composing emails, essays, creative texts |
| Role-playing | roleplay | Dialogue playing specific characters |
| Reasoning | reasoning | Logical reasoning, causal analysis |
| Math | math | Mathematical computation and proofs |
| Coding | coding | Code generation and debugging |
| Information Extraction | extraction | Extracting structured information from text |
| STEM | STEM | Physics, chemistry, biology questions |
| Humanities | humanities | History, philosophy, social issues |

Each prompt includes two dialogue turns: the first turn poses an initial question, and the second turn follows up based on the first turn's response, testing the model's ability to continuously follow instructions within context.

## Evaluation Method

### LLM-as-Judge

MT-Bench's core evaluation mechanism is LLM-as-Judge:

1. **Judge model**: Initially used GPT-4 as the judge model; subsequently, the community has also used Claude, Gemini, and other models as judges
2. **Scoring range**: 1-10 scale
3. **Scoring method**: The judge model scores based on response quality, relevance, accuracy, and other dimensions
4. **Final score**: Reports the average score across all turns

### Single-Turn vs Multi-Turn

| Metric | Description |
|------|------|
| First Turn Score | Average score for first-turn responses |
| Second Turn Score | Average score for second-turn responses |
| Average Score | Combined average score across both turns |

### Judging Modes

MT-Bench's paper proposed three judging modes:

| Mode | Description | Agreement with Humans |
|------|------|------------|
| Pairwise comparison | Pairwise comparison of two responses | Highest |
| Single-answer grading | Single-answer scoring | Relatively high |
| Reference-based | Scoring against reference answers | Medium |

In practice, single-answer grading is most commonly used due to its higher efficiency.

## Model Performance (April 2026)

| Model | Average Score (/10) | First Turn | Second Turn |
|------|-------------|--------|--------|
| GPT-5 | ~9.4 | ~9.6 | ~9.2 |
| Claude Opus 4.6 | ~9.2 | ~9.4 | ~9.0 |
| Gemini 3 Pro | ~9.1 | ~9.3 | ~8.9 |
| Claude Sonnet 4.5 | ~8.9 | ~9.1 | ~8.7 |
| DeepSeek V3 | ~8.7 | ~8.9 | ~8.5 |
| GPT-4o | ~8.5 | ~8.7 | ~8.3 |
| Llama 4 Maverick | ~8.2 | ~8.4 | ~8.0 |
| Llama 3.3 70B | ~7.8 | ~8.0 | ~7.6 |
| Mistral Large 2 | ~7.6 | ~7.8 | ~7.4 |

Note: Values marked with ~ are approximations from unofficial sources or estimates.

Data source: FastChat official leaderboard, various model technical reports, community evaluation results.

## Example Questions

### Writing (First Turn + Second Turn)

**First Turn:**
```
Write a formal email to a potential business partner proposing a joint venture in the renewable energy sector. The email should be professional, concise, and highlight the mutual benefits.
```

**Second Turn:**
```
Now rewrite the same email but make it more persuasive and emotionally appealing while maintaining professionalism.
```

### Math (First Turn + Second Turn)

**First Turn:**
```
Solve the following equation and explain each step: 3x^2 - 12x + 9 = 0
```

**Second Turn:**
```
Now generalize your approach to solve ax^2 + bx + c = 0, and discuss the conditions for real solutions.
```

### Coding (First Turn + Second Turn)

**First Turn:**
```
Write a Python function that finds the longest increasing subsequence in a list of integers.
```

**Second Turn:**
```
Can you optimize the solution to run in O(n log n) time complexity? Explain the optimization.
```

## Variants and Related Benchmarks

### MT-Bench-101

- An expanded version of MT-Bench
- Adds more categories and more fine-grained evaluation dimensions
- Community-driven with continuous updates

### Chatbot Arena

- Created by the same LMSYS team (see [Chatbot Arena](../10-dialogue-generation/Chatbot-Arena.md))
- MT-Bench serves as a complement to its automated evaluation
- Arena uses real human voting, MT-Bench uses LLM judging
- The two validate each other: MT-Bench scores are highly correlated with Arena Elo rankings

### Arena-Hard-Auto

- Also developed by LMSYS
- Focused on high-difficulty programming and reasoning problems
- Correlation with Chatbot Arena rankings reaches 0.97
- Can be seen as a strengthened version of MT-Bench focused on coding

### Related Benchmarks

- **AlpacaEval**: Also an instruction following automated evaluation, but uses single-turn prompts (see [AlpacaEval](AlpacaEval.md))
- **IFEval**: Tests instruction following with format constraints, complementary to MT-Bench's focus on dialogue quality (see [IFEval](IFEval.md))

## Limitations and Controversies

1. **Small question scale**: Only 80 prompts, limited evaluation granularity, susceptible to overfitting
2. **Judge bias**: LLM-as-Judge has position bias (preferring answers listed first), length bias (preferring longer responses), and self-preference bias (preferring responses in the model's own style)
3. **Category imbalance**: 8 categories with 10 questions each, insufficient for in-depth evaluation of any single domain
4. **Ambiguous scoring standards**: The 1-10 scale lacks clear scoring anchors; absolute scores from different judge models vary significantly
5. **Data leakage risk**: MT-Bench prompts are public; some models may have seen them during training
6. **No Chinese evaluation**: All prompts are in English; cannot evaluate Chinese instruction following capabilities
7. **Insufficient depth in second-turn evaluation**: The complexity and depth of second-turn follow-up questions are limited

## Data Sources/References

- Zheng et al., "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena," 2023. https://arxiv.org/abs/2306.05685
- FastChat GitHub: https://github.com/lm-sys/FastChat
- LMSYS Chatbot Arena: https://chat.lmsys.org
- HuggingFaceH4/mt_bench_prompts: https://huggingface.co/datasets/HuggingFaceH4/mt_bench_prompts