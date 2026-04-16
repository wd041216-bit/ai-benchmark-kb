# GAIA — General AI Assistants Benchmark

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | GAIA: A Benchmark for General AI Assistants |
| Creators | Meta AI, Hugging Face, AutoGPT et al. |
| Year Published | 2023 |
| Number of Questions | 466 (3 difficulty levels) |
| Task Type | Complex tasks requiring reasoning, tool use, and multi-step operations |
| Dataset Link | https://huggingface.co/datasets/gaia-benchmark/GAIA |
| Paper Link | https://arxiv.org/abs/2311.12983 |
| GitHub | https://github.com/gaia-benchmark/GAIA |
| Status | ✅ Highly discriminative (top models < 50%) |

## Evaluation Dimensions

GAIA tests AI agents' ability to solve real-world complex tasks:

1. **Reasoning**: Multi-step logical reasoning
2. **Tool Use**: Web search, code execution, file processing
3. **Information Integration**: Integrating information from multiple sources
4. **Planning and Execution**: Formulating and executing multi-step plans
5. **File Processing**: Handling attachments (PDFs, images, audio, etc.)

## Difficulty Levels

### Level 1 (General Difficulty)
- No tools or only simple tools needed
- Approximately 160 questions
- Example: "In which city is the university where the 2023 Nobel Prize in Physics laureate works?"

### Level 2 (Medium Difficulty)
- Requires using 1-2 tools
- Approximately 153 questions
- Example: "Analyze the audio file in the attachment, identify all the bird species mentioned, then calculate the average lifespan of these birds."

### Level 3 (Difficult)
- Requires complex reasoning and multi-step tool use
- Approximately 153 questions
- Example: "The attachment contains a PDF file. Extract all company names mentioned on the third page, look up each company's latest 10-K annual report on SEC EDGAR, then calculate the total revenue of these companies in 2023."

## Example Questions

### Easy (Level 1)
```
On June 6, 2023, an article in The New York Times mentioned a specific scientific paper.
What was the title of that paper?

Answer: [Exact answer]
```

### Medium (Level 2)
```
[Attachment: An image]
The attached image shows a map fragment. What is the name of the country that
is directly south of the highlighted region?

Answer: [Exact answer]
```

### Hard (Level 3)
```
[Attachment: A CSV file]
The attached CSV file contains weather data. What was the average temperature
on the day when the wind speed was highest, across all weather stations?

Answer: 72.3
```

## Scoring Method

- **Exact Match**: The answer must be exactly correct
- **Level-based Scoring**: Accuracy reported separately for Level 1/2/3
- **Average Accuracy**: Weighted average across three levels
- **No Partial Credit**: An answer is either fully correct or wrong

## Model Performance (April 2026)

| Model | GAIA Overall | Level 1 | Level 2 | Level 3 |
|-------|-------------|---------|---------|---------|
| Gemini 3.1 Pro Preview | ~42% | ~70% | ~35% | ~20% |
| Claude Opus 4.6 | ~38% | ~65% | ~30% | ~18% |
| GPT-5 | ~36% | ~62% | ~28% | ~16% |
| DeepSeek R1 | ~22% | ~45% | ~15% | ~5% |
| Humans | ~92% | ~95% | ~90% | ~88% |

## Why GAIA Is Important

1. **Real-World Tasks**: Not simple Q&A like traditional benchmarks
2. **Tests Agent Capabilities**: Requires tool use and multi-step planning
3. **Extremely High Discrimination**: Top models only ~40%
4. **File Processing**: Tests multimodal input processing
5. **Future Direction**: Represents the direction of AI development (from Q&A to agents)

## Variants and Related Benchmarks

### RE-Bench
- Tests AI agents' reasoning and execution capabilities in real ML R&D engineering tasks
- 7 hand-crafted environments, compared against human expert baselines
- **Separate file**: See `RE-Bench.md`

### VisualAgentBench
- Visual agent evaluation
- Tests multimodal agent capabilities

### τ²-bench (Tau2)
- Multi-turn conversational agent evaluation, testing policy compliance + tool calling
- Aviation, retail, telecom, and other domains
- **Separate file**: See `Tau2.md`

### BFCL
- Berkeley Function Calling Leaderboard, testing tool use / function calling capabilities
- Comprehensive evaluation from single-turn to multi-step to multi-turn
- **Separate file**: See `BFCL.md`

### BrowseComp
- Tests deep browsing and persistent search capabilities
- 1,266 questions that are hard to retrieve but easy to verify
- **Separate file**: See `BrowseComp.md`

### OSWorld
- Tests agent capabilities in real desktop OS environments
- 369 cross-application tasks (Ubuntu/Windows/macOS)
- **Separate file**: See `OSWorld.md`

### WebArena
- Tests agent interaction capabilities in web environments
- 812 real web interaction tasks
- **Separate file**: See `WebArena.md`

### GDPval
- Measures AI performance on real-world professional tasks with economic value
- 1,320 tasks, covering 44 occupations
- **Separate file**: See `GDPval.md`

## Limitations and Controversies

1. **Limited Number of Questions**: A sample of 466 questions is relatively small for fine-grained evaluation
2. **Attachment Processing Difficulty**: Processing multimodal files (PDF, audio, images) increases evaluation complexity
3. **Inflexible Scoring**: Exact match scoring cannot tolerate reasonable variations of answers
4. **Human Baseline Controversy**: Whether the 92% human baseline represents a "true human ceiling" is debated
5. **Data Contamination Risk**: Questions and answers are publicly available; subsequent models may encounter them indirectly through training data

## Data Sources / References

- GAIA paper: https://arxiv.org/abs/2311.12983
- Dataset: https://huggingface.co/datasets/gaia-benchmark/GAIA
- GitHub: https://github.com/gaia-benchmark/GAIA
- GAIA leaderboard: https://huggingface.co/spaces/gaia-benchmark/leaderboard