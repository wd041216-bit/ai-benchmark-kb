# ARC-AGI — Abstraction and Reasoning Corpus

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Abstraction and Reasoning Corpus for Artificial General Intelligence |
| Creator | François Chollet (Creator of Keras) |
| Release Year | 2019 (ARC), 2024 (ARC-AGI-2) |
| Number of Problems | 400 (training) + 400 (evaluation) |
| Problem Type | Visual pattern recognition and reasoning |
| Dataset Link | https://github.com/fchollet/ARC-AGI |
| Website | https://arcprize.org |
| Status | ✅ Highly discriminative (top models < 5%) |

## Evaluation Dimensions

ARC-AGI tests the abstract reasoning ability that humans possess innately:

1. **Pattern Recognition**: Identify patterns from a small number of examples
2. **Abstract Reasoning**: Apply discovered patterns to new scenarios
3. **Cross-Domain Generalization**: Each problem is an entirely new pattern
4. **Minimal Prior Knowledge**: No domain-specific knowledge required

## Problem Format

Each problem contains:
- 2-5 input-output example pairs (demonstration examples)
- 1 test input
- The model must predict the correct test output

### Problem Example

```
Demo Example 1:
Input:        Output:
[0,0,0]     [0,1,0]
[0,1,0]  →  [1,1,1]
[0,0,0]     [0,1,0]

Demo Example 2:
Input:        Output:
[0,0,0,0]   [0,0,1,0]
[0,1,1,0] → [0,1,1,0]
[0,0,0,0]   [0,0,1,0]

Test Input:
[0,0,0,0,0]
[0,0,0,1,0]
[0,0,0,0,0]
[0,1,0,0,0]

(The model must predict the correct output)
```

Rule: The cell represented by 1 is expanded into a cross shape

## ARC-AGI-2 (2025)

### Key Improvements
- **Stricter format**: Unified grid sizes
- **More task types**: Added transformation, symmetry, topology, and other patterns
- **Private evaluation set**: Prevents data contamination
- **Prize**: ARC Prize Fund offers $1M+ in rewards

### Scoring Method
- Each problem allows 2 submissions
- Correctly passing all test cases counts as 1 point
- Total score = number of correct problems / total number of problems

## Model Performance (April 2026)

| Model | ARC-AGI | ARC-AGI-2 |
|------|--------|-----------|
| GPT-5 (thinking mode) | ~5% | ~2% |
| Claude Opus 4.6 | ~4% | ~1.5% |
| Gemini 3 Pro | ~4% | ~1% |
| DeepSeek R1 | ~2% | ~<1% |
| Humans | ~98% | ~95% |
| Random | ~0% | ~0% |

## Why ARC-AGI is the Most Important Reasoning Benchmark

1. **Measures General Intelligence**: Tests abstract reasoning rather than specific knowledge
2. **Cannot Be Cheated**: Each problem is an entirely new pattern
3. **Easy for Humans**: Humans perform nearly perfectly, but AI performs extremely poorly
4. **Largest Gap**: One of the largest capability gaps between AI and humans
5. **AGI Indicator**: If AI reaches human level on ARC-AGI, it means approaching AGI

## ARC Prize

- **Prize**: $1,000,000+
- **Goal**: Drive research toward achieving human-level performance on ARC-AGI
- **Rules**: Open-source submissions, public leaderboard
- **Website**: https://arcprize.org

## Limitations

1. **Small problem count**: Only 400 training + 400 evaluation problems
2. **Special format**: Grid transformation tasks have a large gap from real-world tasks
3. **Unstable scoring**: Small sample size leads to high variance
4. **Purely visual**: Does not involve language understanding