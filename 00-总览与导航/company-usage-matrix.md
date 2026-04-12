# 各公司 Benchmark 使用对照表

## OpenAI

| Benchmark | 使用场景 | 数据集链接 |
|-----------|---------|-----------|
| MMLU / MMLU-Pro | 知识理解 | https://huggingface.co/datasets/cais/mmlu |
| GSM8K | 数学推理 | https://huggingface.co/datasets/openai/gsm8k |
| MATH / MATH-500 | 竞赛数学 | https://huggingface.co/datasets/HuggingFaceH4/MATH-500 |
| HumanEval | 代码生成 | https://huggingface.co/datasets/openai/openai_humaneval |
| SWE-bench Verified | 软件工程 | https://www.swebench.com |
| GPQA Diamond | 博士级推理 | https://huggingface.co/datasets/ankner/gpqa |
| ARC-AGI-2 | 抽象推理 | https://arcprize.org |
| SimpleQA / SimpleQA Verified | 事实性 | OpenAI 发布 |
| Chatbot Arena | 人类偏好 | https://chat.lmsys.org |
| AIME 2024/2025 | 数学邀请赛 | https://artificialanalysis.ai |
| IFEval | 指令跟随 | https://huggingface.co/datasets/google/IFEval |
| MRCR (128k) | 长上下文推理 | OpenAI 发布 |

## Anthropic (Claude)

| Benchmark | 使用场景 | 数据集链接 |
|-----------|---------|-----------|
| MMLU / MMLU-Pro | 知识理解 | 同上 |
| GSM8K | 数学推理 | 同上 |
| MATH | 竞赛数学 | 同上 |
| HumanEval / HumanEval+ | 代码生成 | 同上 |
| SWE-bench Verified / SWE-bench Pro | 软件工程 | 同上 |
| GPQA Diamond | 博士级推理 | 同上 |
| IFEval | 指令跟随 | 同上 |
| Chatbot Arena | 人类偏好 | 同上 |
| HLE | 人类最后考试 | https://huggingface.co/datasets/cais/hle |
| BigBench Hard | 困难推理 | https://huggingface.co/datasets/lukaemon/bbh |
| BFCL v3 | 函数调用 | https://gorilla.cs.berkeley.edu/leaderboard.html |

## Google DeepMind (Gemini)

| Benchmark | 使用场景 | 数据集链接 |
|-----------|---------|-----------|
| MMLU / MMLU-Pro | 知识理解 | 同上 |
| GSM8K / MATH | 数学推理 | 同上 |
| HumanEval | 代码生成 | 同上 |
| SWE-bench | 软件工程 | 同上 |
| GPQA Diamond | 博士级推理 | 同上 |
| FACTS Grounding / FACTS Suite | 事实性（自研） | https://www.kaggle.com/benchmarks/google/facts |
| SimpleQA Verified | 事实性 | Kaggle Leaderboard |
| MRCR v2 | 长上下文推理（自研） | Google DeepMind 发布 |
| DeepSearchQA | 深度搜索问答（自研） | Kaggle Leaderboard |
| Chess Text | 棋类推理（自研） | Kaggle Leaderboard |
| MMMU | 多模态理解 | https://huggingface.co/datasets/MMMU/MMMU |
| Chatbot Arena | 人类偏好 | 同上 |

## Meta (Llama)

| Benchmark | 使用场景 | 数据集链接 |
|-----------|---------|-----------|
| MMLU | 知识理解 | 同上 |
| GSM8K | 数学推理 | 同上 |
| MATH | 竞赛数学 | 同上 |
| HumanEval | 代码生成 | 同上 |
| HellaSwag | 常识推理 | https://huggingface.co/datasets/Rowan/hellaswag |
| ARC-Challenge | 推理 | https://huggingface.co/datasets/allenai/ai2_arc |
| TruthfulQA | 真实性 | https://huggingface.co/datasets/truthfulqa/truthful_qa |
| WinoGrande | 共指推理 | https://huggingface.co/datasets/winogrande/winogrande_xl |
| PIQA | 物理直觉 | https://huggingface.co/datasets/piqa |
| DROP | 阅读理解 | https://huggingface.co/datasets/drop |

## Mistral

| Benchmark | 使用场景 | 数据集链接 |
|-----------|---------|-----------|
| MMLU | 知识理解 | 同上 |
| GSM8K | 数学推理 | 同上 |
| HumanEval | 代码生成 | 同上 |
| MBPP | 基础编程 | https://huggingface.co/datasets/google-research-datasets/mbpp |
| HellaSwag | 常识推理 | 同上 |
| ARC | 推理 | 同上 |

## DeepSeek

| Benchmark | 使用场景 | 数据集链接 |
|-----------|---------|-----------|
| MMLU / MMLU-Pro | 知识理解 | 同上 |
| GSM8K / MATH | 数学推理 | 同上 |
| HumanEval | 代码生成 | 同上 |
| AIME 2024/2025 | 数学邀请赛 | 同上 |
| CodeForces | 竞赛编程 | LiveCodeBench |
| SWE-bench Verified | 软件工程 | 同上 |

## 跨公司 Benchmark 使用频率排名

| 排名 | Benchmark | 使用公司数 | 核心程度 |
|------|-----------|-----------|---------|
| 1 | MMLU / MMLU-Pro | 6/6 | 必选 |
| 2 | GSM8K | 6/6 | 必选 |
| 3 | HumanEval | 6/6 | 必选 |
| 4 | MATH | 5/6 | 核心 |
| 5 | SWE-bench | 4/6 | 核心 |
| 6 | GPQA Diamond | 4/6 | 核心 |
| 7 | HellaSwag | 3/6 | 常用 |
| 8 | ARC-Challenge | 3/6 | 常用 |
| 9 | IFEval | 3/6 | 常用 |
| 10 | Chatbot Arena | 4/6 | 核心 |
| 11 | TruthfulQA | 2/6 | 常用 |
| 12 | AIME | 3/6 | 新兴 |