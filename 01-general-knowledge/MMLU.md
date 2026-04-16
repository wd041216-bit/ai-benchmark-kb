# MMLU — Massive Multitask Language Understanding

## Basic Information

| Property | Value |
|----------|-------|
| Full Name | Massive Multitask Language Understanding |
| Creator | Dan Hendrycks et al. (UC Berkeley) |
| Release Year | 2021 |
| Number of Questions | 15,908 (57 subjects) |
| Question Type | Four-option multiple choice |
| Dataset Link | https://huggingface.co/datasets/cais/mmlu |
| Paper Link | https://arxiv.org/abs/2009.03300 |
| GitHub | https://github.com/hendrycks/test |
| Status | Approaching saturation (top models > 90%) |

## Evaluation Dimensions

Covering 57 subjects, divided into four major categories:

### STEM (Science, Technology, Engineering, Mathematics)
- Mathematics: Elementary Math, High School Mathematics, Abstract Algebra, College Mathematics
- Physics: High School Physics, College Physics, Conceptual Physics
- Computer Science: High School Computer Science, College Computer Science, Computer Security, Machine Learning
- Biology: High School Biology, College Biology, Anatomy, Virology
- Chemistry: High School Chemistry, College Chemistry

### Humanities
- History: High School European History, High School US History, High School World History, Prehistory
- Philosophy: Philosophy, Moral Disputes, Moral Scenarios, Logical Fallacies, Formal Logic
- Language: World Religions

### Social Sciences
- Politics: High School Government and Politics, US Foreign Policy, Security Studies
- Economics: High School Microeconomics, High School Macroeconomics, Econometrics
- Psychology: High School Psychology, Professional Psychology, Human Aging, Human Sexuality
- Sociology, Marketing, Public Relations, Management

### Other Professional Fields
- Law: Jurisprudence, Professional Law, International Law
- Medicine: Clinical Knowledge, Professional Medicine, Medical Genetics, Nutrition
- Accounting: Professional Accounting, Business Ethics
- Engineering: Electrical Engineering

## Example Questions

### Math Category
```
Question: If f(x) = x^2 + 3x + 2, then f(x+1) =
A) x^2 + 5x + 6
B) x^2 + 5x + 4
C) x^2 + 3x + 6
D) x^2 + 3x + 4
Answer: A
```

### Law Category
```
Question: Which of the following is a necessary element for a valid contract?
A) Written documentation
B) Consideration
C) Notarization
D) Witness signatures
Answer: B
```

### Computer Science Category
```
Question: What is the worst-case time complexity of quicksort?
A) O(n)
B) O(n log n)
C) O(n^2)
D) O(2^n)
Answer: C
```

## Scoring Method

- **Primary metric**: Accuracy
- **Scoring method**: Percentage of correct answers out of total questions
- **Few-shot setting**: Typically uses 5-shot
- **Random baseline**: 25% (four options)

## Model Performance (April 2026)

| Model | 5-shot Accuracy |
|-------|----------------|
| GPT-5 | 94.2% |
| Claude Opus 4.6 | ~93% |
| Gemini 3 Pro | ~92% |
| DeepSeek V3 | ~88% |
| Llama 4 Maverick | ~88% |
| GPT-4 (2023) | ~86% |
| Human experts | ~88% |

## Variants

### MMLU-Pro
- **Creator**: TIGER Lab (Berkeley)
- **Features**: 10 options instead of 4, more difficult questions
- **Number of questions**: ~12,000
- **Link**: https://huggingface.co/datasets/TIGER-Lab/MMLU-Pro

### MMLU-Redux
- **Creator**: Edinburgh University
- **Features**: Corrects annotation errors in original MMLU
- **Number of questions**: ~3,000 (subset)
- **Link**: https://huggingface.co/datasets/edinburgh-dawg/mmlu-redux

### MMMLU (Multilingual MMLU)
- **Creator**: OpenAI
- **Features**: Covers 14 languages
- **Link**: https://huggingface.co/datasets/openai/MMMLU

### C-Eval
- **Creator**: Shanghai Jiao Tong University
- **Features**: Chinese version of MMLU, 52 subjects
- **Link**: https://huggingface.co/datasets/ceval/ceval-exam

## Limitations

1. **Saturation issue**: Top models have reached 94%+ by 2026, discriminative power declining
2. **Data contamination**: Questions may appear in training data
3. **Only evaluates multiple choice**: Does not reflect open-ended Q&A capabilities
4. **English-centric**: Original version is English only (MMMLU partially addresses this)
5. **Insufficient depth**: Four options cannot evaluate deep reasoning

## Usage in Company Technical Reports

- **OpenAI**: GPT-4, GPT-4o, o1, o3, GPT-5 series all report MMLU scores
- **Anthropic**: Claude 3, 3.5, 4 series all use it
- **Google**: Gemini 1.0/1.5/2.0/3.0 series all use it
- **Meta**: Llama 1/2/3/4 series all use it
- **Mistral**: Mistral 7B/8x7B/Large series all use it
- **DeepSeek**: V2/V3/R1 series all use it