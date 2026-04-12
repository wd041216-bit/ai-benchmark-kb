# 专业领域 Benchmark 合集

## HealthBench — 医疗知识评测

| 属性 | 值 |
|------|-----|
| 全称 | HealthBench |
| 创建者 | OpenAI 等 |
| 题目数量 | 大规模 |
| 覆盖 | 临床知识、医学推理、患者安全 |
| 状态 | 医疗 AI 评测新标准 |

### 特点
- 医疗知识准确性评估
- 临床推理能力测试
- 患者安全评测

### 各模型表现
| 模型 | HealthBench |
|------|------------|
| GPT-5 | ~48% |
| Claude Opus 4.6 | ~45% |
| Gemini 3 Pro | ~42% |

## DeepSearchQA — 深度搜索问答

| 属性 | 值 |
|------|-----|
| 创建者 | Google DeepMind |
| 题目数量 | 900 |
| 覆盖 | 17 个领域 |
| 特点 | 需要多步搜索规划 |
| 数据集链接 | Kaggle Leaderboard |

### 特点
- 因果链结构：每道题需要多步搜索
- 长程规划：需要跨多个搜索步骤整合信息
- 客观可验证答案

## Chess Text — 国际象棋推理

| 属性 | 值 |
|------|-----|
| 创建者 | Google DeepMind |
| 题型 | 从文本描述推断棋局状态 |
| 评测 | 战略推理能力 |
| 数据集链接 | Kaggle Leaderboard |

### 特点
- 测试模型从自然语言描述中理解空间关系
- 评估战略推理而非棋面记忆
- 使用贝叶斯技能评分系统

## SimpleQA / SimpleQA Verified — 短答案事实性

| 属性 | 值 |
|------|-----|
| 全称 | SimpleQA |
| 创建者 | OpenAI (原始) / Google DeepMind (Verified版) |
| 题目数量 | 1,000 |
| 题型 | 短答案事实性问答 |
| 状态 | 事实性评测标准 |

### SimpleQA Verified 改进
- 修正了原始 SimpleQA 中的标注错误
- 减少了主题偏倚
- 消除了冗余问题
- Kaggle 排行榜托管

### 各模型表现
| 模型 | SimpleQA Verified |
|------|-----------------|
| Gemini 3 Pro | 72.1% |
| GPT-5 | ~65% |
| Claude Opus 4.6 | ~55% |