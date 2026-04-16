# AI Benchmark Knowledge Base

> A comprehensive collection of benchmarks used by major AI companies to evaluate model performance

**[中文版 (Chinese Version)](README.zh-CN.md)**

## Overview

This knowledge base systematically catalogs mainstream AI evaluation benchmarks, covering all important benchmark suites used by OpenAI, Anthropic, Google DeepMind, Meta, Mistral, and others in their technical reports.

## Directory Structure

```
ai-benchmark-kb/
├── README.md                    # This file — overview & navigation
├── 00-overview/
│   ├── benchmark-landscape.md   # Benchmark landscape & classification
│   ├── evaluation-frameworks.md # Evaluation frameworks & tools
│   └── company-usage-matrix.md # Benchmark usage by company
├── 01-general-knowledge/
│   ├── MMLU.md                  # Massive Multitask Language Understanding
│   ├── MMLU-Pro.md             # MMLU Professional
│   ├── BIG-bench.md            # Beyond the Imitation Game
│   ├── ARC.md                  # AI2 Reasoning Challenge
│   ├── HellaSwag.md            # Commonsense Reasoning
│   ├── C-Eval.md               # Chinese Comprehensive Evaluation
│   └── MMMLU.md                # Multilingual MMLU
├── 02-reasoning/
│   ├── GPQA.md                 # Graduate-Level Google-Proof Q&A
│   ├── ARC-AGI.md              # Abstraction and Reasoning Corpus
│   ├── ARC-AGI-2.md            # Abstraction and Reasoning Corpus v2 (2025)
│   ├── HLE.md                  # Humanity's Last Exam
│   ├── WinoGrande.md           # Coreference Resolution Reasoning
│   ├── PIQA.md                 # Physical Intuition QA
│   └── SIQA.md                 # Social Interaction QA
├── 03-math-reasoning/
│   ├── GSM8K.md                # Grade School Math 8K
│   ├── MATH.md                 # Competition Mathematics
│   ├── Minerva-Math.md         # DeepMind Math Evaluation
│   └── MATH-500.md             # MATH Curated 500
├── 04-coding/
│   ├── HumanEval.md            # OpenAI 164 Programming Problems
│   ├── MBPP.md                 # Most Basic Python Problems
│   ├── SWE-bench.md            # Real GitHub Issue Fixing
│   ├── SWE-bench-Verified.md   # SWE-bench Human-Verified Subset
│   ├── SWE-bench-Pro.md        # SWE-bench Professional
│   ├── LiveCodeBench.md        # Live Programming Competition
│   ├── BigCodeBench.md         # Large-Scale Code Evaluation
│   └── CodeForces.md           # Competitive Programming Evaluation
├── 05-long-context/
│   ├── MRCR.md                 # Multi-Round Coreference Resolution
│   ├── AA-LCR.md               # Long Context Reasoning
│   └── RULER.md                # Long Text Retrieval & Reasoning
├── 06-instruction-following/
│   ├── IFEval.md               # Instruction Following Evaluation
│   ├── MT-Bench.md             # Multi-Turn Benchmark
│   └── AlpacaEval.md           # Alpaca Evaluation
├── 07-truthfulness/
│   ├── TruthfulQA.md            # Truthfulness QA
│   ├── SimpleQA.md             # Short-Answer Factual QA
│   └── FACTS.md                # Google DeepMind Factuality Suite
├── 08-safety-alignment/
│   ├── Anthropic-HH.md          # Helpful & Harmless
│   ├── RealToxicityPrompts.md   # Toxicity Prompt Evaluation
│   ├── ToxiGen.md               # Implicit Toxicity Detection
│   └── WMDP.md                  # Weapons of Mass Destruction Prevention
├── 09-multimodal/
│   ├── MMMU.md                 # Multi-Discipline Multimodal Understanding
│   ├── MMMU-Pro.md             # MMMU Professional
│   ├── VQAv2.md                # Visual Question Answering v2
│   └── MVBench.md              # Video Understanding Evaluation
├── 10-dialogue-generation/
│   ├── Chatbot-Arena.md         # Chatbot Arena
│   ├── WildBench.md            # Wild Evaluation
│   └── MixEval.md              # Mixed Evaluation
├── 11-embedding-retrieval/
│   ├── MTEB.md                 # Massive Text Embedding Benchmark
│   └── BEIR.md                 # Information Retrieval Evaluation
├── 12-agent-capabilities/
│   ├── GAIA.md                  # General AI Assistant Evaluation
│   ├── RE-Bench.md              # Agent Reasoning Evaluation
│   ├── BFCL.md                  # Berkeley Function Calling Leaderboard
│   ├── Tau2.md                  # Multi-Turn Agent Evaluation
│   ├── BrowseComp.md            # Browser Agent Evaluation
│   ├── OSWorld.md               # OS Agent Evaluation
│   ├── WebArena.md              # Web Agent Evaluation
│   └── GDPval.md                # GDP Validation Evaluation
├── 13-domain-specific/
│   ├── HealthBench.md           # Healthcare Evaluation
│   ├── DeepSearchQA.md          # Deep Search QA
│   └── Chess-Text.md           # Chess Reasoning
├── 14-competition-math/
│   ├── AIME.md                  # American Invitational Mathematics Exam
│   ├── HMMT.md                  # Harvard-MIT Mathematics Tournament
│   └── FrontierMath.md          # Frontier Math Evaluation
└── 15-eval-frameworks/
    ├── eval-frameworks-tools.md # Evaluation Frameworks & Tools Overview
    └── emerging-benchmark-trends.md # Emerging Benchmark Trends
```

## Benchmark Classification Quick Reference

| Category | Representative Benchmarks | Core Evaluation Dimension |
|----------|--------------------------|---------------------------|
| General Knowledge | MMLU, MMLU-Pro, BIG-bench | Subject knowledge coverage |
| Reasoning | GPQA, ARC-AGI, ARC-AGI-2, HLE | Deep reasoning & generalization |
| Math | GSM8K, MATH, AIME | Mathematical problem solving |
| Coding | HumanEval, SWE-bench, LiveCodeBench, CodeForces, SWE-bench Verified | Code generation & software engineering |
| Long Context | MRCR, AA-LCR, RULER | Long-text understanding & reasoning |
| Instruction Following | IFEval, MT-Bench | Format/constraint compliance |
| Truthfulness | TruthfulQA, FACTS, SimpleQA | Factual accuracy & hallucination |
| Safety & Alignment | Anthropic HH, WMDP | Safety & alignment |
| Multimodal | MMMU, MMMU-Pro, VQAv2 | Joint image-text understanding |
| Dialogue & Generation | Chatbot Arena, WildBench | Human preference alignment |
| Agent | GAIA, BFCL, RE-Bench, BrowseComp, OSWorld, WebArena | Agent tool use capability |
| Competition Math | AIME, HMMT, FrontierMath | Competition-level math solving |

## Company Usage Reference

| Company | Core Benchmarks Used in Technical Reports |
|---------|------------------------------------------|
| OpenAI | MMLU, MMLU-Pro, GSM8K, MATH, HumanEval, SWE-bench, GPQA, ARC-AGI, SimpleQA, Chatbot Arena, BrowseComp, OSWorld, MMMU-Pro |
| Anthropic | MMLU, GSM8K, MATH, HumanEval, SWE-bench, GPQA, IFEval, Chatbot Arena, HLE, BrowseComp, OSWorld, MMMU-Pro |
| Google DeepMind | MMLU, GSM8K, MATH, HumanEval, SWE-bench, GPQA, FACTS, SimpleQA Verified, MRCR, Chess Text, MMMU-Pro |
| Meta (Llama) | MMLU, GSM8K, MATH, HumanEval, HellaSwag, ARC, TruthfulQA, WinoGrande |
| Mistral | MMLU, GSM8K, HumanEval, MBPP, HellaSwag, ARC |
| DeepSeek | MMLU, GSM8K, MATH, HumanEval, AIME, CodeForces |

## Data Sources

- HuggingFace Datasets: https://huggingface.co/datasets
- EleutherAI lm-eval-harness: https://github.com/EleutherAI/lm-evaluation-harness
- Stanford HELM: https://crfm.stanford.edu/helm/
- Stanford AI Index Report 2025: https://hai.stanford.edu/ai-index-report
- Scale AI Leaderboards: https://scale.com/leaderboard
- Artificial Analysis: https://artificialanalysis.ai/

## Version Information

- Created: 2026-04-12
- Last Updated: 2026-04-16
- Data Cutoff: April 2026