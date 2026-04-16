# Emerging and Frontier Benchmarks

## New Trends in 2025-2026

### 1. Continuously Updated Benchmarks
- **SWE-bench Live**: Automatically collects new issues from GitHub every month
- **LiveCodeBench**: Continuously fetches new problems from coding competition platforms
- **Trend**: Prevent training data contamination and maintain evaluation validity

### 2. Agent Capability Evaluation
- **GAIA**: General AI assistant evaluation
- **RE-Bench**: Agent reasoning evaluation
- **BFCL v3**: Function calling capability evaluation
- **Tau2**: Multi-turn agent evaluation
- **BrowseComp**: Released by OpenAI in April 2025, 1,266 browser navigation questions
- **OSWorld**: NeurIPS 2024, 369 desktop OS tasks, computer-use standard
- **WebArena**: ICLR 2024, 812 web interaction tasks
- **GDPval**: OpenAI/ICLR 2026, 220+ economically valuable tasks
- **Trend**: From single-step Q&A to multi-step real-environment tasks

### 3. Factuality Evaluation Deepening
- **FACTS Suite**: Four-dimensional factuality evaluation
- **SimpleQA Verified**: Improved short-answer factuality
- **DeepSearchQA**: Multi-step search reasoning
- **Trend**: From simple Q&A to search-augmented and document-grounded evaluation

### 4. Long Context Evaluation
- **MRCR v2**: Multi-turn coreference resolution
- **AA-LCR**: 100K token reasoning
- **Trend**: From 4K to 1M+ token reasoning capability evaluation

### 5. Competition Math Evaluation
- **AIME 2024/2025**: New problems each year
- **FrontierMath**: Problems authored by professional mathematicians
- **HMMT**: Harvard-MIT Mathematics Tournament
- **Trend**: Continuously increasing difficulty, maintaining discrimination

### 6. Multimodal Evaluation Expansion
- **MMMU**: Multi-discipline multimodal
- **FACTS Multimodal**: Multimodal factuality
- **MMMU-Pro**: High-difficulty multimodal professional evaluation
- **VQAv2**: Visual Q&A v2
- **MVBench**: Video understanding evaluation
- **Trend**: From pure text to image-text and video understanding

### 7. Browsing and Computer-Use Evaluation
- **BrowseComp**: 1,266 hard-to-find information retrieval questions, "easy to verify, hard to solve"
- **OSWorld**: 369 real desktop environment tasks, Ubuntu/Windows/macOS
- **WebArena**: 812 real web interaction tasks
- **Trend**: From pure text Q&A to real-environment operation capability evaluation

## Upcoming Benchmarks

| Name | Domain | Expected Release |
|------|--------|-----------------|
| ARC-AGI-3 | Abstract reasoning | 2026 |
| MM-BrowseComp | Multimodal browsing | 2026 |
| WebChoreArena | Web multi-step | 2026 |
| SWE-bench Multimodal | Multimodal coding | 2026 |
| SWE-bench Live Windows | Windows coding | 2026 |
| SWE-bench Live MultiLang | Multilingual coding | 2026 |
| Multiple new Live benchmarks | Various domains | Ongoing |

## Retired Benchmarks

The following benchmarks are no longer recommended for frontier model evaluation due to saturation or quality issues:

| Benchmark | Reason for Retirement | Replacement |
|-----------|----------------------|-------------|
| GLUE | Saturated | SuperGLUE |
| SuperGLUE | Approaching saturation | MMLU-Pro |
| MMLU (original) | Approaching saturation | MMLU-Pro |
| HumanEval | Saturated | SWE-bench Live |
| GSM8K | Approaching saturation | MATH-500 |
| HellaSwag | Saturated | GPQA Diamond |
| ARC-Challenge | Approaching saturation | HLE |

## Evaluation Trend Summary

1. **From Static to Dynamic**: Static benchmarks → Continuously updated Live benchmarks
2. **From Simple to Complex**: Single-step Q&A → Multi-step reasoning and tool use
3. **From General to Specialized**: General benchmarks → Domain-specific benchmarks
4. **From Automated to Human-Centered**: Automated evaluation → Human preference evaluation (Chatbot Arena)
5. **From Unimodal to Multimodal**: Pure text → Image, text, audio, video
6. **From Q&A to Action**: Pure text Q&A → Browser navigation, desktop operations, code execution