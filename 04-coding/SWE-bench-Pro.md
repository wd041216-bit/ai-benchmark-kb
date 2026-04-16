# SWE-bench Pro — High-Difficulty Software Engineering Evaluation

## Basic Information

| Property | Value |
|------|-----|
| Full Name | SWE-bench Pro |
| Creator | Scale AI |
| Release Year | 2025 |
| Number of Problems | 1,865 |
| Problem Type | Real GitHub Issue → generate fix patch |
| Dataset Link | https://scale.com/leaderboard/swe-bench-pro |
| Paper Link | https://scale.com/blog/swe-bench-pro |
| GitHub | https://github.com/scaleapi/swe-bench-pro |
| Status | ✅ Recommended replacement for SWE-bench Verified |

## Overview

SWE-bench Pro is a variant of SWE-bench released by Scale AI in 2025, containing 1,865 rigorously screened high-difficulty software engineering tasks. Compared to SWE-bench Verified's 500 problems, SWE-bench Pro is not only larger in scale but also has higher problem difficulty and broader language coverage (Python, Go, TypeScript, JavaScript), making it considered a more reliable coding ability evaluation benchmark.

SWE-bench Pro was created to address two core issues facing SWE-bench Verified: first, training data contamination leading to inflated Verified scores, and second, Verified only covering Python repositories, unable to evaluate multilingual capability. Scale AI attempted to establish a more credible evaluation standard through stricter screening processes and multilingual coverage.

## Dataset Composition

### Language Distribution

| Language | Number of Problems | Proportion |
|------|----------|------|
| Python | ~1,200 | ~64% |
| TypeScript/JavaScript | ~350 | ~19% |
| Go | ~315 | ~17% |

### Difficulty Stratification

| Difficulty | Number of Problems | Description |
|------|----------|------|
| Easy | ~400 | Single-file modification, simple logic |
| Medium | ~700 | Multi-file modification, requires understanding code structure |
| Hard | ~500 | Cross-module modification, requires deep understanding of architecture |
| Very Hard | ~265 | Large-scale refactoring, complex dependency relationships |

### Key Differences from SWE-bench Verified

| Feature | SWE-bench Verified | SWE-bench Pro |
|------|-------------------|---------------|
| Number of Problems | 500 | 1,865 |
| Language Coverage | Python | Python, Go, TypeScript, JavaScript |
| Screening Method | Human-verified as solvable | Stricter screening + contamination detection |
| Contamination Protection | None | Excludes problems that may appear in training data |
| Difficulty | Medium-easy | Leans hard |
| Creator | OpenAI + Princeton | Scale AI |

## Evaluation Method

Consistent with the SWE-bench series:

```
Input: GitHub Issue description + complete code repository snapshot
  ↓
AI system: Analyze Issue, locate code, generate patch
  ↓
Output: Patch in git diff format
  ↓
Evaluation: Apply patch in Docker and run tests
  ↓
Result: % Resolved
```

**Core Metric**: % Resolved — proportion of patches passing all relevant test cases

### Contamination Detection Mechanism

SWE-bench Pro introduced training data contamination detection:
- Excludes problems where the issue description or fix patch is widely distributed in public data
- Uses cutoff dates to distinguish pre- and post-training problems
- Prioritizes more recently created issues

## Model Performance (April 2026)

| Model | % Resolved | Notes |
|------|-----------|------|
| Claude Mythos Preview | 77.8% | |
| GPT-5.3 Codex | 77.3% | |
| Claude Opus 4.6 | ~70% | |
| Gemini 3.1 Pro | ~65% | |
| DeepSeek V3.2 | ~45% | |
| Llama 4 Maverick | ~25% | |

### Comparison with Verified

| Model | Verified | Pro | Difference |
|------|----------|-----|------|
| Claude Mythos Preview | 93.9% | 77.8% | -16.1% |
| Claude Opus 4.6 | 79.2% | ~70% | ~-9% |
| GPT-5.4 | 79.2% | — | — |

Data sources: Scale AI leaderboard, various model technical reports

Note: Values with ~ are approximate, from unofficial sources or estimates. Pro scores are generally lower than Verified, primarily because problems are harder and contamination protection is stricter.

## Problem Examples

### Go Language Problem
```
Issue: Race condition in concurrent map access

In the Go HTTP handler, concurrent requests may simultaneously
read and write to a shared map without synchronization, causing
a panic: "concurrent map writes".

Reproduction:
- Start server with multiple goroutines
- Send 100+ concurrent requests
- Observe intermittent panics

Expected: No panics under concurrent load
Version: go 1.22
```

### TypeScript Problem
```
Issue: Type inference fails for conditional return types

When using conditional types in a generic function, TypeScript
fails to correctly narrow the return type in the else branch.
This causes type errors when the function is called with
satisfying type arguments.

Version: typescript 5.3
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|------|------|------|
| SWE-bench Verified | 500 human-verified problems, see [SWE-bench-Verified.md](./SWE-bench-Verified.md) | |
| SWE-bench Full | Complete 2,294 problems, see [SWE-bench.md](./SWE-bench.md) | |
| SWE-bench Live | 1,319+ problems continuously updated, contamination-resistant | |
| SWE-bench Multilingual | Multilingual version | |

## Limitations and Controversies

1. **New and Not Widely Adopted**: Released relatively recently, not yet adopted as a standard evaluation by all AI companies
2. **Scoring Controversy**: Go and TypeScript test coverage is not as good as Python's, which may affect scoring fairness
3. **Agent Framework Differences**: Like Verified, scores are highly dependent on the choice of Agent framework
4. **Double-Edged Sword of Higher Difficulty**: Harder problems provide better discriminability but may cause evaluation results to be disconnected from actual development scenarios
5. **Scale AI Commercial Interest**: Scale AI simultaneously provides evaluation services and leaderboards, creating potential conflict of interest
6. **Not Yet Saturated but Unstable**: As a newer benchmark, leaderboard rankings are changing rapidly

## Data Sources/References

- Scale AI SWE-bench Pro announcement: https://scale.com/blog/swe-bench-pro
- Scale AI leaderboard: https://scale.com/leaderboard/swe-bench-pro
- Jimenez, C., et al. "SWE-bench: Can Language Models Resolve Real-World GitHub Issues?" arXiv:2310.06770, 2023.