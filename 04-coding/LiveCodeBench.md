# LiveCodeBench — Live Competitive Programming Evaluation

## Basic Information

| Property | Value |
|------|-----|
| Full Name | LiveCodeBench |
| Creator | LiveCodeBench Team (LIVEBENCH) |
| Release Year | 2024 |
| Number of Problems | Continuously updated (100+ new per quarter) |
| Problem Type | Competitive programming problems |
| Dataset Link | https://huggingface.co/datasets/LiveCodeBench |
| Website | https://livecodebench.github.io |
| Paper Link | https://arxiv.org/abs/2406.02753 |
| GitHub | https://github.com/LiveCodeBench/LiveCodeBench |
| Status | ✅ Contamination-resistant, continuously updated |

## Overview

LiveCodeBench is a live competitive programming evaluation benchmark launched in 2024, with a core design philosophy of fundamentally solving training data contamination by scraping newly published programming problems from competitive platforms like CodeForces, LeetCode, and AtCoder in real time. Since problems are published after model training cutoff dates, models cannot have seen these problems during training, ensuring evaluation fairness.

LiveCodeBench is divided into four difficulty levels: Easy, Medium, Hard, and Pro, supporting multiple programming languages including Python, C++, Java, and JavaScript. Unlike HumanEval's simple function generation, LiveCodeBench problems require complete algorithm design and implementation, better reflecting models' deep reasoning ability.

## Dataset Composition

### Problem Sources

| Source Platform | Proportion | Characteristics |
|----------|------|------|
| CodeForces | ~50% | Competitive algorithm problems, ELO rated |
| LeetCode | ~30% | Interview programming problems, engineering-oriented |
| AtCoder | ~20% | Japanese competitive programming platform, math reasoning oriented |

### Difficulty Distribution

| Level | Difficulty Description | Typical ELO | Proportion |
|------|----------|----------|------|
| Easy | Entry-simple | 800-1200 | ~30% |
| Medium | Medium | 1200-1600 | ~35% |
| Hard | Hard | 1600-2000 | ~25% |
| Pro | Very Hard | 2000+ | ~10% |

### Temporal Dimension

- **v1 (2024 Q1-Q2)**: Initial version
- **v2 (2024 Q3-Q4)**: New problems added, model rankings updated
- **v3 (2025 Q1-Q2)**: Continued expansion
- **v4 (2025 Q3-2026 Q1)**: Latest version
- Uses a time window mechanism, only using problems published after model training cutoff dates

## Evaluation Method

### Scoring Methodology

LiveCodeBench's evaluation is based on code execution and test case pass rates:

1. **Code Generation**: Model generates complete executable code based on problem description
2. **Code Execution**: Execute generated code in a sandbox environment
3. **Test Verification**: Compare output with expected results
4. **Pass Rate Calculation**: Number of test cases passed / total test cases

### Specific Scoring Process

```
Input: Programming problem description + sample input/output
  ↓
Model Generation: Complete executable code
  ↓
Execution: Run code in sandbox, input test cases
  ↓
Verification: Compare output with expected output
  ↓
Scoring: Pass@1 = proportion of problems passing all test cases in a single generation
      Can also calculate Test Case Pass Rate (test case pass rate)
```

### Evaluation Configuration

- **Temperature**: 0 (deterministic generation)
- **Maximum tokens**: 2048+
- **Language**: Primarily Python evaluation, some C++/Java evaluation
- **Time Limit**: Each problem has a clear execution time limit (1-5 seconds)

## Model Performance (April 2026)

### Stratified by Difficulty

| Model | Easy | Medium | Hard | Pro | Overall |
|------|------|--------|------|-----|------|
| Claude Opus 4.6 | ~95% | ~72% | ~48% | ~30% | ~61% |
| GPT-5 | ~96% | ~73% | ~50% | ~35% | ~63% |
| GPT-5.4 | ~98% | ~78% | ~55% | ~35% | ~67% |
| Gemini 3 Pro | ~94% | ~68% | ~42% | ~28% | ~58% |
| DeepSeek V3 | ~88% | ~60% | ~35% | ~18% | ~50% |
| DeepSeek R1 | ~92% | ~70% | ~45% | ~25% | ~58% |
| Llama 4 Maverick | ~75% | ~42% | ~20% | ~8% | ~36% |

### Historical Trends

| Model | 2024 Q4 | 2025 Q2 | 2026 Q1 |
|------|---------|---------|---------|
| Claude Opus 4.6 | ~52% | ~57% | ~61% |
| GPT-5 | ~55% | ~60% | ~63% |
| Gemini 3 Pro | ~48% | ~53% | ~58% |

Data sources: Various model technical reports and LiveCodeBench official leaderboard

Note: Values with ~ are approximate, from unofficial sources or estimates.

## Problem Examples

### Easy Difficulty
```python
# Given an integer array, find the element that appears most frequently.
# If multiple elements have the same frequency, return the smallest one.
# Input: [1, 2, 2, 3, 3, 3]
# Output: 3
```

### Medium Difficulty
```python
# Given a string s and an integer k, find the longest substring of s
# such that the substring contains at most k distinct characters.
# Input: s = "eceba", k = 2
# Output: 3 ("ece")
```

### Hard Difficulty
```python
# Given n nodes and a list of edges, construct a directed graph.
# Find all paths from node 0 to node n-1, returned in lexicographic order.
# Number of nodes n ≤ 15, cycles may exist.
# Input: n=4, edges = [[0,1],[0,2],[1,3],[2,3]]
# Output: [[0,1,3],[0,2,3]]
```

### Pro Difficulty
```python
# Given a tree with n nodes, each edge has a weight.
# Process q queries, each query finding the maximum edge weight on the path between two nodes.
# n,q ≤ 2×10^5
# Requirement: O(n log n) preprocessing + O(log n) per query
# (Requires LCA + binary lifting or heavy-light decomposition)
```

## Comparison with HumanEval

| Feature | HumanEval | LiveCodeBench |
|------|-----------|---------------|
| Number of Problems | 164 | Continuously growing |
| Difficulty | Simple-medium | Simple to very hard |
| Contamination-resistant | No | Yes |
| Authenticity | Hand-written functions | Competitive programming problems |
| Saturation | Saturated (>95%) | Still room (~65%) |
| Algorithm Depth | Shallow | Deep |
| Update Frequency | Not updated | Quarterly |
| Evaluation Method | Unit tests | Code execution + test cases |

## Variants and Related Benchmarks

| Variant/Related | Description |
|-----------|------|
| BigCodeBench | 1,140+ real-world programming problems, see [BigCodeBench.md](./BigCodeBench.md) |
| CodeForces Rating | Competitive programming ELO evaluation, see [CodeForces.md](./CodeForces.md) |
| HumanEval | 164 hand-written Python problems, see [HumanEval.md](./HumanEval.md) |
| MBPP | 1,000 basic Python problems, see [MBPP.md](./MBPP.md) |

## Limitations and Controversies

1. **Competition Bias**: Problems come from competitive programming platforms, biased toward algorithmic reasoning, not testing software engineering ability (such as debugging, refactoring)
2. **Uneven Difficulty Distribution**: Pro-level problems are very few (~10%), with limited discriminability for top models
3. **Language Limitation**: Code execution evaluation primarily uses Python; Python's runtime efficiency limitations may cause time limit exceeded (C++ does not have this issue)
4. **Problem Timeliness**: Over time, older problems may gradually "enter" training data (models may have seen them after updates)
5. **Score Fluctuation**: Different time windows have different problem difficulties, scores across different versions are difficult to compare directly
6. **Test Case Coverage**: Hidden test cases on competitive programming platforms are not fully public, evaluation may differ from official results

## Data Sources/References

- LiveCodeBench official website: https://livecodebench.github.io
- LiveCodeBench paper: https://arxiv.org/abs/2406.02753
- HuggingFace dataset: https://huggingface.co/datasets/LiveCodeBench
- CodeForces: https://codeforces.com
- LeetCode: https://leetcode.com