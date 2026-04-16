# τ²-bench — Multi-Turn Conversational Agent Evaluation

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | τ²-bench (Tau-Squared Bench): A Benchmark for Tool-Agent-User Interaction |
| Creators | Sierra Research, Princeton (Shunyu Yao, Karthik Narasimhan et al.) |
| Year Published | 2024 (τ-bench), 2025 (τ²-bench), 2026 (τ³-bench) |
| Number of Questions | 269 (airline 43 + retail 112 + telecom 114) |
| Task Type | Multi-turn conversational agent tasks (policy compliance + tool calling) |
| GitHub | https://github.com/sierra-research/tau2-bench |
| Paper Link | https://arxiv.org/abs/2406.12045 (τ-bench), https://arxiv.org/abs/2506.07982 (τ²-bench) |
| Leaderboard | https://taubench.com |
| Status | ✅ High discrimination, one of the strictest agent evaluations |

## Overview

τ²-bench (pronounced "tau squared bench") is an evaluation benchmark for assessing conversational AI agents' performance in **multi-turn, domain-specific customer service scenarios**. Unlike benchmarks that only test function calling, τ²-bench requires agents to simultaneously achieve:

1. **Tool Use**: Correctly call APIs to complete tasks
2. **Policy Compliance**: Strictly adhere to company policy rules
3. **Dialogue Management**: Engage in natural multi-turn interactions with simulated users

The core innovation is the **dual-control environment**: both the agent and the simulated user have tools and control capabilities, simulating complex interaction scenarios in real customer service.

### Evolution History

| Version | Year | Core Innovation |
|---------|------|-----------------|
| τ-bench | 2024 | Initial version, airline and retail domains |
| τ²-bench | 2025 | Added dual-control environment, telecom domain, Pass@k metric |
| τ³-bench | 2026 | Added knowledge retrieval (RAG) domain, voice duplex evaluation |

## Dataset Composition

### Domain Distribution

| Domain | Number of Questions | Description |
|--------|-------------------|-------------|
| Airline | 43 | Flight booking, cancellation, fare rules |
| Retail | 112 | Returns, discount stacking, inventory queries |
| Telecom | 114 | Account management, plan changes |
| Banking Knowledge | Added in τ³ | Knowledge retrieval-type customer service |
| Mock | Small number | Simple test domain |

### Evaluation Modes

| Mode | Description |
|------|-------------|
| Text (half-duplex) | Traditional turn-based conversation |
| Voice (full-duplex) | Added in τ³, supports simultaneous speech and interruption |

## Evaluation Method

### Pass@k Metric

τ²-bench uses **Pass@k** as its core metric, measuring the probability that an agent succeeds at least once in k independent runs:

- **Pass@1**: Single-run success rate (strictest)
- **Pass@2**: Probability of succeeding at least once in two runs
- **Pass@5**: Probability of succeeding at least once in five runs

> Key insight: Small per-turn failure rates compound exponentially in multi-turn conversations. A 95% success rate per turn in a 10-turn conversation yields only about 60% overall.

### Policy Compliance Verification

The evaluation checks not only whether the task was completed, but also whether the agent **strictly adhered to company policies**:
- Cannot process refunds outside the policy window
- Whether discount stacking follows rules
- Whether unreasonable user requests are properly rejected

### Evaluation Dimensions

| Dimension | Description |
|-----------|-------------|
| Task Completion | Whether the user's request was correctly handled |
| Policy Compliance | Whether company rules were followed |
| Dialogue Fluency | Whether multi-turn interactions were natural |
| Robustness | Consistency of results across multiple runs |

## Model Performance (April 2026)

### τ²-bench Leaderboard

| Model | Retail Pass@1 | Telecom Pass@1 | Overall |
|-------|--------------|----------------|---------|
| Claude Opus 4.6 | 91.9% | 99.3% | ~95% |
| Claude Opus 4.5 | 88.9% | 98.2% | ~93% |
| GPT-5.2 Thinking | 82.0% | 98.7% | ~90% |
| Gemini 3.1 Pro | ~75% | ~92% | ~83% |
| Claude 3.7 Sonnet | ~49% | ~42% | ~46% |

> Note: From Claude 3.7 Sonnet (~46% in 2024) to Claude Opus 4.6 (~95% in 2026), τ²-bench experienced one of the most significant capability leaps in benchmark history.

## Example Tasks

### Airline Domain
```
User: I booked flight JK123 yesterday and now want to cancel. Can I?

Agent needs to:
1. Call get_reservation(id="JK123") to query the booking
2. Check cancellation policy (free cancellation 24 hours before departure)
3. Based on the query results, decide whether cancellation is possible
4. If eligible, call cancel_reservation(id="JK123")
5. If not eligible, politely explain the policy
```

### Retail Domain
```
User: I want to use two coupons and a membership discount together to buy this item.

Agent needs to:
1. Check the applicable conditions for each coupon
2. Verify whether discount stacking complies with company policy (some discounts cannot be stacked)
3. Correctly apply compliant discount combinations
4. If stacking is not allowed, clearly explain why
```

## Variants and Related Benchmarks

### τ-bench (Original Version)
- Released in 2024
- Only includes airline and retail domains
- No dual-control environment

### τ³-bench (Latest Version)
- Released in 2026
- Added banking_knowledge domain (knowledge retrieval + RAG)
- Added voice full-duplex evaluation mode
- 75+ task quality fixes
- **Leaderboard**: https://taubench.com

### BFCL
- Focuses on function call format rather than policy compliance
- **Separate file**: See `BFCL.md`

### GAIA
- Tests comprehensive capabilities of tool use + reasoning
- **Separate file**: See `GAIA.md`

## Limitations and Controversies

1. **Limited Domains**: Only four domains — airline, retail, telecom, and banking
2. **Simulated Users**: Uses LLM-simulated users, which may not reflect real user behavior distributions
3. **Rigid Policies**: Company policy rules are strict; real-world rules are often more flexible
4. **Primarily English**: Currently mainly evaluates English scenarios
5. **Rapid Saturation**: Top models have reached 95%+, and discrimination is declining
6. **Pass@k k-value Selection**: Model rankings may differ under different k values

## Data Sources / References

- τ-bench paper: https://arxiv.org/abs/2406.12045
- τ²-bench paper: https://arxiv.org/abs/2506.07982
- τ³-bench (τ-Knowledge): https://arxiv.org/abs/2603.04370
- τ-Voice paper: https://arxiv.org/abs/2603.13686
- GitHub: https://github.com/sierra-research/tau2-bench
- Leaderboard: https://taubench.com