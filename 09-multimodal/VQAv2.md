# VQAv2 — Visual Question Answering Standard Benchmark

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | Visual Question Answering v2 (VQAv2) |
| Creator | Georgia Tech / Virginia Tech / Microsoft |
| Release Year | 2017 |
| Number of Questions | ~1.1M questions (265K images) |
| Question Type | Open-ended QA + multiple-choice variant |
| Dataset Link | https://huggingface.co/datasets/vqav2 |
| Paper Link | https://arxiv.org/abs/1612.00837 |
| Status | ⚠️ Top models approaching saturation |

## Overview

VQAv2 is the most classic and widely used benchmark dataset in visual question answering, published at CVPR 2017. Its core contribution is significantly alleviating the severe language bias problem in VQAv1 through **balanced pairs** design — in VQAv1, models could achieve high accuracy relying solely on language priors (e.g., always answering "tennis" to "What sport is being played?") without truly understanding image content.

VQAv2 collects multiple **complementary images that produce different answers** for each question, forcing models to observe the image to answer correctly rather than relying on statistical patterns in the question text.

## Dataset Composition

### Core Statistics

| Item | Value |
|------|------|
| Total images | 265,016 (COCO real images + abstract scenes) |
| Total questions | ~1.1M |
| Average questions per image | 5.4 (minimum 3) |
| Annotated answers per question | 10 |
| Plausible wrong answers per question | 3 (seemingly reasonable incorrect answers) |
| Answer vocabulary | ~3,129 candidate answers |

### Balanced Pairs Design

VQAv2's key innovation:

- For each question, multiple complementary images with **different answers** are paired
- For example: "What color are the bananas?" is paired with both yellow banana and green banana images
- Forces models to truly analyze image content rather than relying on language priors
- Significantly reduces the effectiveness of text-only guessing

### Data Splits

| Split | Purpose | Annotation Visibility |
|------|------|------------|
| train | Training | Public |
| val | Validation | Public |
| test-dev | Debugging | Maximum 10 submissions per day |
| test-standard | Default evaluation | Hidden |
| test-challenge | Competition | Hidden |
| test-reserve | Anti-overfitting | Hidden |

### Question Type Distribution

VQAv2 questions are divided into three categories by answer type:

1. **Yes/No**: Judgment questions
2. **Number**: Numerical answers
3. **Other**: Open-ended descriptive answers (largest category)

## Evaluation Method

### Evaluation Metric: "Choose 3 from 10" Soft Accuracy

$$\text{Accuracy} = \min\left(\frac{\text{number of annotators giving the same answer}}{3},\, 1\right)$$

- If ≥3 annotators give the same answer, that answer receives full score 1.0
- If 1-2 annotators agree, partial credit is given
- This metric accounts for the inherent ambiguity of open-ended answers

### Answer Preprocessing Rules

- Convert all text to lowercase
- Remove punctuation
- Remove articles (a, an, the)
- Normalize numbers (e.g., convert digits to English words)

### Evaluation Server

- Hosted on EvalAI (https://evalai.cloudcv.org/)
- Submission format is JSON (containing question_id and predicted answer)
- Results are reported separately for Yes/No, Number, and Other categories

## Model Performance (April 2026)

VQAv2 has become a near-saturated benchmark, with top models performing near human level (~83.3%):

| Model | VQAv2 test-std | Notes |
|------|----------------|------|
| Human performance | ~83.3% | Reference upper bound |
| GPT-4o | ~80%^1 | Closed-source model |
| Gemini 2.5 Pro | ~79%^1 | Closed-source model |
| Qwen2.5-VL-72B | ~72%^1 | Best open-source |
| InternVL2-76B | ~78%^1 | Open-source competitor |

> ^1 Values marked with ~ are approximate; different evaluation configurations may cause slight differences. See [VQA official evaluation server](http://www.visualqa.org/) and [Papers with Code](https://paperswithcode.com/sota/visual-question-answering-on-vqav2).

**Trend assessment**: VQAv2 is approaching saturation for top models, making it difficult to continue distinguishing fine-grained differences between models. Research focus has shifted toward more challenging VQA variants (such as OK-VQA, A-OKVQA, TextVQA, etc.) and multimodal reasoning benchmarks (such as MMMU, MMMU-Pro).

## Example Questions

### Open-Ended QA

```
[Image: A kitchen scene with someone cutting bananas]
Question: What color are the bananas?
Ground truth answers: yellow (7), green (2), ripe (1)
Accuracy for "yellow": min(7/3, 1) = 1.0

[Image: A supermarket scene with unripe green bananas on shelves]
Question: What color are the bananas?
Ground truth answers: green (8), yellow (1), unripe (1)
Accuracy for "green": min(8/3, 1) = 1.0
```

> The two questions above form a "balanced pair" — the same question paired with complementary images producing different answers, testing whether the model truly looks at the image.

### Multiple-Choice Variant

```
[Image: An indoor sports venue]
What sport is being played in this image?
A) Tennis  B) Basketball  C) Football  D) Baseball

Answer: B
```

## Variants and Related Benchmarks

| Variant | Description | Link |
|------|------|------|
| **VQAv1** | Original version, has severe language bias | https://visualqa.org |
| **OK-VQA** | Requires external knowledge (open-knowledge VQA) | https://okvqa.allenai.org |
| **A-OKVQA** | Augmented knowledge VQA with reasoning annotations | https://a-okvqa.github.io |
| **TextVQA** | Focuses on reading and understanding text in images | https://textvqa.org |
| **GQA** | Compositional reasoning visual QA | https://gqadataset.org |
| **VizWiz** | VQA from real questions by blind people | https://vizwiz.org |
| **MMMU** | Multi-discipline multimodal reasoning (university level) | See MMMU.md |
| **MMMU-Pro** | Enhanced MMMU, reduced language shortcuts | See MMMU-Pro.md |

## Limitations and Controversies

1. **Approaching saturation**: Top closed-source models have reached ~80%, approaching human level at 83.3%, with insufficient discriminative power
2. **Residual bias**: Balanced pairs reduce language bias, but reasoning questions are still underrepresented and detection-type questions are overrepresented
3. **Answer granularity**: Open-ended evaluation relies on string matching; synonymous answers may be judged incorrect (e.g., "couch" vs "sofa")
4. **Distribution shift**: COCO images lean toward everyday life scenes, lacking specialized domains (medical, scientific charts, etc.)
5. **Data contamination risk**: As the most commonly used VQA benchmark, training data leakage risk is relatively high

## Data Sources/References

- Goyal et al., "Making the V in VQA Matter: Elevating the Role of Image Understanding in Visual Question Answering", CVPR 2017 — https://arxiv.org/abs/1612.00837
- VQA official website — https://visualqa.org
- EvalAI evaluation server — https://evalai.cloudcv.org
- Salesforce LAVIS dataset documentation — https://github.com/salesforce/LAVIS/blob/main/dataset_card/vqav2.md