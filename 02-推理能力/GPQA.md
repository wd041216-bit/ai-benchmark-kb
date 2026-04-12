# GPQA — Graduate-Level Google-Proof Q&A

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | Graduate-Level Google-Proof Question Answering Benchmark |
| 创建者 | NYU, Cohen et al. |
| 发布年份 | 2023 |
| 题目数量 | 448 (Diamond 子集) |
| 题型 | 四选一多项选择题 |
| 数据集链接 | https://huggingface.co/datasets/ankner/gpqa |
| 论文链接 | https://arxiv.org/abs/2311.12022 |
| 状态 | ✅ 仍有区分度（top 模型 < 95%） |

## 评测维度

GPQA 专门测试博士级专家知识，题目分布在三大领域：

### 物理 (Physics)
- 量子力学、粒子物理、凝聚态物理、天体物理等
- 约 150 题

### 化学 (Chemistry)
- 有机化学、无机化学、物理化学、生物化学等
- 约 150 题

### 生物 (Biology)
- 分子生物学、遗传学、细胞生物学、生态学等
- 约 150 题

## 核心特点：Google-Proof

**关键创新**：题目设计为即使有互联网搜索也难以找到答案

1. **专家出题**: 每道题由相关领域的博士级专家撰写
2. **同行验证**: 其他领域专家尝试作答，平均正确率仅 34%
3. **抗搜索设计**: 题目不是简单的知识检索，需要推理和整合
4. **高区分度**: 随机猜测 25%，非领域专家 34%，领域专家 65%

## 题目示例

### 物理类
```
Question: In quantum mechanics, which of the following is true about the energy eigenstates of a particle in a one-dimensional infinite potential well?
A) The energy levels are equally spaced
B) The ground state energy is zero
C) The energy spacing increases with quantum number
D) All eigenstates have the same energy
Answer: C
```

### 化学类
```
Question: Which of the following statements about the Diels-Alder reaction is correct?
A) It requires a Lewis acid catalyst
B) It proceeds through a concerted [4+2] cycloaddition mechanism
C) It can only occur with electron-rich dienes
D) The endo product is always the thermodynamic product
Answer: B
```

## 评分方式

- **主要指标**: 准确率 (Accuracy)
- **子集**: Diamond (448题) 是最常用的，经过额外筛选确保题目质量
- **评分方法**: 正确答案占总题数的百分比

## 各模型表现（2026年4月）

| 模型 | GPQA Diamond |
|------|-------------|
| GPT-5.4 | 92.0% |
| Gemini 3 Pro | 94.3% |
| Claude Opus 4.6 | 92.8% |
| GPT-5 | ~88% |
| DeepSeek R1 | ~72% |
| 人类非领域专家 | 34% |
| 人类领域专家 | 65% |
| 随机猜测 | 25% |

## 变体

### GPQA Extended
- 完整数据集，包含更多题目
- 约 544 题

### GPQA Diamond
- 最广泛使用的子集
- 448 题，经过严格质量筛选
- 每道题都有领域专家标注的正确答案

## 为何 GPQA 重要

1. **抗污染**: Google-Proof 设计使其无法通过简单搜索获得答案
2. **高区分度**: 2026年top模型在 90-94%，仍有提升空间
3. **真实难度**: 题目需要真正的领域知识和推理能力
4. **已取代 MMLU**: 在许多技术报告中成为 MMLU 的替代或补充

## 局限性

1. **领域偏窄**: 仅覆盖物理、化学、生物三大领域
2. **题目数量有限**: Diamond 仅 448 题
3. **评分不稳定**: 样本量小导致置信区间较宽
4. **专家标注成本高**: 难以扩展