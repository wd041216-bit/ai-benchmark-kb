# Chatbot Arena — 聊天机器人竞技场

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | LMSYS Chatbot Arena |
| 创建者 | LMSYS (UC Berkeley, UCSD, CMU) |
| 发布年份 | 2023 |
| 评测方式 | 人类偏好对比 (Elo Rating) |
| 网站链接 | https://chat.lmsys.org |
| 论文链接 | https://arxiv.org/abs/2403.04132 |
| 状态 | ✅ 最受信任的 LLM 评测标准 |

## 核心机制

### Elo 评分系统
- 用户输入一个 prompt
- 两个匿名模型同时回答
- 用户投票选择更好的回答
- 系统根据结果更新 Elo 评分
- 500万+ 真实用户对比投票

### 评测类别

| 类别 | 说明 |
|------|------|
| Overall | 综合排名 |
| Coding | 编程能力 |
| Math | 数学能力 |
| Hard Prompts | 困难提示 |
| Vision | 视觉理解 |
| Long Context | 长上下文 |
| Creative Writing | 创意写作 |
| Instruction Following | 指令跟随 |

## 2026年4月排名（综合）

| 排名 | 模型 | Elo 评分 |
|------|------|---------|
| 1 | GPT-5 | ~1350 |
| 2 | Gemini 3 Pro | ~1340 |
| 3 | Claude Opus 4.6 | ~1330 |
| 4 | Claude Sonnet 4.5 | ~1310 |
| 5 | Grok 4 | ~1300 |

## Arena-Hard-Auto

- Chatbot Arena 的自动化版本
- 使用 GPT-4 作为评判模型
- 80+ 编程和调试问题
- 与人类偏好的相关性: 0.97
- **数据集**: https://github.com/lm-sys/arena-hard-auto

## WildBench

- Allen AI 开发
- 使用真实用户查询（来自 WildChat 数据集）
- LLM-as-Judge 评分
- 更贴近真实使用场景

## MixEval / MixEval-Hard

- 动态评测，从多个来源自动收集题目
- MixEval-Hard 是困难版本
- 与 Chatbot Arena 排名高度相关

## 为何 Chatbot Arena 重要

1. **最接近真实使用场景**: 基于真实用户偏好
2. **防污染**: 模型无法预训练作弊
3. **持续更新**: 实时反映最新模型表现
4. **多维度**: 覆盖编程、数学、创意等多个子类别
5. **广泛认可**: 所有主流 AI 公司都引用 Arena 排名

## 局限性

1. **偏好偏差**: 人类偏好可能偏向冗长、自信的回答
2. **匿名问题**: 模型特征可能泄露身份
3. **投票质量**: 非专家投票可能不准确
4. **覆盖不均**: 编程和数学问题占比较高
5. **无法离线评测**: 必须在线运行