# FACTS — 多维事实性评测套件

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | FACTS Benchmark Suite |
| 创建者 | Google DeepMind & Kaggle |
| 发布年份 | 2024 (Grounding), 2025 (Suite) |
| 题目数量 | 3,513（四个子集合计） |
| 题型 | 事实性问答（多选 + 开放式） |
| 网站链接 | https://www.kaggle.com/benchmarks/google/facts |
| 论文链接 | FACTS Grounding (2024), FACTS Suite (2025) |
| 状态 | ✅ 仍有区分度（top 模型 < 70%） |

## 四大子基准

### 1. FACTS Grounding v2（文档基础性）
- **测试内容**: 给定长文档，回答问题并确保答案完全基于文档
- **题目数量**: 860 (公开) + 859 (私有)
- **文档长度**: 最长 32,000 tokens
- **覆盖领域**: 金融、技术、零售、医疗、法律
- **任务类型**: 摘要、问答、改写

### 2. FACTS Parametric（参数知识）
- **测试内容**: 不使用任何外部工具，仅凭模型内部知识回答事实性问题
- **题目数量**: 1,052 (公开) + 1,052 (私有)
- **题目类型**: 百科全书式问答
- **特点**: 测试模型的"知识记忆"准确性

### 3. FACTS Search（搜索增强）
- **测试内容**: 模型可使用网络搜索 API 回答事实性问题
- **题目数量**: 890 (公开) + 994 (私有)
- **特点**: 需要多步搜索和信息整合
- **搜索工具**: 统一提供，确保公平比较

### 4. FACTS Multimodal（多模态事实性）
- **测试内容**: 基于图像的事实性问答
- **题目数量**: 711 (公开) + 811 (私有)
- **图像类型**: 照片、图表、地图等
- **特点**: 测试视觉理解与事实知识的结合

## 评分方式

- **自动评分**: 使用三个前沿 LLM 作为评判
  - Gemini 1.5 Pro
  - GPT-4o
  - Claude 3.5 Sonnet
- **FACTS Score**: 四个子基准的平均准确率（公开+私有）
- **私有集合**: 由 Kaggle 管理，防止数据污染

## 各模型表现（2025年12月）

| 模型 | FACTS Score | Grounding | Multimodal | Parametric | Search |
|------|------------|-----------|------------|------------|--------|
| Gemini 3 Pro | 68.8 | 69.0 | 46.1 | 76.4 | 83.8 |
| Gemini 2.5 Pro | 62.1 | 74.2 | 46.9 | 63.2 | 63.9 |
| GPT 5 | 61.8 | 69.6 | 44.1 | 55.8 | 77.7 |
| Grok 4 | 53.6 | 54.7 | 25.7 | 58.6 | 75.3 |
| GPT o3 | 52.0 | 36.2 | 39.9 | 57.1 | 74.8 |
| Claude 4.5 Opus | 51.3 | 62.1 | 39.2 | 30.6 | 73.2 |
| GPT 4.1 | 50.5 | 45.6 | 40.1 | 51.5 | 64.6 |

## 关键发现

1. **搜索增强显著提升**: 所有模型在 Search 子集上表现最好
2. **多模态最难**: 所有模型在 Multimodal 子集上得分最低（< 50%）
3. **参数知识差异大**: Gemini 3 Pro 在 Parametric 上领先 GPT o3 近 20%
4. **Grounding 能力各异**: Gemini 2.5 Pro 在 Grounding 上最强

## 题目示例

### FACTS Grounding
```
Document: [30页金融报告]
Question: What was the company's revenue growth rate in Q3 2024?
Instructions: Answer based ONLY on the provided document.
```

### FACTS Parametric
```
Question: What is the chemical symbol for the element with atomic number 79?
Answer: Au (Gold)
```

### FACTS Search
```
Question: Who won the Nobel Prize in Physics in 2024?
Instructions: Use the provided search API to find the answer.
```

### FACTS Multimodal
```
[Image: A complex scientific diagram]
Question: What does the y-axis represent in this figure?
```

## 为何 FACTS 重要

1. **全面性**: 唯一同时评估参数知识、搜索增强、文档基础和多模态事实性的 benchmark
2. **防污染**: 公开+私有双集合
3. **自动评分**: 多 LLM 评判减少偏见
4. **实时排名**: Kaggle 实时更新排行榜

## 与 SimpleQA 的关系

- SimpleQA (OpenAI) 仅评估短答案事实性
- SimpleQA Verified (Google DeepMind) 改进了 SimpleQA 的标注质量问题
- FACTS 是更全面的事实性评估