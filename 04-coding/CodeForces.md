# CodeForces Rating — Competitive Programming Ability Evaluation

## Basic Information

| Property | Value |
|------|-----|
| Full Name | CodeForces Rating / Competitive Programming Benchmark |
| Creator | CodeForces (Mike Mirzayanov), evaluation organized by various AI companies |
| Release Year | 2010 (platform) / 2024 (AI evaluation) |
| Number of Problems | 8,000+ (continuously growing) |
| Problem Type | Competitive programming problems (algorithms and data structures) |
| Dataset Link | https://codeforces.com/problemset |
| Paper Link | No unified paper; various model technical reports report results independently |
| GitHub | https://github.com/codeforces |
| Status | ✅ High discriminability, continuously updated |

## Overview

CodeForces is one of the world's largest competitive programming online platforms, featuring 8,000+ algorithm programming problems rated by ELO scoring. Since 2024, companies like DeepSeek have started using CodeForces problems as an important evaluation benchmark for AI models' algorithmic reasoning ability.

CodeForces problems range from ELO 800 to 3500, covering various algorithm types including greedy, dynamic programming, graph theory, math, and data structures. Problems require writing correct algorithmic solutions within time and space constraints, testing models' deep reasoning and algorithm design ability.

## Dataset Composition

### ELO Difficulty Levels

| Level | ELO Range | Difficulty Description | Problem Proportion |
|------|----------|----------|----------|
| Gray | 800-1199 | Entry-level | ~20% |
| Green | 1200-1599 | Easy | ~25% |
| Blue | 1600-1999 | Medium | ~20% |
| Purple | 2000-2399 | Hard | ~15% |
| Yellow | 2400-2799 | Very Hard | ~10% |
| Red | 2800-3500 | Master | ~5% |
| LGM (Red-Black) | 3000+ | Legendary Grandmaster | ~5% |

### Algorithm Type Distribution

| Type | Proportion | Typical Algorithms |
|------|------|----------|
| Greedy | ~25% | Greedy strategies, constructive |
| Dynamic Programming (DP) | ~20% | Knapsack, interval DP, state compression |
| Graph Theory | ~15% | BFS/DFS, shortest path, spanning tree |
| Math | ~15% | Number theory, combinatorics, probability |
| Data Structures | ~10% | Segment tree, binary indexed tree, union-find |
| String | ~8% | KMP, suffix array, hashing |
| Constructive | ~7% | Constructive proofs, simulation |

## Evaluation Method

AI model evaluation on CodeForces typically has two approaches:

### 1. Pass@k Method
- Select problems within specific ELO ranges from the platform
- Model generates code and submits it to the CodeForces evaluation system
- Calculate first-attempt pass rate (Pass@1)
- Report results stratified by ELO level

### 2. ELO Rating Method
- Model participates in CodeForces virtual contests
- ELO rating is calculated based on contest results
- Direct comparison with human contestants

### Evaluation Environment
- Strict time and memory limits
- Multiple test case sets (including hidden tests)
- Supports C++, Python, Java, and other languages

## Model Performance (April 2026)

### Pass@1 by ELO Level

| Model | 800-1199 | 1200-1599 | 1600-1999 | 2000-2399 | 2400+ |
|------|----------|-----------|-----------|-----------|-------|
| Claude Opus 4.6 | ~95% | ~80% | ~55% | ~25% | ~8% |
| GPT-5 | ~93% | ~78% | ~52% | ~23% | ~7% |
| DeepSeek R1 | ~90% | ~75% | ~48% | ~20% | ~5% |
| Gemini 3 Pro | ~88% | ~70% | ~42% | ~18% | ~4% |
| DeepSeek V3 | ~85% | ~65% | ~38% | ~15% | ~3% |
| Llama 4 Maverick | ~70% | ~45% | ~20% | ~8% | ~2% |

### Simulated ELO Rating

| Model | Simulated ELO | Corresponding Human Level |
|------|----------|-------------|
| Claude Opus 4.6 | ~1900 | Expert |
| GPT-5 | ~1850 | Expert |
| DeepSeek R1 | ~1750 | Candidate Master |
| Gemini 3 Pro | ~1650 | Expert (lower bound) |
| DeepSeek V3 | ~1550 | Specialist |

Data sources: DeepSeek V3/R1 technical reports, various model public evaluation results

Note: Values with ~ are approximate, from unofficial sources or estimates. ELO ratings vary significantly depending on evaluation method and problem selection.

## Problem Examples

### ELO 800 (Entry-level)
```
Problem: Two Sum
Given n integers, find two numbers such that their sum equals the target value.
Input: n=4, arr=[2,7,11,15], target=9
Output: [0,1] (0-indexed)
Time limit: 2 seconds
```

### ELO 1600 (Medium)
```
Problem: Number of Longest Increasing Subsequences
Given an integer array, find the length of the longest increasing subsequence and
the number of distinct subsequences that achieve that length, modulo 10^9+7.
n ≤ 2000, 1 ≤ a[i] ≤ 10^9
Time limit: 2 seconds
```

### ELO 2400 (Very Hard)
```
Problem: Path Coloring on a Tree
Given a tree with n nodes, each edge initially uncolored. Perform q operations,
each specifying a path and coloring all edges on that path with a given color (overwriting previous colors).
Output the final color of each edge. Requires Heavy-Light Decomposition or Link-Cut Tree.
n,q ≤ 2×10^5
Time limit: 3 seconds
```

## Variants and Related Benchmarks

| Variant/Related | Description |
|-----------|------|
| CodeForces Div.2 | Lower difficulty contests (ELO < 2100) |
| CodeForces Div.1 | Higher difficulty contests (ELO ≥ 2100) |
| LiveCodeBench | Live scraping from CodeForces and other platforms, see [LiveCodeBench.md](./LiveCodeBench.md) |
| AIME | Competition-level math reasoning, see [AIME.md](../14-competition-math/AIME.md) |
| USACO | USA Computing Olympiad, another competitive programming benchmark |

## Limitations and Controversies

1. **Contamination Risk**: CodeForces problems are publicly accessible, with many solutions present in training data, posing data contamination risks
2. **Non-uniform Evaluation**: Different companies select different ELO ranges and evaluation methods, making results difficult to compare directly
3. **Language Bias**: C++ dominates in competitive programming, while Python often fails time limits due to runtime efficiency
4. **Time Pressure**: Competitive programming problems have strict time limits, but LLM-generated code is not subject to time limits, raising fairness questions
5. **No Standard Dataset**: There is no "official" AI evaluation subset; each party selects their own problems
6. **Reasoning vs Coding**: CodeForces primarily tests algorithmic reasoning, not software engineering ability

## Data Sources/References

- CodeForces official website: https://codeforces.com
- DeepSeek-V3 technical report: https://arxiv.org/abs/2412.19437
- DeepSeek-R1 technical report: https://arxiv.org/abs/2501.12948