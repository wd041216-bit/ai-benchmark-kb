# SWE-bench — Software Engineering Benchmark

## Basic Information

| Property | Value |
|------|-----|
| Full Name | SWE-bench: Can Language Models Resolve Real-World GitHub Issues? |
| Creator | Princeton NLP (Jimenez et al.) |
| Release Year | 2023 |
| Number of Problems | 2,294 (Full), 500 (Verified) |
| Problem Type | Real GitHub Issue → generate fix patch |
| Dataset Link | https://www.swebench.com |
| Paper Link | https://arxiv.org/abs/2310.06770 |
| GitHub | https://github.com/princeton-nlp/SWE-bench |
| Status | ✅ Still discriminative (top models < 80%) |

## Evaluation Dimensions

SWE-bench is the benchmark that most closely approximates real software engineering for evaluating AI code capability:

1. **Issue Understanding**: Understanding real bug reports
2. **Code Navigation**: Locating problems in large repositories
3. **Code Editing**: Generating correct fix patches
4. **Test Passing**: Patches must pass relevant test cases

## Workflow

```
Input: GitHub Issue description + complete code repository
↓
AI system: Analyze Issue, locate code, generate patch
↓
Output: Patch in git diff format
↓
Evaluation: Apply patch in Docker and run tests
↓
Result: Pass / Fail
```

## Problem Example

### Issue Description
```
Title: DataFrame.groupby() produces incorrect results with nullable int dtype

When using groupby on a DataFrame with nullable integer dtype (Int64),
the sum aggregation produces incorrect results. The values are off by
a factor related to the number of groups.

Expected behavior:
>>> df.groupby('key')['value'].sum()
key
A    10
B    20
Name: value, dtype: Int64

Actual behavior:
>>> df.groupby('key')['value'].sum()
key
A    30
B    60
Name: value, dtype: Int64

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

## Dataset Variants

### SWE-bench Full (2,294 problems)
- Complete dataset
- Covers 12 Python repositories
- Issue: Many problems are ambiguous or unsolvable

### SWE-bench Verified (500 problems)
- Filtered by OpenAI in collaboration with Princeton
- Each problem verified as solvable by a human engineer
- **Most widely used subset**
- **Dataset**: https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified

### SWE-bench Lite (300 problems)
- Lighter subset
- Suitable for quick evaluation

### SWE-bench Pro
- Harder subset with more complex tasks
- New standard in 2026

### SWE-bench Live (1,319+ problems, continuously updated)
- Continuously updated version created by Microsoft
- ~50 new problems added monthly
- From 93+ repositories (far more than the original 12)
- Prevents training data contamination
- **Dataset**: https://huggingface.co/datasets/SWE-bench-Live

### SWE-bench Multilingual
- Supports C/C++, C#, TypeScript/JavaScript, Go, Rust, Java
- Evaluates multilingual issue-fixing ability

## Model Performance (April 2026)

### SWE-bench Verified

| Model | Resolved |
|------|--------|
| Claude Mythos Preview | 93.9% |
| GPT-5.4 | 79.2% |
| Claude Opus 4.6 | 79.2% |
| Gemini 3 Flash | 76.2% |
| DeepSeek V3.2 | ~60% |
| Llama 4 Maverick | ~40% |

### SWE-bench Pro

| Model | Resolved |
|------|--------|
| Claude Mythos Preview | 77.8% |
| GPT-5.3 Codex | 77.3% |
| Claude Opus 4.6 | ~70% |
| Gemini 3.1 Pro | ~65% |

### SWE-bench Live (Lite)

| Model | Resolved |
|------|--------|
| OpenHands + Qwen3-Coder | 24.67% |
| SWE-Agent + GPT-5 | ~19% |
| OpenHands + Claude 4.5 | ~18% |

## Why SWE-bench is the Most Important Code Benchmark

1. **Authenticity**: Based on GitHub Issues from 12+ real open-source repositories
2. **End-to-End Evaluation**: Full workflow from Issue understanding to patch generation
3. **Automated Scoring**: Run tests in Docker environments
4. **Cannot Be Cheated**: Cannot be solved through simple pattern matching
5. **Still Room**: Top models at ~80% on the Verified subset

## Limitations

1. **Python Only**: Original version only covers Python repositories
2. **Repository Scope**: 12 repositories have limited coverage
3. **Scoring Bias**: Different agent frameworks produce significantly different scores
4. **Update Lag**: Original dataset is no longer updated
5. **High Compute Cost**: Requires complete Docker environments for evaluation