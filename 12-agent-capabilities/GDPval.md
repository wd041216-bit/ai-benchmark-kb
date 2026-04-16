# GDPval — GDP Validation Benchmark

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | GDPval: Measuring AI Performance on Economically Valuable Tasks |
| Creators | OpenAI |
| Year Published | September 2025 |
| Number of Questions | 1,320 (220 open-source gold-standard questions) |
| Task Type | Real-world professional tasks (documents, slides, charts, spreadsheets, etc.) |
| Official Website | https://gdpval.pro/ |
| Paper Link | https://arxiv.org/abs/2510.04374 |
| Leaderboard | https://gdpval.pro/gdpval-leaderboard |
| Status | ✅ Emerging standard for evaluating AI economic value, accepted at ICLR 2026 |

## Overview

GDPval is an evaluation benchmark released by OpenAI in September 2025, designed to measure AI models' performance on **real-world professional tasks with economic value**. Unlike traditional academic benchmarks, GDPval directly benchmarks against **professional work in major U.S. GDP-contributing industries**, covering 44 occupations across 9 major industries, with questions created and reviewed by industry experts with an average of 14 years of experience.

Core design philosophy:
1. **Economic Value Orientation**: Tasks are sourced from real, economically valuable work in industries
2. **Expert-Created and Reviewed**: Tasks created by industry experts and blind-reviewed by peer experts
3. **ELO Scoring**: Uses a chess-style ELO ranking system, determined through blind head-to-head comparisons
4. **Deliverable Evaluation**: Evaluates AI-generated actual deliverables (documents, PPTs, spreadsheets, etc.) rather than multiple-choice questions

## Dataset Composition

### Industry and Occupation Distribution

| Industry | Representative Occupations |
|----------|---------------------------|
| Real Estate | Real estate agents, appraisers |
| Manufacturing | Mechanical engineers, industrial designers |
| Government | Policy analysts, urban planners |
| Healthcare | Registered nurses, medical coders |
| Finance | Financial analysts, auditors |
| Retail | Purchasing managers, retail analysts |
| Wholesale | Supply chain managers, logistics analysts |
| Information Technology | Software developers, data analysts |
| Professional/Scientific Services | Lawyers, management consultants |

Covering **44 occupations** in total, approximately 30 tasks per occupation.

### Deliverable Types

| Type | Percentage | Description |
|------|-----------|-------------|
| Documents | ~35% | Reports, analysis documents, memoranda |
| Slides | ~20% | PPT presentations |
| Diagrams | ~15% | Flowcharts, architecture diagrams |
| Spreadsheets | ~20% | Data analysis spreadsheets, financial models |
| Multimedia | ~10% | Other format deliverables |

### Data Quality

- Task creators have an average of **14 years** of industry experience
- Each task undergoes an average of **5 rounds** of expert review
- 220 gold-standard tasks are fully open source

## Evaluation Method

### ELO Scoring System

GDPval uses an **ELO ranking system** (similar to chess), determining model rankings through **blind head-to-head comparisons**:

1. Industry experts blindly compare AI and human deliverables without knowing the source
2. They judge whether AI output is "better," "comparable," or "worse" than human expert output
3. Through numerous pairwise comparisons, each model's ELO score is calculated

### Scoring Dimensions

| Dimension | Description |
|-----------|-------------|
| Accuracy | Domain knowledge, calculations, factual correctness |
| Aesthetics | Formatting, slide design, visual presentation |
| Completeness | Whether all task requirements are met |
| Usefulness | Whether the output can be directly used in real work |

### Automated Scorer

OpenAI also provides an experimental AI scorer (evals.openai.com), with approximately 66% agreement rate with human experts (human inter-rater agreement is approximately 71%).

## Model Performance (April 2026)

### GDPval-AA ELO Leaderboard (Artificial Analysis Independent Ranking)

| Model | Organization | ELO Score | Release Date |
|-------|-------------|-----------|--------------|
| GPT-5.2 (xhigh) | OpenAI | ~1474 | December 2025 |
| Claude Opus 4.5 (Reasoning) | Anthropic | ~1410 | November 2025 |
| GPT-5 (high) | OpenAI | ~1303 | August 2025 |
| Claude 4.5 Sonnet (Reasoning) | Anthropic | ~1290 | September 2025 |
| GPT-5.1 (high) | OpenAI | ~1241 | November 2025 |
| DeepSeek V3.2 (Reasoning) | DeepSeek | ~1208 | December 2025 |
| Gemini 3 Pro Preview (high) | Google | ~1206 | November 2025 |

### Percentage Ranking (Another Tracking Source)

| Model | Percentage Score |
|-------|-----------------|
| Claude Sonnet 4.6 | ~81.7% |
| Claude Opus 4.6 | ~80.3% |
| GPT-5.2 | ~73.1% |

### Key Findings

1. **Claude Opus 4.1 Leads in Aesthetics**: Best performance in formatting and slide design
2. **GPT-5 Leads in Accuracy**: Stronger in domain knowledge and calculations
3. **Rate of Progress**: From GPT-4o (spring 2024) to GPT-5 (summer 2025), performance approximately doubled, showing a linear trend
4. **Speed and Cost**: Frontier models complete tasks approximately **100× faster and 100× cheaper** than industry experts

## Example Tasks

### Lawyer Task
```
Task: Draft a legal memorandum for a client regarding non-compete clauses in a commercial
lease agreement, covering California law's latest position on such clauses (2024 new regulations),
and providing summaries of three relevant cases.

Deliverable: Legal memorandum (Word document)
Review: Practicing attorneys blind-compare AI output vs. attorney-drafted version
```

### Financial Analyst Task
```
Task: Based on the provided quarterly financial data, create a financial forecast model with
three scenarios (optimistic, neutral, pessimistic) and a supporting PPT presentation.

Deliverable: Excel financial model + PPT presentation
Review: CFO-level financial analysts blind-evaluate
```

### Mechanical Engineer Task
```
Task: Create an engineering specification document with tolerance analysis for a custom part,
using 6061-T6 aluminum alloy, considering a 0.005-inch machining tolerance.

Deliverable: Engineering specification document (Word document + diagrams)
Review: Senior mechanical engineers blind-evaluate
```

## Variants and Related Benchmarks

### GDPval Gold Set
- 220 fully open-source tasks
- Can be used for independent evaluation and reproducibility
- **Link**: https://gdpval.pro/

### SWE-bench
- Tests code repair capabilities (a subset of the professional domain)
- **Separate file**: See `04-coding/SWE-bench.md`

### OSWorld
- Tests desktop operation capabilities
- More focused on operations rather than content creation
- **Separate file**: See `OSWorld.md`

## Why GDPval Is Important

1. **Economic Value Alignment**: Directly measures AI performance on economically valuable work
2. **Expert Review**: Reviewed by real industry experts, not self-constructed academic standards
3. **ELO Ranking**: Better reflects relative strengths between models than percentage scores
4. **Real Deliverables**: Evaluates complete documents, PPTs, and spreadsheets rather than multiple-choice answers
5. **Broad Coverage**: 44 occupations across 9 major GDP-contributing industries
6. **ICLR 2026 Acceptance**: Academic recognition is being established

## Limitations and Controversies

1. **One-Time Evaluation**: Does not reflect iterative/multi-draft workflows (real work often involves iteration)
2. **Knowledge Work Only**: Does not cover physical labor and on-site operational tasks
3. **Clear Task Specifications**: Real-world tasks are often ambiguous, requiring self-discovery and definition
4. **Small Sample Size**: Only 44 occupations × 30 tasks = 1,320 tasks
5. **High Review Cost**: Requires industry expert review; each evaluation round is expensive
6. **OpenAI Dominance**: Created and operated by OpenAI; independence is questioned
7. **ELO Volatility**: ELO scores change as new models are added, limiting historical comparability

## Data Sources / References

- GDPval paper: https://arxiv.org/abs/2510.04374
- Official website: https://gdpval.pro/
- Leaderboard: https://gdpval.pro/gdpval-leaderboard
- OpenAI announcement: https://openai.com/research/gdpval
- Automated scorer: https://evals.openai.com/
- Artificial Analysis independent ranking: https://airank.dev/benchmarks/gdpval-aa-elo