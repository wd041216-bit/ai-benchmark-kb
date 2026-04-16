# MMLU-Pro — High-Difficulty Comprehensive Knowledge Evaluation

## Basic Information

| Property | Value |
|----------|-------|
| Full Name | MMLU-Pro: A More Robust and Challenging Multi-Task Language Understanding Benchmark |
| Creator | TIGER-AI-Lab (University of Waterloo); Yubo Wang, Xueguang Ma, Wenhu Chen et al. |
| Release Year | 2024 (NeurIPS 2024 Datasets and Benchmarks Track) |
| Number of Questions | 12,032 |
| Question Type | Ten-option multiple choice (A-J) |
| Number of Subjects | 14 major categories |
| Dataset Link | https://huggingface.co/datasets/TIGER-Lab/MMLU-Pro |
| Paper Link | https://arxiv.org/abs/2406.01574 |
| GitHub | https://github.com/tiger-ai-lab/mmlu-pro |
| Status | Active, currently a well-discriminating comprehensive knowledge benchmark |

## Overview

MMLU-Pro is a high-difficulty upgraded version of MMLU that addresses the gradual saturation of the original MMLU between 2024-2026 by expanding options from 4 to 10 and introducing more challenging questions. On MMLU, the accuracy gap between top models is only about 1-2%; on MMLU-Pro, the gap between equivalent models widens to 9%+, significantly improving evaluation discriminative power.

Core improvements:
- **Ten options** instead of four, reducing the random baseline from 25% to 10%
- **Consolidated 57 subjects into 14 major categories**, reducing category fragmentation
- **Introduced more difficult questions**, adding sources such as STEM Website, TheoremQA, and SciBench beyond original MMLU questions
- **Chain-of-Thought (CoT) reasoning is crucial**: CoT improves GPT-4o by ~19% on MMLU-Pro, compared to only 1.5% on the original MMLU

## Dataset Composition

### 14 Major Subject Categories

| Subject | Example Sub-fields |
|---------|-------------------|
| Math | Elementary math, advanced math, abstract algebra |
| Physics | High school physics, college physics |
| Chemistry | High school chemistry, college chemistry |
| Biology | High school biology, college biology, anatomy |
| Computer Science | Computer science, machine learning |
| Engineering | Electrical engineering |
| Economics | Microeconomics, macroeconomics, econometrics |
| Health | Clinical knowledge, medical genetics, nutrition |
| Psychology | Professional psychology, human aging |
| Business | Accounting, business ethics, management |
| Philosophy | Philosophy, logic, moral disputes |
| Law | Law, international law, professional law |
| History | World history, European history, US history |
| Other | Miscellaneous subjects |

### Data Sources

| Source | Proportion |
|--------|-----------|
| Original MMLU (filtered and de-noised) | 56.6% |
| STEM Website | 33.9% |
| TheoremQA | 4.97% |
| SciBench | 4.5% |

## Evaluation Method

- **Primary metric**: Accuracy
- **Scoring method**: Percentage of correct answers out of total questions
- **Few-shot setting**: Typically uses 5-shot
- **Random baseline**: 10% (ten options)
- **CoT setting**: Some evaluation reports provide both CoT and non-CoT results
- **Prompt robustness**: MMLU-Pro has ~2% sensitivity to prompt changes, lower than the original MMLU's 4-5%

## Model Performance (April 2026)

| Model | MMLU-Pro Accuracy | Notes |
|-------|-------------------|-------|
| Gemini 3 Pro Preview | ~89.8% | Current highest |
| Claude Opus 4.5 (Thinking) | ~89.5% | CoT reasoning |
| Gemini 3 Flash Preview (Thinking) | ~89.0% | CoT reasoning |
| Claude Sonnet 4.5 (Thinking) | ~87.5% | CoT reasoning |
| Claude Opus 4 (Thinking) | ~87.3% | CoT reasoning |
| GPT-5.2 Pro | ~88.7% | — |
| Grok 4 Heavy | ~86.4% | — |
| GPT-5.2 | ~86.3% | — |
| DeepSeek V3.2-Speciale | ~85.9% | — |
| Gemini 2.5 Pro | ~85.8% | — |
| Qwen 3.5 | ~84.6% | — |
| GPT-4o (2024) | 72.6% | Early baseline |
| Claude 3 Opus (2024) | 68.5% | Early baseline |
| Llama-3-70B (2024) | 56.2% | Early baseline |

Note: Values with ~ are approximations from unofficial sources or estimates.

Data sources: PricePerToken Leaderboard, BenchLM.ai, company technical reports

### Comparison with MMLU

| Model | MMLU | MMLU-Pro | Gap |
|-------|------|----------|-----|
| GPT-4o | ~88.7% | 72.6% | -16.1% |
| Claude 3 Opus | ~86.8% | 68.5% | -18.3% |
| GPT-4 Turbo | ~86.4% | 63.7% | -22.7% |

MMLU-Pro reduces accuracy by 16-33% compared to MMLU on average, but significantly improves discriminative power between models.

## Example Questions

### Math Category
```
Question: Let f be a continuous function on [0,1] such that f(0) = 0 and f(1) = 1.
Which of the following must be true?
A) f(0.5) = 0.5
B) f attains every value between 0 and 1
C) f is differentiable on (0,1)
D) f'(x) exists for all x in [0,1]
E) f is monotonically increasing
F) f has a local maximum
G) f is bounded above by 1
H) f is constant
I) f(x) > 0 for all x > 0
J) f has at most one fixed point
Answer: B
```

### Law Category
```
Question: Under the Fourth Amendment, which of the following searches would most likely
be considered unreasonable without a warrant?
A) Search of a vehicle during a lawful traffic stop
B) Search of a home without exigent circumstances
C) Search of items in plain view during a lawful arrest
D) Stop and frisk based on reasonable suspicion
E) Search of luggage at an international border
F) Search of a student's locker by school officials
G) Search of business records with a subpoena
H) Search of a passenger on a public bus
I) Search of a cell phone during booking
J) Search of a rented apartment with landlord consent
Answer: B
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|---------|-------------|------|
| MMLU | Original version, four options, 57 subjects | [MMLU.md](MMLU.md) |
| MMLU-Redux | Corrects annotation errors in original MMLU | https://huggingface.co/datasets/edinburgh-dawg/mmlu-redux |
| MMMLU | Multilingual version, covering 14 languages | [MMMLU.md](MMMLU.md) |
| C-Eval | Chinese version, 52 subjects | [C-Eval.md](C-Eval.md) |

## Limitations and Controversies

1. **Subject consolidation loses detail**: Merging 57 subjects into 14 categories obscures some fine-grained subject differences
2. **Data contamination risk**: Although some questions were updated, the public dataset may still be included in training corpora
3. **Ten options increase reasoning burden**: More options mean models need stronger elimination abilities, but this may also introduce more confusing distractors
4. **Only evaluates multiple choice**: Same as MMLU, does not reflect open-ended Q&A, long text generation, and other capabilities
5. **English-centric**: Original version is English only; needs MMMLU for multilingual evaluation
6. **Unclear CoT effects**: CoT impact varies significantly across subjects, with math/physics benefiting substantially while law/history see limited improvement

## Data Sources / References

- Wang, Y., Ma, X., Chen, W. et al. "MMLU-Pro: A More Robust and Challenging Multi-Task Language Understanding Benchmark." NeurIPS 2024. https://arxiv.org/abs/2406.01574
- MMLU-Pro GitHub: https://github.com/tiger-ai-lab/mmlu-pro
- HuggingFace dataset: https://huggingface.co/datasets/TIGER-Lab/MMLU-Pro
- PricePerToken MMLU-Pro Leaderboard: https://pricepertoken.com/leaderboards/benchmark/mmlu-pro
- BenchLM MMLU-Pro: https://benchlm.ai/benchmarks/mmluPro