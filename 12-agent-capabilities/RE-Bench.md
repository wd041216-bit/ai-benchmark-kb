# RE-Bench — Frontier AI R&D Engineering Capability Evaluation

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | RE-Bench: Evaluating Frontier AI R&D Capabilities of Language Model Agents Against Human Experts |
| Creators | METR (Model Evaluation & Threat Research) |
| Year Published | 2024 |
| Number of Tasks | 7 R&D engineering environments |
| Task Type | Real ML R&D tasks (code optimization, model training, GPU kernel writing, etc.) |
| Dataset Link | https://github.com/METR/RE-Bench |
| Paper Link | https://arxiv.org/abs/2411.15114 |
| Status | ✅ Highly discriminative; humans still outperform AI with long time budgets |

## Overview

RE-Bench is an evaluation benchmark developed by METR, designed to measure AI agents' performance relative to human experts on **real AI/ML R&D engineering tasks**. Unlike other benchmarks, RE-Bench compares not only final results but also **output quality under the same time budget**, directly answering the key question: "Can AI replace human engineers?"

Core design principles:
- **Time-Equivalent Comparison**: AI and humans are compared on output quality under the same time budget
- **Real Engineering Tasks**: Not artificially constructed toy problems, but real ML optimization and R&D tasks
- **Continuous Scoring**: Tasks have continuous score curves rather than simple pass/fail
- **Multiple Time Budgets**: 2-hour, 8-hour, 32-hour comparisons, among others

## Dataset Composition

### 7 Evaluation Environments

| Environment | Task Description | Scoring Metric | Starting Score | Reference Score |
|-------------|-----------------|----------------|---------------|-----------------|
| Optimize LLM Foundry | Optimize fine-tuning script runtime | log(runtime) | 5.6 (272s) | 4.54 (94s) |
| Optimize a Kernel | Write Triton GPU kernel for prefix sum | log(runtime) | 1.56 (4.76ms) | 0.47 (1.6ms) |
| Fix Embedding | Restore performance of model with corrupted embeddings | log(loss-1.5) | 2.2 | 0.26 |
| Scaling Law Experiment | Predict optimal hyperparameters via scaling laws | Loss + prediction error | 0.24 | 0.84 |
| Restricted Architecture MLM | Build language model using only restricted PyTorch primitives | log(loss-1.5) | 1.81 | 1.13 |
| Finetune GPT-2 for QA | RL fine-tune GPT-2 as a chatbot | Win rate | 0.54 | 0.85 |
| Rust CodeContests Scaffolding | Build Rust programming scaffolding for GPT-3.5 | Solve percentage | 0.00 | 0.13 |

### Human Baseline

- **71 attempts** from **61 human experts**
- Including ML engineers, systems engineers, researchers, etc.
- Each expert invested between 2 and 32 hours

## Evaluation Method

1. **Time Budget Comparison**: Compare AI and human scores under the same time budget
2. **Continuous Scoring**: Each task has a continuous scoring function, not binary pass/fail
3. **Multi-Tier Evaluation**: 2 hours, 8 hours, 32 hours
4. **Automated Execution**: Runs in a sandbox environment, automatically collecting results

### Core Findings

| Time Budget | AI vs Human | Explanation |
|-------------|------------|-------------|
| 2 hours | AI ~4× human | AI generates and tests solutions >10× faster than humans |
| 8 hours | Humans slightly outperform AI | Human long-range planning advantage begins to emerge |
| 32 hours | Humans ~2× AI | Humans significantly lead on sustained engineering tasks |

## Model Performance (April 2026)

### RE-Bench Original Evaluation (November 2024)

| Model | 2-Hour Score | 8-Hour Score | Notes |
|-------|-------------|-------------|-------|
| o1-preview | ~4× human | Slightly below human | Surpassed all humans on GPU kernel optimization |
| Claude 3.5 Sonnet | ~4× human | Slightly below human | Stable performance on most tasks |
| Human median | Baseline | Baseline | Reached reference score at 32 hours |

### METR Autonomous Capability Evaluation (Time Horizon Metric, January 2026 Update)

| Model | 50% Time Horizon (TH1.1) | Confidence Interval |
|-------|--------------------------|-------------------|
| Claude Opus 4.5 | 320 minutes | [170, 729] |
| GPT-5 | 214 minutes | [117, 480] |
| o3 | 121 minutes | [74, 201] |
| Claude Sonnet 3.7 | 60 minutes | [32, 106] |

> Note: 50% time horizon refers to the task duration at which the model has a 50% probability of completion.

## Example Tasks

### Optimize a Kernel
```
Task: Write a Triton GPU kernel that implements an efficient prefix sum computation.
Scoring: Based on runtime, lower is better.
Starting code: A naive PyTorch implementation (4.76ms)
Target: Optimize to near-expert level (~1.6ms)
```

### Fix Embedding
```
Task: A language model's embedding layer has been corrupted, causing a significant
      performance drop. Restore model performance as close to the original level as possible.
Scoring: Based on the restored model loss, lower is better.
Constraint: Cannot access the original embedding matrix.
```

## Variants and Related Benchmarks

### METR Time Horizon
- Continuous evolution version of RE-Bench
- TH1.1 update released in January 2026
- Measures "how long a model can sustain autonomous work"
- **Link**: https://metr.org/

### τ-bench / τ²-bench
- Tests agent capabilities in multi-turn conversations
- Aviation, retail, telecom, and other scenarios
- **Separate file**: See `Tau2.md`

### SWE-bench
- Tests code repair capabilities (pure code, not R&D engineering)
- **Separate file**: See `04-coding/SWE-bench.md`

## Limitations and Controversies

1. **Small Number of Tasks**: Only 7 environments, limited statistical confidence
2. **Narrow Domain**: Only covers ML/systems engineering, not representative of all engineering capabilities
3. **Scaffold Differences**: METR uses its own Inspect scaffold, which may underestimate the actual capabilities of commercial products (like Claude Code)
4. **Wide Confidence Intervals**: Results at different time budgets have significant variance
5. **Limited Human Baseline**: Only 61 experts, with large individual differences
6. **Reward Hacking**: Some models have been found to exploit scoring function vulnerabilities rather than truly solving problems

## Data Sources / References

- RE-Bench paper: https://arxiv.org/abs/2411.15114
- METR blog: https://metr.org/blog/2024-11-22-evaluating-r-d-capabilities-of-llms/
- GitHub repository: https://github.com/METR/RE-Bench
- METR Time Horizon TH1.1: https://www.metr.org/blog/2026-1-29-time-horizon-1-1/
- METR Claude 3.7 evaluation: https://evaluations.metr.org/claude-3-7-report/
- METR o3/o4-mini evaluation: https://evaluations.metr.org/openai-o3-report/