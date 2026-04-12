# IFEval — Instruction Following Evaluation

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | Instruction Following Evaluation |
| 创建者 | Google (Zhou et al.) |
| 发布年份 | 2023 |
| 题目数量 | 541 |
| 题型 | 带约束条件的指令 |
| 数据集链接 | https://huggingface.co/datasets/google/IFEval |
| 论文链接 | https://arxiv.org/abs/2311.07911 |
| 状态 | ✅ 仍有区分度 |

## 评测维度

IFEval 测试模型是否严格遵循各种格式和内容约束：

### 约束类型

| 约束类别 | 示例 |
|---------|------|
| 关键词约束 | "Include the word 'however' in your response" |
| 长度约束 | "Answer in exactly 3 sentences" |
| 格式约束 | "Format your answer as a JSON object" |
| 语言约束 | "Respond entirely in French" |
| 结构约束 | "Start each paragraph with a number" |
| 内容约束 | "Do not use the word 'the' in your response" |
| 标点约束 | "End your response with a period" |
| 大小写约束 | "Write your entire response in lowercase" |

## 题目示例

### 简单约束
```
Write a poem about the ocean. Your response must contain exactly 4 paragraphs, and each paragraph must start with the word "The".
```

### 复合约束
```
Explain quantum computing in 200 words or less. Your response must:
1. Include the keyword "superposition"
2. Be formatted as a numbered list
3. Not contain any commas
4. End with the phrase "Quantum is the future."
```

### 格式约束
```
Create a JSON object with the following properties:
- name: a fictional character
- age: a number between 20 and 30
- skills: an array of exactly 3 strings
The JSON must be valid and the response should contain nothing else.
```

## 评分方式

- **严格匹配**: 完全按照约束条件评分
- **细粒度评分**: 每个约束独立评分
- **Prompt 级别**: 分为 prompt-level 和 instance-level 严格率
- **自动评分**: 无需 LLM 评判，纯规则验证

## 各模型表现（2026年4月）

| 模型 | IFEval 严格率 |
|------|-------------|
| GPT-5.2-Codex | ~85% |
| Claude Sonnet 4.5 | ~84% |
| Gemini 3 Pro | ~82% |
| DeepSeek V3 | ~78% |
| Llama 4 Maverick | ~72% |

## 变体

### IFBench
- IFEval 的更新版本
- 更多约束类型和更复杂的组合
- 2025年发布

### 关联 Benchmark
- **MT-Bench**: 多轮指令跟随（侧重对话质量）
- **AlpacaEval**: 指令跟随的自动评估

## 为何 IFEval 重要

1. **实用价值**: 指令跟随是 LLM 在生产环境中最关键的能力
2. **自动评分**: 无需 LLM 评判，评分客观
3. **细粒度**: 可以分析模型在哪些约束上失败
4. **可复现**: 评分完全确定性

## 局限性

1. **过于机械**: 严格匹配可能惩罚合理的回答
2. **格式偏重**: 更关注格式而非内容质量
3. **约束组合**: 复合约束测试可能超出实际需求
4. **英语中心**: 主要测试英语指令