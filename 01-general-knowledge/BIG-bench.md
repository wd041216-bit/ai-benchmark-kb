# BIG-bench — Beyond the Imitation Game

## Basic Information

| Property | Value |
|----------|-------|
| Full Name | Beyond the Imitation Game Benchmark |
| Creator | Google and 400+ community contributors |
| Release Year | 2022 |
| Number of Tasks | 204 tasks |
| Question Type | Various (multiple choice, generation, scoring, etc.) |
| Dataset Link | https://huggingface.co/datasets/bigbench |
| Paper Link | https://arxiv.org/abs/2206.04615 |
| GitHub | https://github.com/google/BIG-bench |

## Evaluation Dimensions

Covers an extremely wide range of capabilities:

### Core Categories
1. **Logical Reasoning**: Logic puzzles, deductive reasoning, inductive reasoning
2. **Mathematics**: Arithmetic, algebra, number theory
3. **Language Understanding**: Grammar, semantics, pragmatics
4. **Commonsense**: Physical commonsense, social commonsense
5. **Knowledge**: Science, history, culture
6. **Creativity**: Generation, association
7. **Bias and Safety**: Social bias, ethical judgment

### BIG-bench Hard (BBH)
- 23 most challenging tasks selected from 204 tasks
- These are tasks where large models at the time performed below average human levels
- Has become an independent standard benchmark
- **Dataset Link**: https://huggingface.co/datasets/lukaemon/bbh

## 23 Hard Tasks in BBH

| Task Name | Description |
|-----------|-------------|
| boolean_expressions | Boolean expression evaluation |
| causal_judgement | Causal judgment |
| date_understanding | Date understanding |
| disambiguation_qa | Disambiguation Q&A |
| dyck_languages | Dyck languages (bracket matching) |
| formal_fallacies | Formal fallacy identification |
| geometric_shapes | Geometric shape reasoning |
| hyperbaton | Word order judgment |
| logical_deduction | Logical deduction |
| mathematical_induction | Mathematical induction |
| multistep_arithmetic | Multi-step arithmetic |
| navigate | Spatial navigation |
| object_counting | Object counting |
| penguins_in_a_table | Table reasoning |
| reasoning_about_colored_objects | Colored object reasoning |
| ruin_names | Name recognition |
| salient_translation_error_detection | Translation error detection |
| snarks | Sarcasm identification |
| sports_understanding | Sports understanding |
| temporal_sequences | Temporal sequence reasoning |
| tracking_shuffled_objects | Tracking shuffled objects |
| word_sorting | Word sorting |

## Example Questions

### Logical Deduction
```
The following paragraphs each describe a set of three objects arranged in a fixed order. The statements are logically consistent within each paragraph.
On a shelf, there are three books: a white book, a green book, and a blue book. The white book is to the left of the green book. The blue book is the rightmost.
Options:
A) The white book is the leftmost
B) The green book is the leftmost
C) The blue book is the leftmost
Answer: A
```

### Causal Judgment
```
How would a typical person answer the following question about cause and effect?
A military coup overthrew the government. The country's GDP decreased.
Options:
A) The coup caused the GDP decrease
B) The GDP decrease caused the coup
C) Neither caused the other
Answer: A
```

## Scoring Method

- Each task is scored independently
- BBH uses 3-shot prompting
- Primary metric: Average accuracy across tasks
- Comparison baselines: Human performance, random baseline

## Model Performance

| Model | BBH Accuracy |
|-------|-------------|
| GPT-4 | ~83% |
| Claude 3.5 Sonnet | ~80% |
| Gemini 1.5 Pro | ~75% |
| Llama 3 70B | ~70% |
| Random baseline | ~25-50% |

## Limitations

1. Uneven task quality (community contributions)
2. Some tasks are too niche
3. The BBH subset has become the more popular usage
4. Overlap with MMLU

## Use Cases

- **Google**: Widely used in Gemini technical reports
- **Meta**: Llama series reports some BBH scores
- **Academia**: Important reference for comprehensive reasoning capability evaluation