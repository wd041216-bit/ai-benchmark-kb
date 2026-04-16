# HumanEval — Human-Level Code Generation Evaluation

## Basic Information

| Property | Value |
|------|-----|
| Full Name | HumanEval: Hand-Written Code Evaluation |
| Creator | OpenAI (Chen et al.) |
| Release Year | 2021 |
| Number of Problems | 164 |
| Problem Type | Function-level code generation |
| Dataset Link | https://huggingface.co/datasets/openai/openai_humaneval |
| Paper Link | https://arxiv.org/abs/2107.03374 |
| GitHub | https://github.com/openai/human-eval |
| Status | ⚠️ Saturated (top models > 95%) |

## Evaluation Dimensions

Each problem contains:
1. **Function Signature**: Python function declaration
2. **Docstring**: Detailed functionality description and examples
3. **Test Cases**: Unit tests for verifying correctness

The model must generate a complete function implementation based on the signature and docstring.

## Problem Examples

### Simple
```python
from typing import List

def has_close_elements(numbers: List[float], threshold: float) -> bool:
    """Check if in given list of numbers, are any two numbers closer to each other than
    given threshold.
    >>> has_close_elements([1.0, 2.0, 3.0], 0.5)
    False
    >>> has_close_elements([1.0, 2.8, 3.0, 4.0, 5.0, 2.0], 0.3)
    True
    """
```

### Medium
```python
def truncate_number(number: float) -> float:
    """Given a positive floating point number, it can be decomposed into
    an integer part and a decimal part. Return the decimal part.
    >>> truncate_number(3.5)
    0.5
    """
```

### Complex
```python
from typing import List

def string_xor(a: str, b: str) -> str:
    """Input are two strings a and b consisting only of 1s and 0s.
    Perform binary XOR on these inputs and return result also as a string.
    >>> string_xor('010', '110')
    '100'
    """
```

## Scoring Method

- **Primary metric**: Pass@k
  - Pass@1: Probability of passing in a single generation
  - Pass@10: Probability of at least one pass in 10 generations
  - Pass@100: Probability of at least one pass in 100 generations
- **Scoring method**: Run test cases in an isolated Python environment
- **Most commonly used metric**: Pass@1

## Model Performance (April 2026)

| Model | Pass@1 |
|------|--------|
| Claude Opus 4.6 | ~96% |
| GPT-5 | ~95% |
| Gemini 3 Pro | ~94% |
| DeepSeek V3 | ~89% |
| GPT-4 (2023) | ~67% |
| Codex (2021) | ~29% |

## Variants

### HumanEval+
- Expanded number of test cases (average 10x tests)
- Stricter verification, preventing models from "getting lucky" with simple implementations
- **Link**: https://github.com/evalplus/evalplus

### MBPP (Most Basic Python Problems)
- 1,000 basic Python programming problems
- Created by Google Research
- Easier problems than HumanEval
- **Dataset**: https://huggingface.co/datasets/google-research-datasets/mbpp

### LiveCodeBench
- Live scraping of new problems from competitive programming platforms
- Prevents training data contamination
- **Dataset**: https://huggingface.co/datasets/LiveCodeBench

### BigCodeBench
- Large-scale code generation benchmark
- 1,140+ real-world programming problems
- Covers more Python libraries and APIs

## Limitations

1. **Saturated**: In 2026, top models have reached 95%+
2. **Python Only**: Does not cover other programming languages
3. **Function-level**: Does not test project-level code capability
4. **Simple Tasks**: Most problems are simple functions
5. **Data Contamination**: Problems may appear in training sets

## Recommended Alternatives

| Alternative | Advantage | Link |
|------|------|------|
| SWE-bench | Real issue fixing | swebench.com |
| LiveCodeBench | Contamination-resistant, continuously updated | livecodebench.org |
| SWE-bench Live | Multilingual, continuously updated | swe-bench-live.github.io |
| BigCodeBench | Larger scale, more APIs | bigcode-bench.github.io