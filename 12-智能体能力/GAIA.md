# GAIA — General AI Assistants Benchmark

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | GAIA: A Benchmark for General AI Assistants |
| 创建者 | Meta AI, Hugging Face, AutoGPT 等 |
| 发布年份 | 2023 |
| 题目数量 | 466 (3个难度级别) |
| 题型 | 需要推理、工具使用、多步操作的复杂任务 |
| 数据集链接 | https://huggingface.co/datasets/gaia-benchmark/GAIA |
| 论文链接 | https://arxiv.org/abs/2311.12983 |
| GitHub | https://github.com/gaia-benchmark/GAIA |
| 状态 | ✅ 极具区分度（top 模型 < 50%） |

## 评测维度

GAIA 测试 AI 智能体解决真实世界复杂任务的能力：

1. **推理**: 多步逻辑推理
2. **工具使用**: 网页搜索、代码执行、文件处理
3. **信息整合**: 跨多个来源的信息整合
4. **计划与执行**: 制定并执行多步计划
5. **文件处理**: 处理附件（PDF、图片、音频等）

## 难度级别

### Level 1 (一般难度)
- 不需要工具或仅需简单工具
- 约 160 题
- 示例: "2023年诺贝尔物理学奖得主的大学在哪所城市？"

### Level 2 (中等难度)
- 需要使用 1-2 个工具
- 约 153 题
- 示例: "分析附件中的音频文件，识别其中提到的所有鸟的种类，然后计算这些鸟的平均寿命。"

### Level 3 (困难)
- 需要复杂推理和多步工具使用
- 约 153 题
- 示例: "附件包含一个 PDF 文件。提取其中第三页提到的所有公司名称，在 SEC EDGAR 上查找每家公司的最新10-K年报，然后计算这些公司在2023年的总营收。"

## 题目示例

### 简单题 (Level 1)
```
On June 6, 2023, an article in The New York Times mentioned a specific scientific paper.
What was the title of that paper?

Answer: [精确答案]
```

### 中等题 (Level 2)
```
[附件: 一张图片]
The attached image shows a map fragment. What is the name of the country that
is directly south of the highlighted region?

Answer: [精确答案]
```

### 困难题 (Level 3)
```
[附件: 一个 CSV 文件]
The attached CSV file contains weather data. What was the average temperature
on the day when the wind speed was highest, across all weather stations?

Answer: 72.3
```

## 评分方式

- **精确匹配**: 答案必须完全正确
- **分级别评分**: 分别报告 Level 1/2/3 的准确率
- **平均准确率**: 三个级别的加权平均
- **无部分分**: 答案要么完全正确，要么错误

## 各模型表现（2026年4月）

| 模型 | GAIA Overall | Level 1 | Level 2 | Level 3 |
|------|-------------|---------|---------|---------|
| Gemini 3.1 Pro Preview | ~42% | ~70% | ~35% | ~20% |
| Claude Opus 4.6 | ~38% | ~65% | ~30% | ~18% |
| GPT-5 | ~36% | ~62% | ~28% | ~16% |
| DeepSeek R1 | ~22% | ~45% | ~15% | ~5% |
| 人类 | ~92% | ~95% | ~90% | ~88% |

## 为何 GAIA 重要

1. **真实世界任务**: 不像传统 benchmark 那样是简单问答
2. **测试智能体能力**: 需要工具使用和多步规划
3. **极高区分度**: 顶级模型仅 ~40%
4. **文件处理**: 测试多模态输入处理
5. **未来方向**: 代表 AI 发展的方向（从问答到智能体）

## 关联 Benchmark

### RE-Bench
- 测试 AI 代理在真实工作环境中的推理能力
- 包含航空和零售场景

### VisualAgentBench
- 视觉代理评测
- 测试多模态智能体能力

### Tau2
- 多轮代理评测
- 测试在航空和零售领域的代理能力