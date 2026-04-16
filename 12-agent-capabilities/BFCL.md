# BFCL — Berkeley Function Calling Leaderboard

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | Berkeley Function Calling Leaderboard (BFCL) |
| Creators | UC Berkeley (Gorilla team, Shishir Patil et al.) |
| Year Published | 2024 (V1), continuously updated to V4 |
| Number of Questions | ~4,400+ (V3), continuously expanding |
| Task Type | Function calling / tool use (single-turn, multi-step, multi-turn) |
| Dataset Link | https://huggingface.co/datasets/gorilla-llm/BFCL |
| Paper Link | ICML 2025 |
| Leaderboard Link | https://gorilla.cs.berkeley.edu/leaderboard |
| GitHub | https://github.com/ShishirPatil/gorilla |
| Status | ✅ Most active function calling evaluation, continuously updated |

## Overview

BFCL is an evaluation benchmark developed by the UC Berkeley Gorilla team, specifically designed to evaluate large language models' **function calling (Function Calling / Tool Use)** capabilities. As the core benchmark for evaluating tool use capabilities, BFCL has progressively expanded from simple single-function calling to complex multi-turn conversational tool orchestration, evolving from V1 to V4, and remains the standard for measuring agent tool use capabilities.

Core design principles:
- **AST Evaluation**: Uses abstract syntax trees to precisely compare function calls, rather than simple string matching
- **Real-World Scenarios**: Functions sourced from real APIs (weather, finance, calendar, etc.)
- **Multi-Version Evolution**: From single-turn to multi-step to multi-turn, progressively increasing complexity
- **Open-Source Evaluation**: Complete evaluation code is open source, available via `pip install bfcl-eval`

## Dataset Composition

### V1 — Single-Turn Function Calling (Early 2024)
- Introduced AST as an evaluation metric
- Basic single-function calling scenarios
- Approximately 1,400 questions

### V2 — Enterprise-Grade and Community Contributions (August 2024)
- Added real-time data contributed by enterprises and open-source communities
- Added Live subset using the latest API definitions
- Expanded to approximately 3,600 questions

### V3 — Multi-Turn and Multi-Step Calling (September 2024)

**Core Innovation**: Introduced multi-turn and multi-step evaluation.

| Category | Count | Description |
|----------|-------|-------------|
| Basic Multi-Turn | 200 | 4 domains (file system, vehicle control, trading bot, travel booking) |
| Missing Parameters | 200 | Model must identify missing parameters and ask the user |
| Missing Functions | 200 | Model must identify that no available function can satisfy the request |
| Long Context Multi-Turn | 200 | Function calling in information-dense contexts |
| Composite Challenges | 200 | Combination of the three challenges above |

### V4 — Agent Evaluation (2025)
- Added holistic agent evaluation
- Includes real tool use such as web search
- Expanded from pure function calling to end-to-end agent workflows

### Overall Score Composition (V3)

Total score = unweighted average of:
- Non-live / single-turn (1,390 items)
- Live / single-turn (2,251 items)
- Multi-turn (800 items)

## Evaluation Method

### Single-Turn Evaluation
- Uses **AST (Abstract Syntax Tree)** comparison
- Exact matching of function names, parameter names, and parameter values
- Allows equivalent calls with different parameter ordering

### Multi-Turn Evaluation
- **State-based Evaluation**: Compares backend system state after function execution
- **Subset Matching Evaluation**: Checks whether the model's execution path contains the minimum viable truth subset, allowing multiple valid trajectories

### Evaluation Dimensions

| Dimension | Description |
|-----------|-------------|
| Function Selection | Whether the correct function was selected |
| Parameter Passing | Whether parameter names and values are correct |
| Parallel Calling | Whether multiple independent functions can be called simultaneously |
| Missing Handling | Whether missing parameters / unavailable functions can be identified |
| Context Maintenance | Whether context is maintained across multi-turn conversations |

## Model Performance (April 2026)

### BFCL V3 Leaderboard (as of April 2026)

| Model | BFCL V3 Overall | Notes |
|-------|-----------------|-------|
| GLM-4.5 (Zhipu) | ~77.8% | Chinese model leading |
| Qwen3 VL 560B | ~74.4% | |
| Qwen3 VL 80B Thinking | ~72.0% | |
| Qwen3 236B Thinking | ~71.9% | |
| Gemini 3.1 Pro | ~70% | |
| Claude Opus 4.6 | ~68% | |
| GPT-5 | ~67% | |
| DeepSeek V3 | ~60% | |

> Note: The BFCL leaderboard is updated frequently; the above are approximate values. Please refer to the official leaderboard for the latest data.

## Example Tasks

### Single-Turn Function Calling
```json
// User input
"What's the weather like in San Francisco today?"

// Available functions
[get_weather(location: str, unit: str)]

// Expected output
{"name": "get_weather", "arguments": {"location": "San Francisco", "unit": "celsius"}}
```

### Multi-Step Function Calling
```json
// User input
"Book me a flight from New York to London for tomorrow, then book a hotel in London."

// Expected: Model must call in sequence
// 1. search_flights(origin, destination, date)
// 2. book_flight(flight_id)
// 3. search_hotels(location, check_in, check_out)
// 4. book_hotel(hotel_id)
```

### Missing Parameter Detection
```json
// User input
"Send an email for me."

// Available functions
[send_email(to: str, subject: str, body: str)]

// Expected output: Model should ask for missing parameters
"Who would you like to send it to? What should the subject and body be?"
```

## Variants and Related Benchmarks

### BFCL V4
- Added end-to-end agent evaluation
- Includes web search capability testing
- Currently still in data collection phase

### Gorilla Open-Source Ecosystem
- Function calling training datasets
- APIBench (API knowledge evaluation)
- **Link**: https://github.com/ShishirPatil/gorilla

### τ²-bench
- Tests agent capabilities in multi-turn conversations
- Focuses on policy compliance rather than pure function calling
- **Separate file**: See `Tau2.md`

### GAIA
- Tests comprehensive capabilities of tool use + reasoning
- **Separate file**: See `GAIA.md`

## Limitations and Controversies

1. **Scoring Bias Toward JSON Format**: Strict requirements for function call format may favor certain models
2. **Static Function Definitions**: V1/V2 use static API definitions, which may become disconnected from real API evolution
3. **Missing Reasoning Chain Evaluation**: Primarily evaluates function call format, not the correctness of reasoning chains
4. **Insufficient Chinese Coverage**: Primarily English-focused, with limited evaluation of Chinese function calling capabilities
5. **V4 Not Yet Mature**: The agent evaluation portion is still under construction

## Data Sources / References

- BFCL paper (ICML 2025): Patil et al., "The Berkeley Function Calling Leaderboard"
- V3 blog: https://gorilla.cs.berkeley.edu/blogs/13_bfcl_v3_multi_turn.html
- V4 blog: https://gorilla.cs.berkeley.edu/blogs/15_bfcl_v4_web_search.html
- Leaderboard: https://gorilla.cs.berkeley.edu/leaderboard
- GitHub: https://github.com/ShishirPatil/gorilla
- Dataset: https://huggingface.co/datasets/gorilla-llm/BFCL
- BFCL V3 leaderboard tracking: https://pricepertoken.com/leaderboards/benchmark/bfcl-v3