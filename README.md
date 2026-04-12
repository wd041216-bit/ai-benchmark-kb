# AI Benchmark 知识库

> 全面收录各大 AI 公司用来测试模型性能的 Benchmark 题库完整集合

## 概述

本知识库系统性地整理了当前 AI 行业主流评测基准（Benchmark），涵盖 OpenAI、Anthropic、Google DeepMind、Meta、Mistral 等公司在其技术报告中使用的所有重要评测集。

## 目录结构

```
ai-benchmark-kb/
├── README.md                    # 本文件 — 总览与导航
├── 00-总览与导航/
│   ├── benchmark-landscape.md   # Benchmark 全景图与分类体系
│   ├── evaluation-frameworks.md # 评测框架与工具
│   └── company-usage-matrix.md # 各公司使用的 Benchmark 对照表
├── 01-综合知识理解/
│   ├── MMLU.md                  # Massive Multitask Language Understanding
│   ├── MMLU-Pro.md              # MMLU 专业级
│   ├── BIG-bench.md             # Beyond the Imitation Game
│   ├── ARC.md                   # AI2 Reasoning Challenge
│   ├── HellaSwag.md             # 常识推理
│   ├── C-Eval.md                # 中文综合评测
│   └── MMMLU.md                 # 多语言 MMLU
├── 02-推理能力/
│   ├── GPQA.md                  # Graduate-Level Google-Proof Q&A
│   ├── ARC-AGI.md               # 抽象推理语料库
│   ├── HLE.md                   # Humanity's Last Exam
│   ├── WinoGrande.md            # 共指消解推理
│   ├── PIQA.md                  # 物理直觉问答
│   └── SIQA.md                  # 社会交互问答
├── 03-数学推理/
│   ├── GSM8K.md                 # 小学数学 8K
│   ├── MATH.md                  # 竞赛数学
│   ├── Minerva-Math.md          # DeepMind 数学评测
│   └── MATH-500.md              # MATH 精选 500 题
├── 04-编程能力/
│   ├── HumanEval.md             # OpenAI 164 道编程题
│   ├── MBPP.md                  # Most Basic Python Problems
│   ├── SWE-bench.md             # 真实 GitHub Issue 修复
│   ├── LiveCodeBench.md         # 实时编程竞赛题
│   └── BigCodeBench.md          # 大规模代码评测
├── 05-长上下文/
│   ├── MRCR.md                  # 多轮共指消解
│   ├── AA-LCR.md                # 长上下文推理
│   └── RULER.md                 # 长文本检索与推理
├── 06-指令跟随/
│   ├── IFEval.md                # Instruction Following Evaluation
│   ├── MT-Bench.md              # 多轮对话评测
│   └── AlpacaEval.md            # Alpaca 评测
├── 07-真实性与事实性/
│   ├── TruthfulQA.md            # 真实性问答
│   ├── SimpleQA.md              # 简短事实性问答
│   └── FACTS.md                 # Google DeepMind 事实性评测套件
├── 08-安全与对齐/
│   ├── Anthropic-HH.md          # Helpful & Harmless
│   ├── RealToxicityPrompts.md   # 毒性提示评测
│   ├── ToxiGen.md               # 隐性毒性检测
│   └── WMDP.md                  # 大规模杀伤性武器防护
├── 09-多模态理解/
│   ├── MMMU.md                  # 多学科多模态理解
│   ├── VQAv2.md                 # 视觉问答 v2
│   └── MVBench.md               # 视频理解评测
├── 10-对话与生成/
│   ├── Chatbot-Arena.md         # 聊天机器人竞技场
│   ├── WildBench.md             # 野外评测
│   └── MixEval.md               # 混合评测
├── 11-嵌入与检索/
│   ├── MTEB.md                  # 大规模文本嵌入评测
│   └── BEIR.md                  # 信息检索评测
├── 12-智能体能力/
│   ├── GAIA.md                  # 通用 AI 助手评测
│   ├── RE-Bench.md              # 代理推理评测
│   ├── BFCL.md                  # 伯克利函数调用评测
│   └── Tau2.md                  # 多轮代理评测
├── 13-专业领域/
│   ├── HealthBench.md           # 医疗评测
│   ├── DeepSearchQA.md          # 深度搜索问答
│   └── Chess-Text.md            # 国际象棋推理
└── 14-竞赛级数学/
    ├── AIME.md                  # 美国数学邀请赛
    └── FrontierMath.md          # 前沿数学评测
```

## Benchmark 分类速查

| 类别 | 代表性 Benchmark | 核心评测维度 |
|------|------------------|-------------|
| 综合知识 | MMLU, MMLU-Pro, BIG-bench | 学科知识覆盖度 |
| 推理 | GPQA, ARC-AGI, HLE | 深度推理与泛化 |
| 数学 | GSM8K, MATH, AIME | 数学问题求解 |
| 编程 | HumanEval, SWE-bench, LiveCodeBench | 代码生成与软件工程 |
| 长上下文 | MRCR, AA-LCR, RULER | 长文本理解与推理 |
| 指令跟随 | IFEval, MT-Bench | 格式/约束遵从性 |
| 事实性 | TruthfulQA, FACTS, SimpleQA | 事实准确度与幻觉 |
| 安全对齐 | Anthropic HH, WMDP | 安全性与对齐度 |
| 多模态 | MMMU, VQAv2 | 图文联合理解 |
| 对话生成 | Chatbot Arena, WildBench | 人类偏好对齐 |
| 智能体 | GAIA, BFCL, RE-Bench | 代理工具使用能力 |

## 主要使用方对照

| 公司 | 核心技术报告使用的 Benchmark |
|------|------------------------------|
| OpenAI | MMLU, MMLU-Pro, GSM8K, MATH, HumanEval, SWE-bench, GPQA, ARC-AGI, SimpleQA, Chatbot Arena |
| Anthropic | MMLU, GSM8K, MATH, HumanEval, SWE-bench, GPQA, IFEval, Chatbot Arena, HLE |
| Google DeepMind | MMLU, GSM8K, MATH, HumanEval, SWE-bench, GPQA, FACTS, SimpleQA Verified, MRCR, Chess Text |
| Meta (Llama) | MMLU, GSM8K, MATH, HumanEval, HellaSwag, ARC, TruthfulQA, WinoGrande |
| Mistral | MMLU, GSM8K, HumanEval, MBPP, HellaSwag, ARC |
| DeepSeek | MMLU, GSM8K, MATH, HumanEval, AIME, CodeForces |

## 数据来源

- HuggingFace Datasets: https://huggingface.co/datasets
- EleutherAI lm-eval-harness: https://github.com/EleutherAI/lm-evaluation-harness
- Stanford HELM: https://crfm.stanford.edu/helm/
- Stanford AI Index Report 2025: https://hai.stanford.edu/ai-index-report
- Scale AI Leaderboards: https://scale.com/leaderboard
- Artificial Analysis: https://artificialanalysis.ai/

## 版本信息

- 创建日期: 2026-04-12
- 最后更新: 2026-04-12
- 数据截止: 2026年4月