# AI Benchmark Landscape and Taxonomy

## Evolution History

### First Generation (2020-2022): Basic Capability Evaluation
- **GLUE / SuperGLUE**: Cornerstone of natural language understanding
- **MMLU** (2021): 57-subject knowledge evaluation, becoming the most widely used LLM benchmark
- **HumanEval** (2021): 164 hand-written programming problems
- **GSM8K** (2021): Elementary school math reasoning

### Second Generation (2022-2024): Reasoning and Professionalism Enhancement
- **BIG-bench Hard**: Curated difficult subset from 204 tasks
- **GPQA Diamond**: Graduate-level expert Q&A with anti-cheating design
- **SWE-bench** (2023): Real GitHub issue fixing
- **MATH**: Competition-level math reasoning
- **MMLU-Pro**: Enhanced professional version of MMLU

### Third Generation (2024-2026): Frontier and Agent Evaluation
- **ARC-AGI-2**: Abstract reasoning, testing general intelligence
- **Humanity's Last Exam**: Expert-level difficult problems, current top score is 45.9%
- **SWE-bench Live**: Continuously updated programming benchmark
- **FACTS Benchmark Suite**: Multi-dimensional factuality evaluation
- **Chatbot Arena**: Real-time ranking based on human preferences

## Classification Dimensions

### By Capability

```
Capability Dimension
├── Knowledge Breadth
│   ├── MMLU / MMLU-Pro — 57-subject knowledge
│   ├── BIG-bench — 204-task comprehensive
│   ├── C-Eval — 52 Chinese subjects
│   └── MMMLU — 14-language knowledge
├── Reasoning Depth
│   ├── GPQA Diamond — PhD-level reasoning
│   ├── ARC-AGI — Abstract reasoning
│   ├── HLE — Humanity's Last Exam
│   └── BIG-bench Hard — Difficult reasoning
├── Math Reasoning
│   ├── GSM8K — Elementary math
│   ├── MATH — Competition math
│   ├── AIME — Math invitational
│   └── FrontierMath — Frontier math
├── Coding
│   ├── HumanEval — Function-level code generation
│   ├── SWE-bench — Real issue fixing
│   ├── LiveCodeBench — Competition programming
│   ├── BigCodeBench — Large-scale code
│   ├── CodeForces — Competition programming
│   ├── SWE-bench Verified — Human-verified software engineering
│   └── SWE-bench Pro — High-difficulty software engineering
├── Long Context
│   ├── MRCR v2 — Multi-round coreference resolution
│   ├── AA-LCR — 100K token reasoning
│   └── RULER — Long text retrieval
├── Instruction Following (IF)
│   ├── IFEval / IFBench — Format constraints
│   └── MT-Bench — Multi-turn instruction
├── Factuality
│   ├── TruthfulQA — Truthfulness
│   ├── SimpleQA Verified — Short-answer facts
│   └── FACTS — Multi-dimensional factuality
├── Safety Alignment
│   ├── Anthropic HH — Helpful and harmless
│   ├── WMDP — Weapons knowledge protection
│   └── ToxiGen — Toxicity detection
├── Agent
│   ├── GAIA — General AI assistant
│   ├── BFCL — Function calling
│   ├── RE-Bench — Agent reasoning
│   ├── BrowseComp — Browser navigation
│   ├── OSWorld — Computer use
│   └── WebArena — Web agent
└── Multimodal
    ├── MMMU-Pro — High-difficulty multimodal
    ├── MMMU — Multi-subject multimodal
    ├── VQAv2 — Visual Q&A
    └── MVBench — Video understanding
```

### By Difficulty Level

| Difficulty Level | Benchmark | Human Baseline | Frontier Model Performance |
|-----------------|-----------|---------------|----------------------------|
| Basic | MMLU, HellaSwag, ARC-Easy | ~88% | ~94% (saturated) |
| Intermediate | GSM8K, HumanEval, MMLU-Pro | ~98%/N/A | ~96%/~95% |
| Hard | GPQA Diamond, SWE-bench Verified | 65% (experts) | ~79% |
| Very Hard | HLE, ARC-AGI-2, AIME 2025 | ~90%/~0% | ~46%/~5%/~43% |
| Extremely Hard | BrowseComp, OSWorld, WebArena, GDPval | varies | <50% |
| Frontier | FrontierMath, SWE-bench Pro | N/A | <10% |

## Benchmark Saturation Analysis (April 2026)

### Saturated (top models > 90%)
- MMLU, HellaSwag, ARC-Easy, GSM8K, HumanEval

### Approaching Saturation (75-90%)
- MMLU-Pro, GPQA Diamond, SWE-bench Verified

### Still Room for Improvement (50-75%)
- SWE-bench Pro, FACTS Suite, LiveCodeBench Pro, BrowseComp (partial model performance)

### Far from Saturated (< 50%)
- HLE, ARC-AGI-2, FrontierMath, OSWorld, WebArena, AIME 2025

## Benchmark Contamination Issues

The "benchmaxxxing" phenomenon: when a benchmark becomes an industry standard, models begin optimizing for it, leading to:
1. Benchmark questions appearing in training data
2. Optimization for specific formats rather than genuine capability improvement
3. Inflated scores but poor real-world application performance

### Countermeasures
- **Live series benchmarks** (LiveCodeBench, SWE-bench Live): Continuously updated to prevent contamination
- **Private evaluation sets**: Keeping hidden test data
- **GPQA Diamond**: Questions are not Google-searchable
- **Chatbot Arena**: Based on real human preferences, impossible to cheat through pre-training

### 2025-2026 Emerging Directions

1. **Agent evaluation explosion**: BrowseComp, OSWorld, WebArena, GDPval, etc. testing AI agent performance in real-world environments
2. **Long context becoming standard**: MRCR v2, AA-LCR, etc. testing 128K-1M token reasoning capabilities
3. **Factuality deepening**: SimpleQA Verified, FACTS Suite moving from simple Q&A to search-augmented and document-grounded evaluation
4. **Competition math upgrading**: AIME 2025 approaching saturation, HMMT and FrontierMath becoming new sources of differentiation