# BrowseComp — Browsing Competition Benchmark

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | BrowseComp: A Benchmark for Browsing Agents |
| Creators | OpenAI (Jason Wei, Zhiqing Sun et al.) |
| Year Published | April 2025 |
| Number of Questions | 1,266 |
| Task Type | Web browsing retrieval-style Q&A (answers hard to find but easy to verify) |
| Dataset Link | https://github.com/openai/simple-evals |
| Paper Link | https://cdn.openai.com/pdf/5e10f4ab-d6f7-442e-9508-59515c65e35d/browsecomp.pdf |
| Status | 🔥 Most important agent benchmark of 2025, top models still < 50% (excluding Deep Research) |

## Overview

BrowseComp is an evaluation benchmark released by OpenAI in April 2025, specifically designed to test AI agents' ability to find hard-to-retrieve information by **browsing the internet**. Its core philosophy is **"easy to verify, hard to solve"** — once the answer is found, it is easy to confirm as correct, but finding the answer requires creativity, persistence, and complex search strategies.

BrowseComp fills a critical gap in AI evaluation: traditional Q&A benchmarks (such as TriviaQA, SimpleQA) test easily retrievable knowledge, while BrowseComp specifically tests information that requires **browsing tens to hundreds of web pages** and **trying multiple search strategies** to find.

### Core Design Principles

1. **Inverse Question Design**: Starting from known facts, construct questions that are difficult to find answers for through simple searches
2. **Asymmetric Verification**: Answers are easy to verify but hard to find
3. **Resistance to Simple Searches**: Five simple Google searches cannot find the answer on the first page
4. **Resistance to Model Solutions**: GPT-4o (with browsing), o1, and early Deep Research all fail to answer

### Quality Control (Triple Verification)

1. **Model-Unsolvable**: Trainers verified that GPT-4o (with/without browsing), o1, and early Deep Research all fail to answer
2. **Not Simple Search**: Five simple Google searches did not find the answer on the first page of results
3. **Human Difficulty**: Another trainer could not solve it within 10 minutes

## Dataset Composition

### Topic Distribution

| Topic | Percentage |
|-------|-----------|
| TV & Film | 16.2% |
| Other | 15.6% |
| Science & Technology | 13.7% |
| Arts | 10.0% |
| History | 9.9% |
| Sports | 9.7% |
| Music | 9.2% |
| Video Games | 5.6% |
| Geography | 5.5% |
| Politics | 4.7% |

### Human Performance

| Metric | Result |
|--------|--------|
| Total questions attempted | 1,255 |
| Human give-up rate (after ~2 hours) | 70.8% (888/1,255) |
| Human solve rate | 29.2% (367/1,255) |
| Answer match rate among solved | 86.4% (317/367) |

> Even experienced human trainers chose to give up on approximately 70% of questions after 2 hours.

## Evaluation Method

- **Exact Match**: The answer must be exactly correct
- **Automated Scoring**: Uses LLM to judge whether answers are equivalent
- **Single Attempt vs Multiple Attempts**: Supports Pass@1 and Best-of-N evaluation
- **Inference Time Scaling**: Allows more browsing time and computational resources to observe performance improvements

### Aggregation Strategies (64 Samples)

| Strategy | Improvement over single attempt |
|----------|-------------------------------|
| Majority Vote | ~15% |
| Weighted Vote | ~20% |
| Best-of-N | ~25% (highest) |

## Model Performance (April 2026)

### OpenAI Initial Evaluation (April 2025)

| Model | Accuracy | Notes |
|-------|----------|-------|
| Deep Research | 51.5% | Specifically trained for browsing tasks |
| o1 | 9.9% | No browsing capability |
| GPT-4.5 | 0.9% | No browsing capability |
| GPT-4o + Browsing | 1.9% | Browsing alone is not enough |
| GPT-4o | 0.6% | Baseline |

### Latest Leaderboard (April 2026)

| Model | BrowseComp | Notes |
|-------|-----------|-------|
| Gemini 3.1 Pro Preview | ~85.9% | Current highest score |
| Claude Opus 4.6 | ~84.0% | |
| GPT-5.2 | ~77.9% | |
| Claude Opus 4.5 / Sonnet 4.6 | ~75-78% | |
| Kimi K2 (Moonshot AI) | ~60.2% | |
| Gemini 3 Pro | ~59.2% | |
| o3 | ~49.7% | |
| Deep Research (original) | ~51.5% | April 2025 data |

> Note: Progress on BrowseComp has been remarkable — from GPT-4o's 0.6% to Gemini 3.1 Pro's 85.9% in just one year. This is primarily due to improvements in reasoning capability and search strategies, not data contamination.

## Example Questions

### TV & Film
```
Identify a fictional character who occasionally breaks the fourth wall, whose backstory involves
the help of a selfless ascetic, is known for humor, and whose TV show aired in the 1960s-1980s
with fewer than 50 episodes.

Answer: Plastic Man
```

### Scientific Papers
```
Among papers published at EMNLP 2018-2023, which paper has a first author who did their
undergraduate at Dartmouth College and a fourth author who did their undergraduate at the
University of Pennsylvania?

Answer: Frequency Effects on Syntactic Rule Learning in Transformers (EMNLP 2021)
```

### Key Characteristics
- The answers to these questions are easy to verify once found
- But finding the answers requires multiple searches, cross-verification, and creative search strategies
- Simple Google searches are almost impossible to find the answers

## Variants and Related Benchmarks

### BrowseComp Long Context
- 128K and 256K context versions
- Tests whether long context windows assist browsing retrieval

### BrowseComp-VL
- Vision-language version
- Combines image understanding and browsing capabilities

### BrowseComp-zh
- Chinese web version
- 289 multi-hop Chinese questions, covering 11 domains

### GAIA
- Also tests tool use + information retrieval
- But GAIA includes multimodal tasks such as file processing
- **Separate file**: See `GAIA.md`

### SimpleQA
- OpenAI's simple Q&A benchmark
- Complementary to BrowseComp — SimpleQA tests knowledge retrieval, BrowseComp tests deep browsing

## Why BrowseComp Is the Most Important Agent Benchmark of 2025

1. **Fills a Critical Gap**: Specifically tests deep browsing and persistent search capabilities
2. **Extreme Differentiation**: Ordinary models < 5%, top reasoning models < 50% (at initial release)
3. **Real-World Value**: Reflects AI's practical value in research and information retrieval
4. **Reasoning + Search Combination**: Proves that browsing alone or reasoning alone is insufficient; both must be combined
5. **Widely Adopted**: Since April 2025, nearly all major model evaluations include BrowseComp
6. **Rapid Progress**: From 0.6% to 85% in one year, demonstrating the huge potential of inference-time scaling

## Limitations and Controversies

1. **Answer Uniqueness**: Some questions may have multiple valid answers
2. **Time Sensitivity**: Relies on internet information; answers may change over time
3. **Search Engine Dependence**: Performance may be affected by search engine quality
4. **Insufficient Chinese Coverage**: Original version is English-only; BrowseComp-zh is still relatively new
5. **Data Contamination Risk**: Questions and answers are publicly available; subsequent models may answer through memorization
6. **Human Baseline Controversy**: Whether a 2-hour time limit is reasonable is debatable; some questions may only need more time

## Data Sources / References

- BrowseComp paper: https://cdn.openai.com/pdf/5e10f4ab-d6f7-442e-9508-59515c65e35d/browsecomp.pdf
- OpenAI announcement: https://openai.com/index/browsecomp
- Evaluation code: https://github.com/openai/simple-evals
- BrowseComp leaderboard: https://llm-stats.com/benchmarks/browsecomp
- BrowseComp analysis: https://airank.dev/benchmarks/browsecomp