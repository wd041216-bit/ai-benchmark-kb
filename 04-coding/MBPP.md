# MBPP — Basic Python Programming Problems Evaluation

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Most Basic Python Problems (MBPP) |
| Creator | Google Research (Austin et al.) |
| Release Year | 2021 |
| Number of Problems | 1,000 |
| Problem Type | Function-level code generation |
| Dataset Link | https://huggingface.co/datasets/mbpp |
| Paper Link | https://arxiv.org/abs/2108.07732 |
| GitHub | https://github.com/google-research-datasets/mbpp |
| Status | ⚠️ Saturated (top models > 90%) |

## Overview

MBPP is a large-scale Python programming evaluation dataset released by Google Research in 2021, containing 1,000 basic Python programming problems, each accompanied by a functional description and corresponding test cases. Problems cover basic programming skills including array operations, string processing, mathematical computation, and data structures.

Unlike HumanEval's 164 hand-written problems, MBPP problems were primarily collected through crowdsourcing, targeting broader basic programming ability evaluation with overall lower difficulty, serving as an important early large-scale code generation benchmark.

## Dataset Composition

The MBPP dataset contains the following splits:

| Split | Number of Problems | Purpose |
|------|----------|------|
| train | 120 | Few-shot examples |
| test | 500 | Main evaluation set |
| validation | 260 | Validation set |
| sanitization | 120 | Data cleaning auxiliary set |

Each problem contains three core parts:
1. **Problem Description**: A programming task described in natural language
2. **Function Signature**: Python function declaration
3. **Test Cases**: 3+ unit tests (with input-output pairs)

Problem difficulty distribution:
- **Easy (~60%)**: Basic string/list operations, simple math
- **Medium (~30%)**: Multi-step logic, data structure operations
- **Hard (~10%)**: Complex algorithms, multi-condition decisions

## Evaluation Method

- **Primary metric**: Pass@k (consistent with HumanEval)
  - Pass@1: Probability of passing in a single generation
  - Pass@10: Probability of at least one pass in 10 generations
- **Scoring method**: Execute generated functions in an isolated Python environment and run test cases
- **Most commonly used metric**: Pass@1

## Model Performance (April 2026)

| Model | Pass@1 |
|------|--------|
| Claude Opus 4.6 | ~93% |
| GPT-5 | ~92% |
| Gemini 3 Pro | ~90% |
| DeepSeek V3 | ~85% |
| GPT-4 (2023) | ~80% |
| CodeLlama 34B (2023) | ~55% |
| Codex 12B (2021) | ~47% |

Data sources: Various model technical reports and public evaluation results

Note: Values with ~ are approximate, from unofficial sources or estimates.

## Problem Examples

### Easy
```python
def even_Parity(n):
    """Write a python function to check whether the given number is even or not.
    >>> even_Parity(4)
    True
    >>> even_Parity(5)
    False
    """
```

### Medium
```python
def max_of_subarrays(arr, k):
    """Write a function to find the maximum of each subarray of size k in the given array.
    >>> max_of_subarrays([1, 2, 3, 1, 4, 5, 2, 3, 6], 3)
    [3, 3, 4, 5, 5, 5, 6]
    >>> max_of_subarrays([8, 5, 10, 7, 9, 4, 15, 12, 90, 13], 4)
    [10, 10, 10, 15, 15, 90, 90]
    """
```

### Hard
```python
def find_kth_smallest(arr, k):
    """Write a function to find the kth smallest element in an unsorted array.
    >>> find_kth_smallest([7, 10, 4, 3, 20, 15], 3)
    7
    >>> find_kth_smallest([7, 10, 4, 3, 20, 15], 4)
    10
    """
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|------|------|------|
| MBPP+ | Extended test cases, preventing "lucky" passes | https://github.com/evalplus/evalplus |
| HumanEval | 164 hand-written Python programming problems, slightly harder | See [HumanEval.md](./HumanEval.md) |
| LiveCodeBench | Live competitive programming problems, contamination-resistant | See [LiveCodeBench.md](./LiveCodeBench.md) |
| BigCodeBench | 1,140+ real-world programming problems | See [BigCodeBench.md](./BigCodeBench.md) |

## Limitations and Controversies

1. **Saturated**: In 2026, top models have reached 90%+, with limited discriminability
2. **Low Difficulty**: Most problems are simple function implementations, unable to test complex engineering ability
3. **Python Only**: Does not cover other programming languages
4. **Insufficient Test Cases**: Original version has only 3 test cases, easy to pass by "luck" (MBPP+ has improved this)
5. **Data Contamination**: Problems and solutions are widely available on the internet and may appear in training sets
6. **Uneven Problem Quality**: Crowdsourced collection method leads to some problems with vague descriptions or insufficient testing

## Data Sources/References

- Austin, J., et al. "Program Synthesis with Large Language Models." arXiv:2108.07732, 2021.
- HuggingFace MBPP dataset: https://huggingface.co/datasets/mbpp
- EvalPlus (MBPP+): https://github.com/evalplus/evalplus