# SWE-bench Verified — Human-Verified Software Engineering Evaluation

## Basic Information

| Property | Value |
|------|-----|
| Full Name | SWE-bench Verified |
| Creator | OpenAI + Princeton NLP |
| Release Year | 2024-2025 |
| Number of Problems | 500 |
| Problem Type | Real GitHub Issue → generate fix patch |
| Dataset Link | https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified |
| Paper Link | https://arxiv.org/abs/2310.06770 |
| GitHub | https://github.com/princeton-nlp/SWE-bench |
| Status | ✅ The most important code evaluation benchmark variant |

## Overview

SWE-bench Verified is a human-verified subset of the SWE-bench Full dataset, selected through collaboration between OpenAI and Princeton NLP, containing 500 GitHub Issue fix tasks confirmed as solvable by human engineers.

SWE-bench Verified has become the de facto standard for AI coding ability evaluation in 2025-2026. Nearly all major AI companies (OpenAI, Anthropic, Google, DeepSeek, etc.) report scores on this dataset in their technical reports, replacing the original SWE-bench Full which contained a large number of unsolvable problems.

Of the 2,294 problems in the original SWE-bench Full, a significant proportion had issues such as unclear descriptions, non-reproducible issues, or non-unique answers, leading to unreliable evaluation results. The Verified subset addressed this through individual human verification, ensuring each problem has a clear correct fix solution.

## Dataset Composition

### Source Repositories (12 Python repositories)

| Repository | Number of Problems | Domain |
|------|----------|------|
| django/django | ~150 | Web framework |
| scikit-learn/scikit-learn | ~70 | Machine learning |
| matplotlib/matplotlib | ~50 | Data visualization |
| sympy/sympy | ~40 | Symbolic computation |
| flask/flask | ~30 | Web framework |
| requests/requests | ~25 | HTTP library |
| Other 6 repositories | ~135 | Various Python projects |

### Problem Screening Criteria

1. **Issue Reproducible**: Bug description is clear and can be independently reproduced
2. **Unique Fix Solution**: A clear correct fix patch exists
3. **Test Verifiable**: Corresponding test cases exist to verify fix correctness
4. **Human Confirmed**: Each problem reviewed by a professional engineer

## Evaluation Method

Consistent with SWE-bench Full:

```
Input: GitHub Issue description + complete code repository snapshot
  ↓
AI system: Analyze Issue, locate code, generate patch
  ↓
Output: Patch in git diff format
  ↓
Evaluation: Apply patch in Docker and run tests
  ↓
Result: % Resolved (proportion passing all relevant tests)
```

**Core Metric**: % Resolved — proportion of patches passing all relevant test cases

## Model Performance (April 2026)

| Model | % Resolved | Notes |
|------|-----------|------|
| Claude Mythos Preview | 93.9% | Released April 2026 |
| GPT-5.4 | 79.2% | |
| Claude Opus 4.6 | 79.2% | |
| Gemini 3 Flash | 76.2% | |
| DeepSeek V3.2 | ~60% | |
| Llama 4 Maverick | ~40% | |

### Historical Comparison (Same Model, Different Time Periods)

| Model | Time | % Resolved |
|------|------|-----------|
| Claude 3.5 Sonnet | 2024 Q4 | ~49% |
| Claude 3.5 Sonnet + SWE-Agent | 2024 Q4 | ~55% |
| o1 + SWE-Agent | 2024 Q4 | ~48% |
| GPT-4o | 2024 Q3 | ~33% |

Data sources: Anthropic/OpenAI/Google/DeepSeek technical reports and public evaluations

Note: Values with ~ are approximate, from unofficial sources or estimates.

## Problem Example

### Issue Description
```
Title: DataFrame.groupby() produces incorrect results with nullable int dtype

When using groupby on a DataFrame with nullable integer dtype (Int64),
the sum aggregation produces incorrect results. The values are off by
a factor related to the number of groups.

Version: pandas 2.0.3
```

### Correct Patch
```diff
--- a/pandas/core/groupby/groupby.py
+++ b/pandas/core/groupby/groupby.py
@@ -1234,7 +1234,7 @@
- result = self._aggregate_named()
+ result = self._aggregate_named().astype(self.obj.dtype)
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|------|------|------|
| SWE-bench Full | Complete 2,294 problems, see [SWE-bench.md](./SWE-bench.md) | |
| SWE-bench Lite | 300-problem lighter subset | |
| SWE-bench Pro | 1,865 harder tasks, see [SWE-bench-Pro.md](./SWE-bench-Pro.md) | |
| SWE-bench Live | 1,319+ problems continuously updated, contamination-resistant | |
| SWE-bench Multilingual | Multilingual version | |

## Limitations and Controversies

1. **Python Only**: Only covers 12 Python repositories, not representative of multilingual software engineering capability
2. **Repository Scope**: 12 repositories have limited coverage, fix patterns may be concentrated in specific domains
3. **Agent Dependency**: Scores are highly dependent on the Agent framework used (SWE-Agent, OpenHands, etc.), with significant differences between frameworks
4. **Contamination Risk**: Problems come from public GitHub repositories; Issues and fix patches may appear in training data
5. **Scoring Method Controversy**: Patches only need to pass tests, there may be cases of "passing tests but not being a correct fix"
6. **Gradually Saturating**: Top models have reached 90%+, discriminability is decreasing

## Data Sources/References

- Jimenez, C., et al. "SWE-bench: Can Language Models Resolve Real-World GitHub Issues?" arXiv:2310.06770, 2023.
- OpenAI SWE-bench Verified announcement and evaluation results
- SWE-bench official website: https://www.swebench.com
- HuggingFace SWE-bench Verified: https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified