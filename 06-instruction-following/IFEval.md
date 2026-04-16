# IFEval — Instruction Following Evaluation

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | Instruction Following Evaluation |
| Creator | Google (Zhou et al.) |
| Release Year | 2023 |
| Number of Questions | 541 |
| Question Type | Instructions with constraints |
| Dataset Link | https://huggingface.co/datasets/google/IFEval |
| Paper Link | https://arxiv.org/abs/2311.07911 |
| Status | ✅ Still discriminative |

## Evaluation Dimensions

IFEval tests whether models strictly follow various format and content constraints:

### Constraint Types

| Constraint Category | Example |
|---------|------|
| Keyword constraint | "Include the word 'however' in your response" |
| Length constraint | "Answer in exactly 3 sentences" |
| Format constraint | "Format your answer as a JSON object" |
| Language constraint | "Respond entirely in French" |
| Structure constraint | "Start each paragraph with a number" |
| Content constraint | "Do not use the word 'the' in your response" |
| Punctuation constraint | "End your response with a period" |
| Case constraint | "Write your entire response in lowercase" |

## Example Questions

### Simple Constraint
```
Write a poem about the ocean. Your response must contain exactly 4 paragraphs, and each paragraph must start with the word "The".
```

### Compound Constraints
```
Explain quantum computing in 200 words or less. Your response must:
1. Include the keyword "superposition"
2. Be formatted as a numbered list
3. Not contain any commas
4. End with the phrase "Quantum is the future."
```

### Format Constraint
```
Create a JSON object with the following properties:
- name: a fictional character
- age: a number between 20 and 30
- skills: an array of exactly 3 strings
The JSON must be valid and the response should contain nothing else.
```

## Scoring Method

- **Strict matching**: Scored strictly according to constraint conditions
- **Fine-grained scoring**: Each constraint is scored independently
- **Prompt level**: Divided into prompt-level and instance-level strict accuracy
- **Automated scoring**: No LLM judging required; pure rule-based verification

## Model Performance (April 2026)

| Model | IFEval Strict Accuracy |
|------|-------------|
| GPT-5.2-Codex | ~85% |
| Claude Sonnet 4.5 | ~84% |
| Gemini 3 Pro | ~82% |
| DeepSeek V3 | ~78% |
| Llama 4 Maverick | ~72% |

## Variants

### IFBench
- Updated version of IFEval
- More constraint types and more complex combinations
- Released in 2025

### Related Benchmarks
- **MT-Bench**: Multi-turn instruction following (focused on dialogue quality)
- **AlpacaEval**: Automated evaluation of instruction following

## Why IFEval Matters

1. **Practical value**: Instruction following is the most critical capability for LLMs in production environments
2. **Automated scoring**: No LLM judging required; scoring is objective
3. **Fine-grained**: Can analyze which specific constraints a model fails on
4. **Reproducible**: Scoring is fully deterministic

## Limitations

1. **Overly mechanical**: Strict matching may penalize reasonable responses
2. **Format-heavy**: Focuses more on format than content quality
3. **Constraint combinations**: Compound constraint tests may exceed practical needs
4. **English-centric**: Primarily tests English instructions