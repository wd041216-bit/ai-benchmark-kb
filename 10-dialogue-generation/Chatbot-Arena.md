# Chatbot Arena — Chatbot Arena

## Basic Information

| Attribute | Value |
|------|-----|
| Full Name | LMSYS Chatbot Arena (now LMArena) |
| Creator | LMSYS Org (UC Berkeley, UCSD, CMU) |
| Release Year | 2023 |
| Evaluation Method | Human preference comparison (Elo Rating / Bradley-Terry model) |
| Website Link | https://chat.lmsys.org (now https://arena.ai) |
| Paper Link | https://arxiv.org/abs/2403.04132 |
| GitHub | https://github.com/lmarena/arena-hard-auto |
| Status | ✅ Most trusted LLM evaluation standard |

## Overview

Chatbot Arena is currently the most widely recognized LLM evaluation platform in the industry. Users input a prompt, two anonymous models respond simultaneously, and users vote for the better response. The system calculates model rankings based on millions of real user comparison votes. As of April 2026, it has accumulated over 5 million human preference comparisons, covering 100+ models.

## Core Mechanisms

### Elo Rating System

Chatbot Arena's scoring has evolved from classic Elo to the Bradley-Terry model:

#### First Generation: Online Elo (at launch in 2023)

| Parameter | Value |
|------|-----|
| Initial rating | 1000 |
| K factor | 4 |
| Base | 10 |
| Scale | 400 |

Rating update formula: `rating[model_a] += K * (sa - ea)`, where `ea = 1 / (1 + 10^((rb - ra) / 400))`.

This method is similar to chess Elo but has instability — ratings favor recent matches, and match order can affect results.

#### Second Generation: Bradley-Terry Model (late 2023 to present)

- Uses maximum likelihood estimation (MLE), equivalent to logistic regression's binary cross-entropy loss
- Probability of model B beating model A: P(B beats A) = σ(x^T θ*)
- Ratings undergo linear transformation (multiplied by 400 then added 1000) so the numerical range is consistent with chess Elo
- Provides bootstrap confidence intervals for more stable ratings

#### Third Generation: Extended Bradley-Terry (2024)

- Introduces regularized logistic regression: θ̂ = argmin Σ ℓ(σ(X_i^T θ), Y_i) + λ‖θ‖_p
- Supports joint ranking across multiple subsystems (models + tools + frameworks)
- Used for extended evaluations such as RedTeam Arena and Agent Arena

### Voting Process

1. User inputs a prompt
2. Two anonymous models respond simultaneously
3. User votes: A is better / B is better / Tie / Both are bad
4. System updates ratings based on results (Bradley-Terry model batch calculation)

### Evaluation Categories

| Category | Description |
|------|------|
| Overall | Comprehensive ranking |
| Coding | Programming ability |
| Math | Mathematical ability |
| Hard Prompts | Difficult prompts |
| Vision | Visual understanding |
| Long Context | Long context |
| Creative Writing | Creative writing |
| Instruction Following | Instruction following |

## April 2026 Rankings (Overall)

| Rank | Model | Elo Rating | Organization |
|------|------|---------|------|
| 1 | Claude Opus 4.6 Thinking | ~1504 | Anthropic |
| 2 | Claude Opus 4.6 | ~1500 | Anthropic |
| 3 | Gemini 3.1 Pro Preview | ~1493 | Google |
| 4 | Grok 4.20 Beta1 | ~1491 | xAI |
| 5 | Gemini 3 Pro | ~1486 | Google |
| 6 | GPT-5.4 High | ~1484 | OpenAI |
| 7 | Grok 4.20 Beta Reasoning | ~1483 | xAI |
| 8 | GPT-5.2 Chat Latest | ~1480 | OpenAI |
| 9 | Gemini 3 Flash | ~1475 | Google |
| 10 | Claude Opus 4.5 Thinking | ~1474 | Anthropic |

> Note: The above Elo ratings are approximate; actual scores are continuously updated with voting data. The top 6 models differ by only about 20 points, making competition extremely intense. Data source: [arena.ai](https://arena.ai/leaderboard), April 2026.

### Style Control Elo (Style-Controlled Rankings)

To control the impact of response length and format preferences on ratings, Arena also provides Style Control Elo:

| Rank | Model | Style Control Elo |
|------|------|-------------------|
| 1 | GPT-5.2 Pro | ~1402 |
| 2 | Claude Opus 4.6 | ~1398 |
| 3 | Gemini 3 Pro | ~1389 |
| 4 | GPT-5.2 | ~1380 |
| 5 | Grok 4 Heavy | ~1375 |

### Coding Rankings (April 2026)

| Rank | Model | Coding Elo |
|------|------|------------|
| 1 | Claude Opus 4.6 | ~1549 |
| 2 | Claude Opus 4.6 Thinking | ~1545 |
| 3 | Claude Sonnet 4.6 | ~1522 |
| 4 | Claude Opus 4.5 Thinking | ~1491 |
| 5 | Claude Opus 4.5 | ~1465 |

## Arena-Hard-Auto

Arena-Hard-Auto is the automated evaluation version of Chatbot Arena, using LLM judge models to replace human voting:

| Attribute | Value |
|------|-----|
| Current version | Arena-Hard-v2.0 (released April 2025) |
| Number of questions | 500 difficult prompts + 250 creative writing prompts |
| Judge model | GPT-4.1 / Gemini-2.5 (v2.0); GPT-4-Turbo (v0.1) |
| Baseline model | GPT-4-0314 (v0.1) |
| Scoring method | 5-level pairwise comparison + Bradley-Terry model |
| Correlation with human preference | 89.1% (v0.1) |
| Single model evaluation cost | ~$25 |
| Dataset | https://github.com/lmarena/arena-hard-auto |

### Key Technical Features

- **Position bias elimination**: Each question is compared twice (swapping model positions), for a total of 500×2 = 1000 judgments
- **Chain-of-Thought judging**: The judge model first outputs reasoning process then gives its verdict
- **Style Control**: Controls the impact of Markdown density and response length on scoring
- **BenchBuilder pipeline**: Screens high-quality prompts from 200K Arena user queries through BERTopic clustering and 7-dimension scoring

### Judge Model Comparison

| Judge Model | Agreement with Arena | Differentiability | Brier Score |
|----------|----------------|----------|-----------|
| GPT-4-Turbo | 89.1% | 87.4% | 0.07 |
| Claude-3-Opus | 66.7% | 83.7% | 0.17 |

## Related Benchmarks

### WildBench

- Developed by Allen AI
- Uses real user queries (from WildChat dataset)
- LLM-as-Judge scoring
- Correlation with Arena: Pearson 0.984 (Top-6 models)
- **See →** [WildBench.md](./WildBench.md)

### MixEval / MixEval-Hard

- Dynamic evaluation, automatically collecting questions from multiple sources
- MixEval-Hard correlation with Arena rankings reaches 0.96 (Spearman)
- Single model evaluation cost only $0.60
- **See →** [MixEval.md](./MixEval.md)

## Why Chatbot Arena Matters

1. **Closest to real-world usage**: Based on real user preferences, not artificially designed evaluation questions
2. **Contamination-proof**: Models cannot cheat through pre-training because questions come from real-time user input
3. **Continuously updated**: Real-time reflection of latest model performance; new models immediately join rankings upon launch
4. **Multi-dimensional**: Covers coding, math, creative writing, long context, and other subcategories
5. **Widely recognized**: All major AI companies cite Arena rankings
6. **Confidence intervals**: The Bradley-Terry model provides statistical confidence intervals, making results more reliable

## Limitations and Controversies

1. **Human preference bias**: Users may prefer verbose, confident, well-formatted responses rather than truly accurate ones
2. **Anonymity issues**: Model characteristics (such as specific phrasing styles) may reveal identity, affecting voting fairness
3. **Voting quality**: Non-expert users may not accurately judge the quality of complex technical questions
4. **Uneven coverage**: Programming and math questions are overrepresented; creative writing and professional domains are underrepresented
5. **Cannot evaluate offline**: Must run online, which is not ideal for large-scale internal evaluation
6. **Vote manipulation risk**: Research shows the Bradley-Terry model has an "omni-property" vulnerability — any new vote can affect all models' rankings, even those not involved in the target comparison
7. **Language bias**: English-dominant; evaluation coverage and reliability for other languages are lower
8. **Position bias**: Even with dual comparisons, position bias still exists in human voting

## Data Sources/References

- Chiang, W.L. et al. "Chatbot Arena: An Open Platform for Evaluating LLMs by Human Preference." arXiv:2403.04132, 2024. https://arxiv.org/abs/2403.04132
- Arena leaderboard: https://arena.ai/leaderboard
- Arena-Hard-Auto: https://github.com/lmarena/arena-hard-auto
- Extended Bradley-Terry model: https://arena.ai/blog/extended-arena/
- Vote manipulation research: Min, Y. et al. "Improving Your Model Ranking on Chatbot Arena by Vote Rigging." ICML 2025. https://arxiv.org/abs/2501.17858
- Arena Elo rating methodology: https://bryanyzhu.github.io/posts/2024-06-20-elo-part1