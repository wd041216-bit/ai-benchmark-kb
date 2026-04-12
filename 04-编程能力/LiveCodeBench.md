# LiveCodeBench — 实时编程竞赛评测

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | LiveCodeBench |
| 创建者 | LiveCodeBench Team |
| 发布年份 | 2024 |
| 题目数量 | 持续更新（每季度新增） |
| 题型 | 竞赛编程题 |
| 数据集链接 | https://huggingface.co/datasets/LiveCodeBench |
| 网站 | https://livecodebench.github.io |
| 状态 | ✅ 防污染，持续更新 |

## 核心特点

1. **防污染**: 题目从 CodeForces、LeetCode 等竞赛平台实时抓取
2. **持续更新**: 每季度新增题目，模型无法预训练作弊
3. **多语言**: 支持 Python, C++, Java, JavaScript 等
4. **多难度**: Easy / Medium / Hard / Pro

## 与 HumanEval 的对比

| 特性 | HumanEval | LiveCodeBench |
|------|-----------|---------------|
| 题目数 | 164 | 持续增加 |
| 难度 | 简单-中等 | 简单到困难 |
| 防污染 | ❌ | ✅ |
| 真实性 | 手写函数 | 竞赛题目 |
| 饱和度 | 已饱和 | 仍有空间 |

## 各模型表现（2026年4月）

| 模型 | LiveCodeBench (Easy) | LiveCodeBench (Pro) |
|------|---------------------|---------------------|
| GPT-5.4 | ~98% | ~35% |
| Claude Opus 4.6 | ~95% | ~30% |
| Gemini 3 Pro | ~94% | ~28% |

## 关联 Benchmark

### BigCodeBench
- 1,140+ 道真实场景编程题
- 覆盖更多 Python 库和 API
- **链接**: https://huggingface.co/datasets/bigcode/bigcodebench