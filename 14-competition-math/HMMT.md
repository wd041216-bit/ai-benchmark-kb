# HMMT — Harvard-MIT Mathematics Tournament Benchmark

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | Harvard-MIT Mathematics Tournament (HMMT) |
| Creators | Harvard University and MIT student organizations |
| Year Published | Held annually since 1998; widely used as AI benchmark since 2025 |
| Number of Questions | Approximately 66 questions per competition (30 individual + 10 team + 36 Guts) |
| Task Type | Short-answer (individual/Guts) + proof (February team round) |
| Dataset Link | https://hmmt.org |
| Paper Link | No dedicated paper; competition problems published by the organizing committee |
| Status | ⚠️ Gradually saturating (frontier models ~90-97%) |

## Overview

HMMT is an annual mathematics competition organized by Harvard University and MIT student organizations, held since 1998. It is one of the most influential high school mathematics competitions in the United States. HMMT hosts two competitions each year:

1. **HMMT November** (November): Slightly lower difficulty, aimed at more participants, equivalent to mid-AMC to upper-AIME level
2. **HMMT February** (February): Higher difficulty, equivalent to mid-AIME to USAMO level, with proof problems

The 2025 HMMT problems (HMMT25) have been used by multiple AI labs as a standard evaluation set for mathematical reasoning capability, appearing alongside AIME in the technical reports of major models.

## Dataset Composition

### HMMT February (High Difficulty)

| Round | Format | Duration | Number of Questions | Difficulty |
|-------|--------|----------|---------------------|-----------|
| Algebra & Number Theory | Individual short-answer | 50 minutes | 10 | mid-AIME to USAMO |
| Geometry | Individual short-answer | 50 minutes | 10 | mid-AIME to USAMO |
| Combinatorics | Individual short-answer | 50 minutes | 10 | mid-AIME to USAMO |
| Team Round | Team proofs | 60 minutes | 10 | USAMO level |
| Guts Round | Team short-answer (4 problems per set) | 80 minutes | 36 | Increasing difficulty |

### HMMT November (Medium-High Difficulty)

| Round | Format | Duration | Number of Questions | Difficulty |
|-------|--------|----------|---------------------|-----------|
| General | Individual short-answer | 50 minutes | 10 | mid-AMC to upper-AIME |
| Theme | Individual short-answer (themed) | 50 minutes | 10 | mid-AMC to upper-AIME |
| Team Round | Team short-answer | 60 minutes | 10 | Similar to General/Theme |
| Guts Round | Team short-answer (3 problems per set) | 80 minutes | 36 | Increasing difficulty |

### Scoring System

- **Individual Competition**: Each problem has a weight (3 to 10 points), scored by the sum of weights of correctly solved problems
- **Team Total Score (Sweepstakes)**: Sum of scaled scores from three sections
  - Individual total → scaled to 800 points maximum
  - Guts Round → scaled to 400 points maximum
  - Team Round → scaled to 400 points maximum
  - Total maximum score = 1600 points

## Evaluation Method

As an AI benchmark, HMMT25 is evaluated as follows:

1. **Problem Selection**: HMMT February 2025 individual competition problems (30 short-answer problems) are used as the evaluation set
2. **Scoring**: Scored by percentage correct, comparable to human competitors
3. **Tool Usage**: Some evaluations allow models to use Python code execution (with tools vs. without tools versions)
4. **Thinking Mode**: Most evaluation reports distinguish between Thinking (reasoning chain) and Instruct (direct answer) modes

## Model Performance (April 2026)

### HMMT25 (February 2025 Individual Competition)

| Model | HMMT25 | Notes |
|-------|--------|-------|
| Grok-4 Heavy | ~96.7% | Current highest score¹ |
| GPT-5 (high) | ~92% | ¹ |
| Grok-4 | ~90.0% | ¹ |
| Qwen3-235B-A22B-Thinking | ~83.9% | Thinking mode¹ |
| o4-mini (high) | ~80% | ¹ |
| Qwen3-Next-80B-A3B-Thinking | ~73.9% | Thinking mode¹ |
| Qwen3-235B-A22B-Instruct | ~55.4% | Instruct mode¹ |
| Qwen3-Next-80B-A3B-Instruct | ~54.1% | Instruct mode¹ |

> ¹ All data is self-reported by model developers and has not been independently verified

### Difficulty Comparison with AIME

| Benchmark | Difficulty Level | Best Frontier Model (April 2026) | Discrimination |
|-----------|-----------------|--------------------------------|----------------|
| AIME 2025 | Competition | ~100% (with tools) | ⚠️ Approaching saturation |
| HMMT25 Feb | Competition+ | ~97% | ⚠️ Gradually saturating |
| IMO 2025 | Olympiad | ~83% (5/6 problems) | Still discriminative |
| FrontierMath | Research | ~40-50% | ✅ High discrimination |

## Example Problems

### HMMT February 2025 — Algebra Problem 5 (Style Example)

```
Let f(x) be a polynomial of degree 2025 such that f(k) = 2^k for k = 0, 1, 2, ..., 2025.
Find f(2026).

Answer: (Specific integer answer)
```

### HMMT February 2025 — Team Round (Proof Problem Style)

```
Let ABC be a triangle with side lengths AB = 13, BC = 14, CA = 15.
Points D, E, F lie on BC, CA, AB respectively such that AD, BE, CF are concurrent.
Prove that ...
```

> Note: HMMT team rounds are proof problems; current AI performance on such problems is significantly weaker than on short-answer problems

## Variants and Related Benchmarks

| Benchmark | Relationship |
|-----------|-------------|
| [AIME](AIME.md) | Same competition level; AIME is short-answer, HMMT Feb is slightly harder and includes proof problems |
| [FrontierMath](FrontierMath.md) | Research-level mathematics, several orders of magnitude harder than HMMT |
| USAMO / IMO | Higher difficulty olympiad competitions, primarily proof problems |
| MATH | High school competition problem set, nearing saturation |
| MathArena | Newly launched in 2025, competition math evaluation with more olympiad-level problems |

## Limitations and Controversies

1. **Gradually Saturating**: Frontier models have reached ~90-97% on HMMT25 short-answer problems; discrimination is declining rapidly
2. **Limited Number of Questions**: Each competition has only about 30 individual short-answer problems, with limited statistical significance
3. **Only Short-Answer Portions Used for Evaluation**: Automated scoring of team proof problems is not yet mature
4. **Large Thinking vs Instruct Gap**: The same model can differ by up to 30 points between the two modes; evaluation standards need to be clarified
5. **Data Contamination Risk**: HMMT problems are publicly available on the competition website and may have been included in training data
6. **Self-Reported Scores**: All AI model scores are self-reported and lack independent third-party verification
7. **Not Directly Comparable to Human Competitions**: AI evaluations only use a subset of problems, not the full competition format

## Data Sources / References

- HMMT official website: https://hmmt.org
- HMMT February 2025 results: https://alpha.hmmt.org/www/archive/282
- HMMT25 leaderboard (llm-stats): https://llm-stats.com/benchmarks/hmmt25
- HMMT25 leaderboard (BenchLM): https://benchlm.ai/benchmarks/hmmt2025
- HMMT25 leaderboard (AIRank): https://airank.dev/benchmarks/hmmt25
- IntuitionLabs HMMT25 analysis: https://www.intuitionlabs.ai/articles/hmmt25-ai-benchmark-explained
- [AIME](AIME.md) — Comparison reference
- [FrontierMath](FrontierMath.md) — Higher difficulty evaluation