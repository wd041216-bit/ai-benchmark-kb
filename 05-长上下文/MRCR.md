# 长上下文 Benchmark 合集

## MRCR v2 — 多轮共指消解

| 属性 | 值 |
|------|-----|
| 全称 | Multi-Round Coreference Resolution v2 |
| 创建者 | Google DeepMind |
| 发布年份 | 2024 |
| 题型 | 长文本中的指代消解 |
| 数据集链接 | Google DeepMind 发布 |
| 状态 | 测试长上下文推理能力 |

### 特点
- 测试模型在 128K+ token 长文本中追踪指代关系
- 多轮共指消解需要跨越长距离理解上下文
- v2 版本增加了难度和长度泛化测试

## AA-LCR — 长上下文推理

| 属性 | 值 |
|------|-----|
| 全称 | Artificial Analysis Long Context Reasoning |
| 创建者 | Artificial Analysis |
| 发布年份 | 2025 |
| 题目数量 | 100 题 |
| 特点 | 10K-100K token 文档推理 |
| 数据集链接 | https://huggingface.co/datasets/ArtificialAnalysis/AA-LCR |

### 特点
- 测试模型在 10K 到 100K token 长文档中的信息提取和推理能力
- 100 道精心设计的长上下文问题
- 当前最佳模型仅达到 76%

## RULER — 长文本检索与推理

| 属性 | 值 |
|------|-----|
| 全称 | Retrieval Under Long-Extensive Requirements |
| 创建者 | NVIDIA |
| 发布年份 | 2024 |
| 题型 | 长文本中的信息检索 |
| 状态 | 评估长上下文窗口的检索能力 |

### 特点
- 测试模型在不同上下文长度下的信息检索能力
- 从 4K 到 128K token 递增测试
- 包括 Needle-in-a-Haystack 等经典长上下文测试

## 各模型长上下文表现

| 模型 | 128K 窗口 | 256K 窗口 | 1M 窗口 |
|------|----------|----------|---------|
| Gemini 3 Pro | 优秀 | 优秀 | 优秀 |
| GPT-5 | 良好 | 良好 | 有限 |
| Claude Opus 4.6 | 良好 | 良好 | 有限 |
| Gemini 2.5 Pro | 良好 | 良好 | 良好 |