# HellaSwag — 常识推理评测

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | HellaSwag: Can a Machine Really Finish Your Sentence? |
| 创建者 | University of Washington (Zellers et al.) |
| 发布年份 | 2019 |
| 题目数量 | 10,042 (测试集) |
| 题型 | 四选一句子补全 |
| 数据集链接 | https://huggingface.co/datasets/Rowan/hellaswag |
| 论文链接 | https://arxiv.org/abs/1905.07830 |
| 状态 | ⚠️ 已饱和（top 模型 > 95%） |

## 评测维度

测试常识推理和物理世界理解：
- 事件续写：给定描述，选择最合理的后续
- 物理常识：理解物体如何运动和交互
- 社会常识：理解社会情境中的行为

## 题目示例

```
A woman is seen walking into a room with a broom. She...
A) starts sweeping the floor with the broom ✓
B) drives a car down the highway ✗
C) cooks a meal in the kitchen ✗
D) swims in the ocean ✗
```

## 各模型表现

| 模型 | HellaSwag |
|------|----------|
| GPT-5 | ~98% |
| Claude Opus 4.6 | ~97% |
| Gemini 3 Pro | ~97% |
| 人类 | ~95% |

## 局限性

1. **已饱和**: 顶级模型超过人类基线
2. **格式简单**: 四选一使随机基线就有 25%
3. **推荐替代**: 使用 GPQA、HLE 等更难的推理基准