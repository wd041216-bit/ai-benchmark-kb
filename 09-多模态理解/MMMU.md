# MMMU — 多学科多模态理解评测

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | A Massive Multi-discipline Multimodal Understanding and Reasoning Benchmark |
| 创建者 | NYU, CMU, UW-Madison 等 |
| 发布年份 | 2024 |
| 题目数量 | 11,500+（30个学科） |
| 题型 | 多项选择题（含图像） |
| 数据集链接 | https://huggingface.co/datasets/MMMU/MMMU |
| 论文链接 | https://arxiv.org/abs/2311.16502 |
| 状态 | ✅ 仍有区分度 |

## 评测维度

测试视觉+语言的联合理解能力，覆盖6个大学级别学科群：

1. **艺术与设计**: 艺术史、设计理论
2. **商业**: 会计、经济、金融、管理、营销
3. **科学**: 生物、化学、地理、物理
4. **健康与医学**: 临床医学、公共卫生
5. **人文与社会科学**: 历史、社会学、心理学
6. **技术与工程**: 计算机科学、电气工程、机械工程

## 题目示例

### 化学类
```
[图像：一个化学反应的分子结构图]
Based on the molecular structure shown, which functional group is highlighted?
A) Hydroxyl  B) Carbonyl  C) Carboxyl  D) Amino

Answer: C
```

### 医学类
```
[图像：一张胸部X光片]
This chest X-ray most likely shows which of the following conditions?
A) Pneumonia  B) Pleural effusion  C) Normal  D) Lung cancer

Answer: A
```

## 各模型表现（2026年4月）

| 模型 | MMMU |
|------|------|
| o4 Mini High | 79.2% |
| GPT-5 | 79.1% |
| Gemini 3 Pro | ~70% |
| Claude Opus 4.6 | ~65% |
| 人类专家 | ~85% |

## 关联 Benchmark

### VQAv2
- 265K 图像 + 3M 问题
- 视觉问答标准基准
- **链接**: https://huggingface.co/datasets/lmms-lab/vqav2

### MVBench
- 视频理解评测
- 20 个子任务涵盖时空推理
- **链接**: https://huggingface.co/datasets/OpenGVLab/MVBench