# AI Benchmark 全景图与分类体系

## 演进历史

### 第一代（2020-2022）：基础能力评测
- **GLUE / SuperGLUE**：自然语言理解基石
- **MMLU**（2021）：57学科知识评测，成为最广泛使用的 LLM benchmark
- **HumanEval**（2021）：164 道手写编程题
- **GSM8K**（2021）：小学数学推理

### 第二代（2022-2024）：推理与专业性提升
- **BIG-bench Hard**：从 204 个任务中精选困难子集
- **GPQA Diamond**：研究生级专家问答，抗作弊设计
- **SWE-bench**（2023）：真实 GitHub Issue 修复
- **MATH**：竞赛级数学推理
- **MMLU-Pro**：MMLU 专业加强版

### 第三代（2024-2026）：前沿与智能体评测
- **ARC-AGI-2**：抽象推理，测试通用智能
- **Humanity's Last Exam**：专家级难题，当前最高得分为 45.9%
- **SWE-bench Live**：持续更新的编程 benchmark
- **FACTS Benchmark Suite**：多维度事实性评测
- **Chatbot Arena**：基于人类偏好的实时排行

## 分类维度

### 按能力维度

```
能力维度
├── 知识广度 (Breadth)
│   ├── MMLU / MMLU-Pro — 57学科知识
│   ├── BIG-bench — 204任务综合
│   ├── C-Eval — 中文52学科
│   └── MMMLU — 14语言知识
├── 推理深度 (Depth)
│   ├── GPQA Diamond — 博士级推理
│   ├── ARC-AGI — 抽象推理
│   ├── HLE — 人类最后考试
│   └── BIG-bench Hard — 困难推理
├── 数学推理 (Math)
│   ├── GSM8K — 小学数学
│   ├── MATH — 竞赛数学
│   ├── AIME — 数学邀请赛
│   └── FrontierMath — 前沿数学
├── 编程 (Code)
│   ├── HumanEval — 函数级代码生成
│   ├── SWE-bench — 真实Issue修复
│   ├── LiveCodeBench — 竞赛编程
│   └── BigCodeBench — 大规模代码
├── 长上下文 (Long Context)
│   ├── MRCR v2 — 多轮共指消解
│   ├── AA-LCR — 100K token 推理
│   └── RULER — 长文本检索
├── 指令跟随 (IF)
│   ├── IFEval / IFBench — 格式约束
│   └── MT-Bench — 多轮指令
├── 事实性 (Factuality)
│   ├── TruthfulQA — 真实性
│   ├── SimpleQA Verified — 短答案事实
│   └── FACTS — 多维事实性
├── 安全对齐 (Safety)
│   ├── Anthropic HH — 有用无害
│   ├── WMDP — 武器知识防护
│   └── ToxiGen — 毒性检测
└── 智能体 (Agent)
    ├── GAIA — 通用AI助手
    ├── BFCL — 函数调用
    └── RE-Bench — 代理推理
```

### 按难度层级

| 难度层 | Benchmark | 人类基线 | 前沿模型表现 |
|--------|-----------|----------|-------------|
| 基础 | MMLU, HellaSwag, ARC-Easy | ~88% | ~94%（已饱和） |
| 中级 | GSM8K, HumanEval, MMLU-Pro | ~98%/N/A | ~96%/~95% |
| 困难 | GPQA Diamond, SWE-bench Verified | 65%（专家） | ~79% |
| 极难 | HLE, ARC-AGI-2, AIME 2025 | ~90%/~0% | ~46%/~5%/~43% |
| 前沿 | FrontierMath, SWE-bench Pro | N/A | <10% |

## Benchmark 饱和度分析（2026年4月）

### 已饱和（top 模型 > 90%）
- MMLU, HellaSwag, ARC-Easy, GSM8K, HumanEval

### 接近饱和（75-90%）
- MMLU-Pro, GPQA Diamond, SWE-bench Verified

### 仍有空间（50-75%）
- SWE-bench Pro, FACTS Suite, LiveCodeBench Pro

### 远未饱和（< 50%）
- HLE, ARC-AGI-2, FrontierMath, AIME 2025

## Benchmark 污染问题

"benchmaxxxing" 现象：当某个 benchmark 成为行业标准时，模型开始针对其优化，导致：
1. 训练数据中包含 benchmark 题目
2. 针对特定格式优化而非真正能力提升
3. 分数虚高但实际应用表现不佳

### 对策
- **Live 系列基准**（LiveCodeBench, SWE-bench Live）：持续更新，防污染
- **私有评测集**：保留隐藏测试数据
- **GPQA Diamond**：题目 Google 不可搜
- **Chatbot Arena**：基于真实人类偏好，无法预训练作弊