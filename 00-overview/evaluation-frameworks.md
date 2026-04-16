# Evaluation Frameworks and Tools

## Mainstream Evaluation Frameworks

### 1. EleutherAI lm-evaluation-harness

- **Repository**: https://github.com/EleutherAI/lm-evaluation-harness
- **Status**: Industry-standard open-source LLM evaluation framework
- **Supported Benchmarks**: 60+ (MMLU, HellaSwag, GSM8K, ARC, BBH, TruthfulQA, etc.)
- **Features**: Unified evaluation protocol, supports few-shot/zero-shot, community-driven
- **Usage**:
```bash
pip install lm-eval
lm_eval --model hf --model_args pretrained=meta-llama/Llama-3-8B --tasks mmlu,hellaswag,gsm8k
```

### 2. HELM (Holistic Evaluation of Language Models)

- **Website**: https://crfm.stanford.edu/helm/
- **Institution**: Stanford CRFM
- **Features**: Comprehensive coverage, including scenarios, adapters, and metrics layers
- **Coverage Dimensions**: Accuracy, calibration, robustness, fairness, bias, toxicity, efficiency

### 3. DeepEval

- **Website**: https://deepeval.com
- **Features**: Integrated benchmark evaluation and custom metrics
- **Supports**: MMLU, GSM8K, HumanEval, TruthfulQA, HellaSwag, BBH
- **Code Example**:
```python
from deepeval.benchmarks import MMLU, GSM8K
benchmark = MMLU(tasks=[...], n_shots=3)
benchmark.evaluate(model=my_model)
```

### 4. rLLM

- **Website**: https://docs.rllm-project.com
- **Features**: 50+ benchmark datasets, automatic pulling and evaluation
- **Coverage**: Math, code, multiple choice, Q&A, long context, multimodal

### 5. Scale AI Leaderboards

- **Website**: https://scale.com/leaderboard
- **Features**: Provides private evaluation sets to prevent data contamination
- **Primary Benchmarks**: HLE, Chatbot Arena

### 6. Chatbot Arena (LMSYS)

- **Website**: https://chat.lmsys.org
- **Features**: Elo rating-based human preference evaluation
- **Coverage**: Text, code, vision, long context
- **Rating**: Based on 5 million+ real user comparisons

## Evaluation Tool Comparison

| Framework | Open Source | Benchmark Count | Ease of Use | Anti-Contamination | Community Activity |
|-----------|------------|-----------------|-------------|-------------------|-------------------|
| lm-eval-harness | Yes | 60+ | High | No | 5/5 |
| HELM | Yes | 40+ | Medium | No | 4/5 |
| DeepEval | Yes | 10+ | High | No | 4/5 |
| rLLM | Yes | 50+ | Medium | No | 3/5 |
| Scale AI | No | Few | High | Yes | 4/5 |
| Chatbot Arena | Semi-open | N/A | High | Yes | 5/5 |

## Key Evaluation Metrics

| Metric | Description | Applicable Scenarios |
|--------|-------------|---------------------|
| Accuracy | Accuracy rate, the most basic metric | Multiple choice, factual Q&A |
| Pass@k | Proportion of at least one pass in k samples | Code generation (HumanEval) |
| Exact Match | Exact match rate | Math problems (GSM8K, MATH) |
| F1 Score | Harmonic mean of precision and recall | Q&A, information extraction |
| Elo Rating | Comparison-based dynamic rating | Chatbot Arena |
| BLEU/ROUGE | Overlap between generated text and reference | Translation, summarization |
| Brier Score | Calibration error | Model confidence assessment |