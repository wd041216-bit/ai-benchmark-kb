# HLE — Humanity's Last Exam

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | Humanity's Last Exam |
| 创建者 | Center for AI Safety & Scale AI |
| 发布年份 | 2025 |
| 题目数量 | 2,500 题 |
| 题型 | 多选 + 开放式 |
| 数据集链接 | https://huggingface.co/datasets/cais/hle |
| 网站 | https://lastexam.ai |
| 状态 | ✅ 极具区分度（top 模型 < 50%） |

## 设计理念

HLE 被称为"人类最后的考试"，专门设计来测试 AI 的极限推理能力：

1. **专家出题**: 由各领域的研究人员撰写
2. **超越训练数据**: 题目需要深层推理，而非简单知识检索
3. **持续更新**: 私有评测集防止数据污染
4. **极高难度**: 2026年4月，最高得分仅 45.9%

## 学科分布

| 学科 | 占比 |
|------|------|
| 数学 | 41% |
| 物理 | 9% |
| 生物/医学 | 11% |
| 人文/社会科学 | 9% |
| 计算机科学 | 8% |
| 化学 | 7% |
| 工程学 | 5% |
| 其他 | 10% |

## 题目示例

### 数学类（高级）
```
Question: Let f: R → R be a continuous function satisfying f(x+y) = f(x) + f(y) + xy for all x,y ∈ R.
If f(1) = 2, what is f(2024)?
```

### 物理类
```
Question: Consider a quantum harmonic oscillator with Hamiltonian H = p²/2m + mω²x²/2.
If the oscillator is initially in the state |ψ(0)⟩ = (|0⟩ + |1⟩)/√2, what is the expectation value of energy at time t = π/(2ω)?
```

## 各模型表现（2026年4月）

| 模型 | HLE 准确率 | 校准误差 |
|------|-----------|---------|
| Gemini 3.1 Pro Preview | 45.90% | 50% |
| Claude Opus 4.6 (Thinking) | 34.44% | 46% |
| GPT-5 Pro | 31.64% | 49% |
| Kimi K2.5 | 24.37% | 67% |
| GLM 4.5 | 8.32% | 79% |
| Llama 4 Maverick | 5.68% | 83% |
| Mistral Medium 3 | 4.52% | 77% |

## 为何 HLE 是最重要的新 Benchmark

1. **未饱和**: 最高分仅 45.9%，远未饱和
2. **抗污染**: 有私有评测集
3. **专家级难度**: 题目需要研究生以上水平的知识
4. **广覆盖**: 涵盖多学科
5. **将成为新标准**: 正在取代 MMLU/GPQA 成为前沿模型的核心 benchmark