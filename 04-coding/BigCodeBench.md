# BigCodeBench — Large-Scale Real-World Code Generation Evaluation

## Basic Information

| Property | Value |
|------|-----|
| Full Name | BigCodeBench |
| Creator | BigCode Community (Zhu et al.) |
| Release Year | 2024 |
| Number of Problems | 1,140+ |
| Problem Type | Real-world code generation |
| Dataset Link | https://huggingface.co/datasets/bigcode/bigcodebench |
| Paper Link | https://arxiv.org/abs/2406.04434 |
| GitHub | https://github.com/bigcode-project/bigcodebench |
| Website | https://bigcode-bench.github.io |
| Status | ✅ Still discriminative (top models < 70%) |

## Overview

BigCodeBench is a large-scale code generation evaluation benchmark released by the BigCode Community in 2024, containing 1,140+ Python programming tasks based on real-world scenarios. Unlike HumanEval and MBPP's simple function generation, BigCodeBench requires models to generate code involving complex logic, multi-step operations, and rich Python library calls.

BigCodeBench's core design philosophy is: evaluating models' code generation ability in real software development scenarios, rather than simple algorithm problems. Problems originate from real development tasks, covering API usage across 130+ Python packages.

## Dataset Composition

BigCodeBench provides two evaluation variants:

| Variant | Number of Problems | Description |
|------|----------|------|
| BigCodeBench-Complete | 1,140+ | Given function signature and docstring, complete function implementation |
| BigCodeBench-Instruct | 1,140+ | Given natural language instructions, generate complete function |

Main domains covered by problems:

| Domain | Proportion | Typical Tasks |
|------|------|----------|
| Data Processing | ~30% | CSV/JSON parsing, data cleaning, format conversion |
| File Operations | ~15% | File reading/writing, path handling, compression/decompression |
| Network Requests | ~15% | API calls, HTTP requests, web scraping |
| Mathematical Computation | ~10% | Statistical analysis, numerical computation |
| System Operations | ~10% | Process management, environment variables |
| Other | ~20% | Image processing, encryption/decryption, database operations |

Examples of Python libraries involved: `pandas`, `numpy`, `requests`, `os`, `json`, `csv`, `datetime`, `re`, `hashlib`, `PIL`, `sqlite3`, etc.

## Evaluation Method

- **Primary metric**: Pass@1 (probability of passing in a single generation)
- **Scoring method**:
  1. Execute generated code in a sandboxed Python environment
  2. Run multiple test cases (average 5+ tests per problem)
  3. Calculate test case pass rate
- **Auxiliary metrics**:
  - Calibrated Pass@1: Calibrated pass rate, reducing bias from insufficient test cases
  - Completeness score: Whether the code handles edge cases

## Model Performance (April 2026)

### BigCodeBench-Complete

| Model | Pass@1 |
|------|--------|
| Claude Opus 4.6 | ~65% |
| GPT-5 | ~62% |
| Gemini 3 Pro | ~58% |
| DeepSeek V3 | ~50% |
| CodeLlama 70B (2024) | ~35% |

### BigCodeBench-Instruct

| Model | Pass@1 |
|------|--------|
| Claude Opus 4.6 | ~60% |
| GPT-5 | ~57% |
| Gemini 3 Pro | ~52% |
| DeepSeek V3 | ~45% |

Data sources: Various model technical reports and public evaluation results

Note: Values with ~ are approximate, from unofficial sources or estimates.

## Problem Examples

### Data Processing Problem
```python
def task_csv_to_json(csv_path, json_path):
    """Read a CSV file from csv_path, convert it to JSON format,
    and write the result to json_path. The CSV file contains
    columns: name, age, email. Handle missing values by using null.
    """
```

### Network Request Problem
```python
def task_fetch_api_data(url, params, output_path):
    """Make a GET request to the given URL with query parameters.
    Parse the JSON response, extract the 'results' field,
    filter items where 'status' is 'active',
    and save the filtered list to output_path as JSON.
    Handle HTTP errors by returning an empty list.
    """
```

### Comprehensive Problem
```python
def task_analyze_log_file(log_path, output_path):
    """Read a log file, parse each line to extract timestamp,
    log level, and message. Group entries by log level,
    compute statistics (count, earliest, latest timestamp per level),
    and write results to output_path as a formatted JSON report.
    Handle malformed lines by skipping them.
    """
```

## Variants and Related Benchmarks

| Variant | Description |
|------|------|
| BigCodeBench-Complete | Function completion mode (given signature + docstring) |
| BigCodeBench-Instruct | Instruction mode (given natural language description) |
| HumanEval | 164 simple hand-written problems, see [HumanEval.md](./HumanEval.md) |
| MBPP | 1,000 basic Python problems, see [MBPP.md](./MBPP.md) |
| LiveCodeBench | Live competitive programming problems, see [LiveCodeBench.md](./LiveCodeBench.md) |

## Limitations and Controversies

1. **Python Only**: Current version only covers Python, does not evaluate multilingual capability
2. **Heavy Library Dependencies**: Highly dependent on the rich libraries of the Python ecosystem, not representative of other language ecosystems
3. **Sandbox Limitations**: Some problems involve system operations, sandbox environments may limit evaluation accuracy
4. **Uneven Difficulty Distribution**: Data processing problems are overrepresented, algorithmic complexity is relatively limited
5. **Contamination Risk**: Although problems are original, the API usage patterns involved are widely present in training data

## Data Sources/References

- Zhu, T., et al. "BigCodeBench: Benchmarking Code Generation with Diverse Function Calls and Complex Libraries." arXiv:2406.04434, 2024.
- HuggingFace BigCodeBench dataset: https://huggingface.co/datasets/bigcode/bigcodebench
- BigCodeBench official website: https://bigcode-bench.github.io