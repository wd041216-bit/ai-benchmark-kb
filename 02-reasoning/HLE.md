# HLE — Humanity's Last Exam

## Basic Information

| Property | Value |
|------|-----|
| Full Name | Humanity's Last Exam |
| Creator | Center for AI Safety & Scale AI |
| Release Year | 2025 |
| Number of Problems | 2,500 |
| Problem Type | Multiple-choice + open-ended |
| Dataset Link | https://huggingface.co/datasets/cais/hle |
| Website | https://lastexam.ai |
| Status | ✅ Highly discriminative (top models < 50%) |

## Design Philosophy

HLE is called "Humanity's Last Exam," specifically designed to test the limits of AI reasoning ability:

1. **Expert-authored**: Written by researchers across various fields
2. **Beyond Training Data**: Problems require deep reasoning, not simple knowledge retrieval
3. **Continuously Updated**: Private evaluation set prevents data contamination
4. **Extremely High Difficulty**: As of April 2026, the highest score is only 45.9%

## Subject Distribution

| Subject | Proportion |
|------|------|
| Mathematics | 41% |
| Physics | 9% |
| Biology/Medicine | 11% |
| Humanities/Social Sciences | 9% |
| Computer Science | 8% |
| Chemistry | 7% |
| Engineering | 5% |
| Other | 10% |

## Problem Examples

### Mathematics (Advanced)
```
Question: Let f: R → R be a continuous function satisfying f(x+y) = f(x) + f(y) + xy for all x,y ∈ R.
If f(1) = 2, what is f(2024)?
```

### Physics
```
Question: Consider a quantum harmonic oscillator with Hamiltonian H = p²/2m + mω²x²/2.
If the oscillator is initially in the state |ψ(0)⟩ = (|0⟩ + |1⟩)/√2, what is the expectation value of energy at time t = π/(2ω)?
```

## Model Performance (April 2026)

| Model | HLE Accuracy | Calibration Error |
|------|-----------|---------|
| Gemini 3.1 Pro Preview | 45.90% | 50% |
| Claude Opus 4.6 (Thinking) | 34.44% | 46% |
| GPT-5 Pro | 31.64% | 49% |
| Kimi K2.5 | 24.37% | 67% |
| GLM 4.5 | 8.32% | 79% |
| Llama 4 Maverick | 5.68% | 83% |
| Mistral Medium 3 | 4.52% | 77% |

## Why HLE is the Most Important New Benchmark

1. **Unsaturated**: The highest score is only 45.9%, far from saturated
2. **Contamination-resistant**: Has a private evaluation set
3. **Expert-level Difficulty**: Problems require graduate-level knowledge and above
4. **Broad Coverage**: Covers multiple disciplines
5. **Becoming the New Standard**: Is replacing MMLU/GPQA as the core benchmark for frontier models