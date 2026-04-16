# FrontierMath — Frontier Mathematics Evaluation

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | FrontierMath: A Benchmark for Evaluating Advanced Mathematical Reasoning in AI |
| Creators | Epoch AI (led by Elliot Glazer, Ege Erdil, Tamay Besiroglu et al., including multiple mathematicians) |
| Year Published | November 2024 (arXiv preprint), continuously updated through 2025 |
| Number of Questions | 350 questions (Tiers 1-3 totaling 300 + Tier 4 totaling 50) |
| Task Type | Free-response math problems (numeric/symbolic/tuple answers) |
| Dataset Link | https://epoch.ai/benchmarks/frontiermath |
| Paper Link | https://arxiv.org/abs/2411.04872 |
| Status | ✅ Extremely high discrimination (top models ~50%) |

## Overview

FrontierMath is a mathematical reasoning evaluation benchmark developed by Epoch AI, containing 350 original high-difficulty math problems covering core areas of modern mathematics including algebraic geometry, number theory, real analysis, combinatorics, and category theory. Its core design principles are:

1. **Extremely High Standards**: Problems are carefully designed by professional mathematicians (including math competition gold medalists, PhD students, and professors); most problems require hours to days of professional research to solve
2. **Contamination Prevention**: All problems are original and unpublished, with a private evaluation set preventing training data leakage
3. **Automatically Verifiable**: Answers are computable definite values (large integers, symbolic reals, tuples, etc.) that can be automatically verified by executing Python functions
4. **Multi-Level Difficulty**: Divided into four difficulty levels from Tiers 1-4, ranging from IMO-level to short-term research project-level

The project is funded by OpenAI, which has exclusive access to some problems, but Epoch AI maintains editorial independence.

## Dataset Composition

### Difficulty Tiers

| Tier | Number of Questions | Difficulty Description | Expected Solving Time |
|------|---------------------|------------------------|-----------------------|
| Tier 1 | ~60 | Similar to IMO problems/advanced undergraduate exercises, but allowing tools and programming | Hours |
| Tier 2 | ~120 | Advanced graduate level, requiring professional proofs, programming, and multi-step reasoning | Hours to a day |
| Tier 3 | ~120 | Similar to early exploratory research questions for PhD students | Days |
| Tier 4 | 50 | Short-term research projects designed by math professors and postdocs | Days to weeks |

### Problem Domain Distribution

Covering major branches of modern mathematics:
- Number theory (algebraic number theory, analytic number theory, computational number theory)
- Real and complex analysis
- Algebraic geometry
- Combinatorics
- Category theory and homological algebra
- Topology
- Differential equations
- Probability theory and stochastic processes

### Problem Design Requirements

Each problem must satisfy:
1. **Deterministic Answer**: The answer is a verifiable number, symbolic real, or finite tuple
2. **Anti-Guessing Design**: Random attempts or brute-force search have extremely low success probability (vast answer space)
3. **Computational Feasibility**: Verification script runs within 60 seconds on standard hardware
4. **Originality**: The problem has not appeared in any public source

### Peer Review Process

- Each problem undergoes peer review by professional mathematicians to verify correctness, lack of ambiguity, and difficulty rating
- Secondary review randomly samples a subset, finding approximately 1/20 of problems have errors requiring correction
- Problems are rated on three dimensions: Background (1-5, high school to research level), Creativity (how many hours an expert needs to discover the key insight), Execution (how many hours to convert the insight into a solution)

## Evaluation Method

### Evaluation Framework

- Uses the UK AI Safety Institute's (UK AISI) **Inspect** evaluation framework
- Models can freely reason and execute Python code in a sandbox environment
- Mathematical libraries including NumPy, SymPy, SciPy, gmpy2, and mpmath are available

### Evaluation Process

1. The model reads the problem and generates a reasoning process
2. The model submits a Python function `answer()` that returns the answer when called
3. The system executes the `answer()` function (30-second runtime limit) and compares the result with the reference answer
4. **Token Limit**: 1,000,000 tokens (hard limit), forced submission at 660,000 tokens

### Pass@k Evaluation

- **pass@1**: Single-attempt pass rate (strictest)
- **pass@k**: Proportion of problems passed at least once in k independent samples
- **pass@the-kitchen-sink**: Joint pass rate across all models and all runs

### Human Baseline

In early 2025, a competition was held at MIT with approximately 40 outstanding undergraduate math students forming 8 teams, on 23 Tier 1-3 problems:
- **Average Team Score**: 19%
- **All Teams Collectively Solved**: 35% of problems

## Model Performance (April 2026)

### Tiers 1-3 (300 questions)

| Model | pass@1 | pass@16 | Notes |
|-------|--------|---------|-------|
| GPT-5.4 Pro | ~40-50% | — | Highest score as of March 2026¹ |
| Gemini 3 Pro Deep Think | ~38% | — | ¹ |
| ChatGPT Agent (pass@16) | — | ~49% | Joint multi-model² |
| GPT-5 (high) | ~27% | ~46% | ² |
| GPT-5 (medium) | ~25% | — | ² |
| Gemini 3 Pro Preview | ~38% | — | ±3% margin² |
| Gemini 2.5 Pro | ~10% | — | ±2% margin² |
| o3-mini (high) | ~11% | ~18% | pass@16² |
| o1 (high) | ~9% | — | Early 2025 data² |
| Claude 3.7 Sonnet | ~3-5% | — | Early 2025 data² |
| GPT-4o, Grok 2, Mistral Large | ~0% | — | Early 2025 data² |

### Tier 4 (50 questions, extremely difficult)

| Model | pass@1 | Notes |
|-------|--------|-------|
| GPT-5.4 Pro | ~38% | ¹ |
| Gemini 3 Pro Deep Think | ~19% | ±6% margin² |
| Grok 4 | ~2% | ±2% margin² |

### Human vs AI Comparison

| Evaluated On | Tiers 1-3 (subset of ~23 questions) |
|-------------|--------------------------------------|
| Human math teams (average) | 19% |
| Human math teams (best) | ~35% |
| AI best (GPT-5.4 Pro) | ~40-50% (full 300 questions) |

> ¹ Data from llm-stats.com and similar leaderboards, either self-reported by model developers or third-party evaluations
> ² Data from Epoch AI official paper and blog

### Pass@k Growth Analysis

Epoch AI analyzed the trend of pass@k as k increases:
- **Sub-logarithmic growth**: Each time k doubles, pass@k increases by only approximately 2.6 percentage points
- **Joint pass@the-kitchen-sink across all models and all runs**: 57% (165/290 questions)
- **Estimated upper bound**: Even with unlimited retries, approximately 20% of problems are completely unsolvable by current models

## Example Problems

### Tier 1 Example (IMO Level)

```
Determine the number of positive integers n ≤ 10^6 such that the sum of
the decimal digits of n equals the sum of the decimal digits of n^2.

def answer():
    # Returns an integer
    return 42  # Example format, not the real answer
```

### Tier 2 Example (Graduate Level)

```
Let p be a prime number. Define S(p) as the sum over all polynomials
f(x) ∈ Z/pZ[x] of degree at most p-1 of the number of roots of f in Z/pZ.
Compute S(p) for p = 2027.

def answer():
    # Returns a large integer
    return 1234567890  # Example format
```

### Tier 3 Example (Research Level)

```
For a positive integer n, let f(n) denote the number of isomorphism classes
of groups of order n. Determine the largest integer k such that
f(p^k) > f(p^(k+1)) for at least half of all primes p < 10^5.

def answer():
    # Returns an integer
    return 7  # Example format
```

### Tier 4 Example (Short-Term Research Project Level)

```
Involves computing fine invariants in algebraic geometry or verifying deep
conjectures in number theory, requiring days to weeks of specialized research
by mathematicians.

Answers are typically invariants of high-dimensional objects, large integers,
or complex symbolic expressions.
```

> Note: Real problems are private; the above are style examples only, not actual problems.

## Variants and Related Benchmarks

| Benchmark | Relationship | Comparison |
|-----------|-------------|------------|
| [AIME](AIME.md) | Lower difficulty reference | AIME is high school competition level, FrontierMath Tier 1 ≈ IMO level |
| [HMMT](HMMT.md) | Lower difficulty reference | HMMT is competition level, FrontierMath far exceeds its difficulty |
| MATH / MATH-500 | Lower difficulty reference | MATH is high school level, nearing saturation |
| Humanity's Last Exam (HLE) | Similar difficulty reference | HLE is cross-disciplinary expert level, FrontierMath focuses on mathematics |
| IMO Grand Challenge | Similar goal | IMO is proof-based, FrontierMath has numerical answers |
| MathArena | Competition math evaluation | Difficulty between AIME and FrontierMath |

### Difficulty Comparison with Other Math Benchmarks

| Benchmark | Difficulty | Best Frontier Model (April 2026) | Discrimination |
|-----------|-----------|--------------------------------|----------------|
| GSM8K | Elementary | ~100% | ❌ Saturated |
| MATH-500 | High school | ~95%+ | ⚠️ Approaching saturation |
| AIME 2025 | Competition | ~100% (with tools) | ⚠️ Approaching saturation |
| HMMT25 | Competition+ | ~97% | ⚠️ Gradually saturating |
| IMO 2025 | Olympiad | ~83% | ✅ Still discriminative |
| **FrontierMath Tiers 1-3** | **Research-level** | **~50%** | **✅ High discrimination** |
| **FrontierMath Tier 4** | **Research frontier** | **~38%** | **✅ Extremely high discrimination** |

## Limitations and Controversies

1. **OpenAI Conflict of Interest**: The project is funded by OpenAI, which has exclusive access to some problems, raising questions about independence
2. **Private Evaluation Set Trust Issues**: Problems are not public; third parties cannot independently verify evaluation results
3. **Numeric Answers Only**: Does not test proof capabilities; a complete assessment of mathematical reasoning requires proof problems
4. **Small Sample Size**: 350 problems is more than AIME (15/year) but still yields wide statistical confidence intervals
5. **API Errors Impact**: Some model evaluations (Gemini 2.5 Pro, Gemini 3 Pro, Grok 4) experienced API errors, affecting result accuracy
6. **Version Iteration**: The benchmark has been updated to v1.1.4, including scorer fixes and a 10× token budget increase; results across versions are not fully comparable
7. **Pass@k Interpretation**: Sub-logarithmic growth means simply increasing sampling has diminishing returns; real breakthroughs require reasoning capability improvements
8. **Limited Human Baseline**: The human baseline was measured on only a 23-question subset, and was undergraduate students rather than professional mathematicians

## Data Sources / References

- Epoch AI FrontierMath official page: https://epoch.ai/benchmarks/frontiermath
- FrontierMath Tier 4 page: https://epoch.ai/benchmarks/frontiermath-tier-4
- FrontierMath Tiers 1-3 page: https://epoch.ai/benchmarks/frontiermath-tiers-1-3
- Paper: Glazer et al., "FrontierMath: A Benchmark for Evaluating Advanced Mathematical Reasoning in AI", arXiv:2411.04872, 2024-2025
- Epoch AI blog — Pass@k analysis: https://epoch.ai/gradient-updates/less-than-70-percent-of-frontiermath-is-within-reach-for-todays-models
- llm-stats leaderboard: https://llm-stats.com/benchmarks/frontiermath
- [AIME](AIME.md) — Lower difficulty reference
- [HMMT](HMMT.md) — Lower difficulty reference