# DeepSearchQA — Deep Search Question Answering

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | DeepSearchQA |
| Creators | Google DeepMind |
| Year Published | 2025 |
| Number of Questions | 900 |
| Domains Covered | 17 domains |
| Task Type | Multi-step search planning Q&A |
| Dataset Link | Kaggle Leaderboard |
| Status | Standard for search-augmented reasoning evaluation |

## Overview

DeepSearchQA is a deep search question answering evaluation benchmark developed by Google DeepMind, focused on evaluating AI systems' performance on complex questions requiring multi-step search and information integration. Unlike traditional single-step retrieval Q&A, DeepSearchQA requires models to have long-horizon planning and causal reasoning capabilities; each question requires progressively obtaining and integrating information through multiple search steps before answering.

## Dataset Composition

### Domain Coverage

17 domains include but are not limited to:

1. **Science & Technology**: Frontiers of physics, biotechnology, computer science
2. **Medicine & Health**: Clinical research, public health policy
3. **History & Humanities**: Cross-cultural historical events, archaeological discoveries
4. **Economics & Finance**: Global market dynamics, policy impacts
5. **Law & Policy**: International regulations, environmental policy
6. **Geography & Environment**: Climate change, ecosystems

### Causal Chain Structure

The core design feature of DeepSearchQA is the Causal Chain structure:

- Each question consists of a causal chain, where each node on the chain represents a search step
- The result of a previous search step is the input condition for the next search step
- The model must execute search steps in the correct causal order
- Skipping steps or out-of-order execution will result in missing critical information

### Long-Horizon Planning Requirements

- Average question requires 3-5 search steps
- Some difficult questions require 6+ steps
- Requires integrating information across multiple search steps
- Must plan an overall strategy before searching

## Evaluation Method

### Scoring Criteria

- **Answer Accuracy**: Exact match of the final answer with the reference answer
- **Search Efficiency**: Minimum number of search steps needed to reach the correct answer
- **Planning Quality**: Reasonableness and completeness of the search path

### Objectively Verifiable

- All questions have objectively verifiable answers
- Answers are concrete factual content (names, numbers, locations, etc.)
- Answer correctness can be independently verified through external knowledge sources

### Leaderboard

- Hosted on Kaggle Leaderboard
- Real-time ranking updates
- Supports submission of both search strategies and final answers

## Model Performance (April 2026)

| Model | DeepSearchQA Accuracy |
|-------|----------------------|
| Gemini 3 Pro | ~35% |
| GPT-5 | ~30% |
| Claude Opus 4.6 | ~28% |
| Agent systems with search tools | ~40% |

> Note: The above are approximate values; please refer to the Kaggle leaderboard for specific scores. Agent systems with search tools refer to AI agents equipped with complete search and browsing tools.

## Example Tasks

### Multi-Step Causal Chain Example
```
Question: Who is the corresponding author of the last paper published before
winning the 2024 Nobel Prize in Chemistry? Which institution does that
corresponding author currently work at?

Search step planning:
1. Search "2024 Nobel Prize in Chemistry laureates" → Get laureate names
2. Search "[laureate] latest paper" → Get paper list
3. Search "[paper title] corresponding author" → Get corresponding author name
4. Search "[corresponding author] current institution" → Get institution

Answer: [Specific answer]
```

### Cross-Domain Integration Example
```
Question: Which country's capital has both an airport named after a Nobel Peace Prize
laureate and a UNESCO World Heritage Site? What year was the heritage site inscribed?

Search step planning:
1. Search "airports named after Nobel Peace Prize laureates" → Get candidate list
2. For each candidate, confirm the country's capital → Narrow down
3. Search "[candidate capital] World Heritage" → Verify if there is a World Heritage site
4. Search "[heritage site name] inscription year" → Get final answer

Answer: [Specific answer]
```

## Variants and Related Benchmarks

### GAIA
- Also tests multi-step reasoning and tool use
- Broader task types, but shallower search planning depth
- See [12-agent-capabilities/GAIA.md](../12-agent-capabilities/GAIA.md)

### FRAMES
- Tests multi-hop reasoning for factual Q&A
- Focuses on reasoning chain length rather than search strategy planning

### BrowseComp
- Browser usage capability evaluation
- Focuses on information retrieval efficiency rather than deep planning

## Limitations and Controversies

1. **Search Environment Dependency**: Evaluation results are affected by search tool quality and accessibility
2. **Answer Timeliness**: Some answers may change over time, requiring periodic updates
3. **Scoring Granularity**: Only evaluates final answer correctness, not fully considering intermediate step quality
4. **Coverage Balance**: The number of questions across 17 domains may not be evenly distributed
5. **Search Strategy Diversity**: The same question may have multiple valid search paths, which scoring does not fully account for

## Data Sources / References

- Google DeepMind DeepSearchQA official release
- Kaggle Leaderboard ranking data