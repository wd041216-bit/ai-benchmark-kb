# WebArena — Real Web Environment Agent Evaluation

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | WebArena: A Realistic Web Environment for Building Autonomous Agents |
| Creators | CMU, Inspired Cognition (Shunyu Yao et al.) |
| Year Published | 2023 (arXiv), 2024 (ICLR 2024) |
| Number of Questions | 812 |
| Task Type | Real web interaction tasks (information retrieval, navigation, content creation) |
| Project Page | https://webarena.dev/ |
| Paper Link | https://arxiv.org/abs/2307.13854 |
| GitHub | https://github.com/web-arena-x/webarena |
| Status | ✅ Approaching saturation (top models ~68%), harder variants being developed |

## Overview

WebArena is the first **fully self-hosted, reproducible** web agent evaluation benchmark, containing 812 long-horizon web interaction tasks. It uses real websites built with open-source software (Magento e-commerce, Postmill forum, GitLab development platform, etc.) rather than relying on public websites, ensuring evaluation reproducibility and consistency.

Core innovations:
1. **Real Web Environments**: Fully functional websites built on open-source software, not simulations
2. **Self-Hosted and Reproducible**: Docker deployment, no public internet access needed, no CAPTCHAs or content drift
3. **Multi-Tab Support**: The first web agent benchmark to support cross-site multi-tab browsing
4. **Functional Correctness Evaluation**: Verifies task completion results rather than action sequences, allowing multiple valid paths

## Dataset Composition

### Website Environments

| Website | Base Software | Purpose |
|---------|--------------|---------|
| OneStopShop | Magento (e-commerce) | Shopping, searching products, placing orders |
| Reddit Clone | Postmill (forum) | Browsing posts, posting, commenting |
| GitLab | GitLab CE (development) | Code repositories, issue management, merge requests |
| CMS | Admin backend | Content management, configuration |
| OpenStreetMap | — | Map queries |
| Calculator | — | Calculation tool |
| Scratchpad | — | Notepad |
| Wikipedia | — | Knowledge queries |

### Task Type Distribution

| Type | Percentage | Example |
|------|-----------|---------|
| Information Seeking | ~35% | "When was the last time I bought shampoo?" |
| Site Navigation | ~35% | "Show me the highest-rated office chair" |
| Content & Configuration | ~30% | "Post asking 'Do you need a car in NYC?'" |

### Impossible Tasks

WebArena includes **deliberately designed impossible tasks**, testing whether agents can recognize that a task cannot be completed rather than hallucinating an answer.

## Evaluation Method

- **Functional Correctness**: Verifies whether the final result meets the task requirements
- **End-to-End Evaluation**: Does not check action sequences, only checks the final state
- **Multi-Path Tolerance**: Allows multiple valid paths to achieve the same result
- **Programmatic Verification**: Uses deterministic evaluation scripts rather than LLM-as-judge

### Input Formats

| Format | Description |
|--------|-------------|
| HTML | Web page HTML source code |
| Accessibility Tree | Structured representation of UI elements |
| Screenshot | Web page screenshot |

## Model Performance (April 2026)

### Original Baseline (2023)

| Model | Success Rate |
|-------|-------------|
| GPT-4 + CoT | 14.41% |
| GPT-4 | 11.70% |
| GPT-3.5 + CoT | 8.75% |
| Humans | 78.24% |

### Current Leaderboard (April 2026)

| Model | WebArena | Notes |
|-------|----------|-------|
| Claude Mythos Preview | ~68.7% | |
| GPT-5.4 Pro | ~65.8% | |
| Claude Opus 4.6 | ~64.5% | |
| Claude Sonnet 4.6 | ~59.2% | |
| Gemini 3.1 Pro | ~58.4% | |
| Gemini 3 Pro | ~52.1% | |
| DeepSeek V3.2 Thinking | ~48.6% | |
| Llama 4 Behemoth | ~46.2% | |
| Humans | 78.24% | Original baseline |

> Note: WebArena is approaching saturation; top models have improved from 14% in 2023 to ~68% in 2026, but there is still ~10 percentage points of room for improvement to reach the human baseline.

## Example Tasks

### Information Retrieval
```
Task: Find all closed Issues with "memory leak" in the title in project X on GitLab,
     return the number of the most recent one.

Evaluation: Check whether the returned Issue number is correct.
```

### Site Navigation
```
Task: Find the highest-rated wireless mouse under $50 on the e-commerce site,
     add it to the cart and take a screenshot.

Evaluation: Check whether the cart contains the correct product.
```

### Content Creation
```
Task: Create a new post on the forum titled "NYC Travel Advice",
     with the body asking "Do you need a car in NYC?",
     then create a corresponding Issue on GitLab to record this discussion.

Evaluation: Check whether the post title/content and GitLab Issue match.
```

### Impossible Task
```
Task: Find a laptop priced at $0.01 on the e-commerce site.

Evaluation: The agent should recognize the task is impossible and explain why,
      rather than hallucinating a non-existent product.
```

## Variants and Related Benchmarks

### WebArena-Verified (ServiceNow, December 2025)
- Manually reviewed and corrected all 812 tasks
- Removed LLM-as-judge evaluation, replaced with deterministic scoring
- Added "Hard" subset (258 questions) for efficient evaluation
- PyPI install: `pip install webarena-verified`
- **GitHub**: https://github.com/ServiceNow/webarena-verified

### VisualWebArena
- Visual version of WebArena
- More focused on visual understanding and image manipulation
- **Paper**: https://arxiv.org/abs/2306.06694

### WebChoreArena (June 2025)
- Harder extended benchmark
- 532 tasks, focused on memory, computation, and long-horizon operations
- Even models that perform well on WebArena (e.g., Gemini 2.5 Pro 54.8%) only achieve 37.8% on WebChoreArena
- **Paper**: https://arxiv.org/abs/2506.01952

### BrowserGym
- WebArena's browser agent ecosystem
- Provides a unified agent framework
- **GitHub**: https://github.com/ServiceNow/BrowserGym

### OSWorld
- Tests desktop OS operations (not limited to web)
- **Separate file**: See `OSWorld.md`

## Why WebArena Is Important

1. **Real and Reproducible**: Self-hosted environment, no CAPTCHAs or content drift
2. **Industry Standard**: De facto standard for web agent evaluation, widely cited
3. **Functional Evaluation**: Based on outcomes rather than action sequences, allowing multiple valid paths
4. **Multi-Tab**: First benchmark to support cross-site multi-tab browsing
5. **Impossible Tasks**: Tests agents' ability to recognize impossible tasks
6. **Rapid Progress Indicator**: Progress from 14% to 68% clearly demonstrates the leap in agent capabilities

## Limitations and Controversies

1. **Approaching Saturation**: Top models have reached ~68%, and discrimination is declining
2. **Limited Website Scope**: Only 4-5 websites, not covering all web types
3. **Evaluation Cost**: Requires complete Docker environment deployment
4. **Environment Stability**: Docker environments occasionally experience state inconsistencies
5. **Language Limitation**: Only English environments
6. **LLM-as-judge Issues**: The original version used LLM evaluation for some tasks; WebArena-Verified has fixed this
7. **Benchmark Optimization Risk**: Models may be over-optimized for the WebArena environment

## Data Sources / References

- WebArena paper (ICLR 2024): https://arxiv.org/abs/2307.13854
- Project page: https://webarena.dev/
- GitHub: https://github.com/web-arena-x/webarena
- WebArena-Verified: https://github.com/ServiceNow/webarena-verified
- WebChoreArena: https://arxiv.org/abs/2506.01952
- VisualWebArena: https://arxiv.org/abs/2306.06694
- BenchLM leaderboard: https://benchlm.ai/benchmarks/webArena
- Steel leaderboard: https://leaderboard.steel.dev/registry/benchmarks/webarena/