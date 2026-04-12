# 新兴与前沿 Benchmark

## 2025-2026 年新趋势

### 1. 持续更新型 Benchmark
- **SWE-bench Live**: 每月自动从 GitHub 收集新 Issue
- **LiveCodeBench**: 从编程竞赛平台实时抓取新题
- **趋势**: 防止训练数据污染，保持评测有效性

### 2. 智能体能力评测
- **GAIA**: 通用 AI 助手评测
- **RE-Bench**: 代理推理评测
- **BFCL v3**: 函数调用能力评测
- **Tau2**: 多轮代理评测
- **趋势**: 从单次问答转向多步骤任务完成

### 3. 事实性评测深化
- **FACTS Suite**: 四维事实性评测
- **SimpleQA Verified**: 改进的短答案事实性
- **DeepSearchQA**: 多步搜索推理
- **趋势**: 从简单问答到搜索增强和文档基础性

### 4. 长上下文评测
- **MRCR v2**: 多轮共指消解
- **AA-LCR**: 100K token 推理
- **趋势**: 从 4K 到 1M+ token 的推理能力评测

### 5. 竞赛数学评测
- **AIME 2024/2025**: 每年新题目
- **FrontierMath**: 专业数学家出题
- **HMMT**: 哈佛-MIT 数学竞赛
- **趋势**: 难度不断提升，区分度保持

### 6. 多模态评测扩展
- **MMMU**: 多学科多模态
- **FACTS Multimodal**: 多模态事实性
- **趋势**: 从纯文本到图文、视频理解

## 即将出现的 Benchmark

| 名称 | 领域 | 预期发布 |
|------|------|---------|
| ARC-AGI-3 | 抽象推理 | 2026 |
| SWE-bench Live Windows | Windows 编程 | 2026 |
| SWE-bench Live MultiLang | 多语言编程 | 2026 |
| 多个新 Live benchmark | 各领域 | 持续 |

## 已淘汰的 Benchmark

以下 benchmark 因饱和或质量问题，不再推荐用于前沿模型评测：

| Benchmark | 淘汰原因 | 替代 |
|-----------|---------|------|
| GLUE | 已饱和 | SuperGLUE |
| SuperGLUE | 接近饱和 | MMLU-Pro |
| MMLU (原始) | 接近饱和 | MMLU-Pro |
| HumanEval | 已饱和 | SWE-bench Live |
| GSM8K | 接近饱和 | MATH-500 |
| HellaSwag | 已饱和 | GPQA Diamond |
| ARC-Challenge | 接近饱和 | HLE |

## 评测趋势总结

1. **从静态到动态**: 静态 benchmark → 持续更新的 Live benchmark
2. **从简单到复杂**: 单步问答 → 多步推理与工具使用
3. **从通用到专业**: 通用 benchmark → 领域专业 benchmark
4. **从自动到人本**: 自动评测 → 人类偏好评测（Chatbot Arena）
5. **从单模态到多模态**: 纯文本 → 图文音视频