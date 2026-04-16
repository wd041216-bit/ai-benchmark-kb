# OSWorld — Real OS Environment Agent Evaluation

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | OSWorld: Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments |
| Creators | University of Hong Kong (HKU), Salesforce Research, CMU, University of Waterloo |
| Year Published | 2024 (NeurIPS 2024), 2025 (OSWorld-Verified update) |
| Number of Questions | 369 |
| Task Type | Real desktop OS tasks (cross-application, file operations, web interaction, etc.) |
| Project Page | http://os-world.github.io/ |
| Paper Link | https://arxiv.org/abs/2404.07972 |
| GitHub | https://github.com/xlang-ai/osworld |
| Status | 🔥 Most important benchmark for computer-use agents, human baseline 72.4% |

## Overview

OSWorld is the first scalable **real computer environment** evaluation benchmark for assessing multimodal agents' ability to perform open-ended tasks in real desktop operating systems (Ubuntu, Windows, macOS). Unlike benchmarks that test in simulated environments or single applications, OSWorld runs in real OS environments where agents must operate mice, keyboards, and applications like humans.

Core innovations:
1. **Real OS Environment**: Not a simulator, but real Ubuntu/Windows/macOS desktops
2. **Cross-Application Workflows**: Tasks may involve collaboration across multiple applications (e.g., copying data from web to Excel)
3. **Execution-Based Evaluation**: Verifies task completion through custom scripts rather than checking action sequences
4. **134 Unique Evaluation Functions**: Precise verification logic tailored to different task types

## Dataset Composition

### OS Distribution

| OS | Number of Tasks | Description |
|----|----------------|-------------|
| Ubuntu | ~150 | Linux desktop environment |
| Windows | ~130 | Windows desktop environment |
| macOS | ~90 | macOS desktop environment |

### Task Types

| Type | Percentage | Example |
|------|-----------|---------|
| Desktop Application Operations | ~40% | Formatting documents in LibreOffice/Office |
| Web Browsing | ~30% | Searching and operating in Chrome/Firefox |
| File Management | ~15% | Organizing files, renaming, compressing |
| Multi-Application Collaboration | ~15% | Cross-application data transfer and operations |

### Evaluation Functions

- **134 unique evaluation functions**
- Each task has a dedicated verification script
- Supports partial credit scoring
- Based on actual execution results, not action sequences

## Evaluation Method

1. **Initialize Environment**: Launch a clean OS snapshot in a Docker/VM
2. **Execute Task**: Agent perceives the environment through screenshots and accessibility trees, outputting operation instructions
3. **Verify Results**: Run evaluation scripts to check whether the task is completed
4. **Calculate Success Rate**: Percentage of subtasks passed

### Input Formats

| Format | Description |
|--------|-------------|
| Screenshot | Pixel-level screen image |
| Accessibility Tree (A11y Tree) | Tree-structured representation of UI elements |
| Set-of-Marks (SoM) | Visual markers of interactive elements overlaid on screenshots |

### Key Findings

- **Higher Resolution Screenshots Improve Performance**: Higher resolution input improves operation accuracy
- **Text Trajectory History Helps**: Text-based history information improves multi-step reasoning
- **Pure Screenshot History Hurts**: Only viewing past screenshots actually degrades performance
- **SoM Effects Vary by Model**: Helps some models but is detrimental for the many small elements in OS environments
- **Ubuntu and Windows Highly Correlated**: r=0.7, suggesting the bottleneck is general operation capability rather than specific OS knowledge

## Model Performance (April 2026)

### OSWorld Evolution Timeline

| Time | Model | Score | Notes |
|------|-------|-------|-------|
| April 2024 | GPT-4 (a11y tree) | 12.24% | OSWorld initial release |
| October 2024 | Claude 3.5 Sonnet | 14.9% | First commercial computer-use product |
| January 2025 | OpenAI Operator (CUA) | 38.1% | ChatGPT Pro |
| May 2025 | Claude Sonnet 4 | 43.9% | |
| July 2025 | GTA1 (Salesforce) | 45.2% | OSWorld-Verified #1 |
| August 2025 | CoACT-1 | 60.76% | Hybrid GUI+code approach |
| September 2025 | Claude Sonnet 4.5 | 61.4% | |
| November 2025 | Claude Opus 4.5 | 66.3% | First to exceed 65% |
| February 2026 | Claude Opus 4.6 | 72.7% | Approaching human baseline |
| February 2026 | Claude Sonnet 4.6 | 72.5% | 1/5 the price, approaching Opus |
| March 2026 | GPT-5.4 | ~75.0%* | First to surpass human baseline (*self-reported) |

### Current Leaderboard

| Model | OSWorld Score | Price (Input/Output per 1M tokens) |
|-------|--------------|--------------------------------------|
| GPT-5.4 | ~75.0%* | $2.50/$15 |
| OSAgent | 76.26% | Limited availability |
| Claude Opus 4.6 | 72.7% | $5/$25 |
| Claude Sonnet 4.6 | 72.5% | $3/$15 |
| Claude Opus 4.5 | 66.3% | — |
| Qwen3 VL 235B | 66.7% | Best open-source |

> *GPT-5.4 score is self-reported and not yet independently verified.

> Note: From 14.9% in October 2024 to 72.7% in February 2026, Claude computer-use improved approximately 58 percentage points in 16 months.

### Human Baseline

| Human Level | Score |
|-------------|-------|
| Human Expert | 72.36% |

## Example Tasks

### Desktop Application Operations
```
Task: Open the attached document in LibreOffice Writer, change the title font to Arial,
     size to 16pt, bold, then save as PDF format to the desktop.

Evaluation: Check the font, size, and bold attributes of the title in the output PDF file.
```

### Cross-Application Workflow
```
Task: Open Chrome browser, visit weather.com to find today's weather in New York City,
     then create a spreadsheet in LibreOffice Calc containing that weather information.

Evaluation: Check whether the Calc file contains the correct weather data.
```

### File Management
```
Task: Move all .jpg files from the Downloads folder to the Pictures folder,
     and rename them to "photo_YYYYMMDD.jpg" format by date.

Evaluation: Check whether files are correctly moved and renamed.
```

## Variants and Related Benchmarks

### OSWorld-Verified (July 2025)
- Fixed issues reported by the community
- AWS support (evaluation time reduced to approximately 1 hour)
- Updated evaluation results
- **Dataset**: https://huggingface.co/datasets/xlang-ai/OSWorld-Verified

### WebArena
- Only tests web operations, not desktop applications
- **Separate file**: See `WebArena.md`

### GAIA
- Tests comprehensive agent capabilities (including file processing)
- But GAIA does not run in a real OS environment
- **Separate file**: See `GAIA.md`

### Computer Use Arena
- Computer-use evaluation developed by Anthropic
- More focused on real product scenarios

## Why OSWorld Is the Most Important Computer-Use Benchmark

1. **Real Environment**: Not a simulator, runs in a real OS
2. **End-to-End Verification**: Verifies through execution results, not action matching
3. **Cross-Platform**: Supports Ubuntu, Windows, and macOS simultaneously
4. **Industry Standard**: Widely cited in Claude system cards, OpenAI CUA paper, etc.
5. **Clear Human Baseline**: 72.36% human baseline provides a clear reference for progress
6. **Still Challenging**: Top models only recently approached human level in early 2026

## Limitations and Controversies

1. **High Environment Setup Cost**: Requires complete OS virtual environments
2. **Long Runtime**: A single task evaluation may take several minutes
3. **Reproducibility**: Different hardware and environments may lead to different results
4. **Limited Task Count**: 369 tasks, limited statistical confidence
5. **UI Layout Sensitivity**: VLM agents are not robust enough to UI layout changes
6. **Inconsistent SoM Effects**: Visual markers have mixed effects in OS environments depending on the model
7. **Claude Bias**: Claude series performs notably well on OSWorld, raising discussion about whether it was specifically optimized for

## Data Sources / References

- OSWorld paper (NeurIPS 2024): https://arxiv.org/abs/2404.07972
- Project page: http://os-world.github.io/
- GitHub: https://github.com/xlang-ai/osworld
- OSWorld-Verified: https://huggingface.co/datasets/xlang-ai/OSWorld-Verified
- NeurIPS paper: https://proceedings.neurips.cc/paper_files/paper/2024/hash/5d413e48f84dc61244b6be550f1cd8f5-Abstract-Datasets_and_Benchmarks_Track.html
- Claude computer-use progress tracker: https://ai2027-tracker.fly.dev/predictions/osworld-benchmark/
- OSWorld leaderboard: https://airank.dev/benchmarks/os-world