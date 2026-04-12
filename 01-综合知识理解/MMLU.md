# MMLU — Massive Multitask Language Understanding

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | Massive Multitask Language Understanding |
| 创建者 | Dan Hendrycks 等 (UC Berkeley) |
| 发布年份 | 2021 |
| 题目数量 | 15,908（57个学科） |
| 题型 | 四选一多项选择题 |
| 数据集链接 | https://huggingface.co/datasets/cais/mmlu |
| 论文链接 | https://arxiv.org/abs/2009.03300 |
| GitHub | https://github.com/hendrycks/test |
| 状态 | ⚠️ 接近饱和（top 模型 > 90%） |

## 评测维度

覆盖 57 个学科，分为四大类：

### STEM (科学、技术、工程、数学)
- 数学：初等数学、高等数学、抽象代数、大学数学
- 物理：高中物理、大学物理、概念物理
- 计算机：高中计算机科学、大学计算机科学、计算机安全、机器学习
- 生物：高中生物、大学生物、解剖学、病毒学
- 化学：高中化学、大学化学

### 人文科学
- 历史：高中欧洲史、高中美国史、高中世界史、史前史
- 哲学：哲学、道德争议、道德情境、逻辑谬误、形式逻辑
- 语言：世界宗教

### 社会科学
- 政治：高中政府与政治、美国外交政策、安全研究
- 经济：高中微观经济学、高中宏观经济学、计量经济学
- 心理：高中心理学、专业心理学、人类衰老、人类性学
- 社会学、营销学、公共关系、管理学

### 其他专业领域
- 法律：法学、专业法律、国际法
- 医学：临床知识、专业医学、医学遗传学、营养学
- 会计：专业会计、商业伦理
- 工程：电气工程

## 题目示例

### 数学类
```
Question: If f(x) = x^2 + 3x + 2, then f(x+1) =
A) x^2 + 5x + 6
B) x^2 + 5x + 4
C) x^2 + 3x + 6
D) x^2 + 3x + 4
Answer: A
```

### 法律类
```
Question: Which of the following is a necessary element for a valid contract?
A) Written documentation
B) Consideration
C) Notarization
D) Witness signatures
Answer: B
```

### 计算机科学类
```
Question: What is the worst-case time complexity of quicksort?
A) O(n)
B) O(n log n)
C) O(n^2)
D) O(2^n)
Answer: C
```

## 评分方式

- **主要指标**: 准确率（Accuracy）
- **评分方法**: 正确答案占总题数的百分比
- **Few-shot 设置**: 通常使用 5-shot
- **随机基线**: 25%（四选一）

## 各模型表现（2026年4月）

| 模型 | 5-shot 准确率 |
|------|-------------|
| GPT-5 | 94.2% |
| Claude Opus 4.6 | ~93% |
| Gemini 3 Pro | ~92% |
| DeepSeek V3 | ~88% |
| Llama 4 Maverick | ~88% |
| GPT-4 (2023) | ~86% |
| 人类专家 | ~88% |

## 变体

### MMLU-Pro
- **创建者**: TIGER Lab (Berkeley)
- **特点**: 10 选项而非 4 选项，题目更难
- **题目数**: ~12,000
- **链接**: https://huggingface.co/datasets/TIGER-Lab/MMLU-Pro

### MMLU-Redux
- **创建者**: Edinburgh University
- **特点**: 修正了原始 MMLU 中的错误标注
- **题目数**: ~3,000（子集）
- **链接**: https://huggingface.co/datasets/edinburgh-dawg/mmlu-redux

### MMMLU (Multilingual MMLU)
- **创建者**: OpenAI
- **特点**: 覆盖 14 种语言
- **链接**: https://huggingface.co/datasets/openai/MMMLU

### C-Eval
- **创建者**: 上海交通大学
- **特点**: 中文版 MMLU，52 个学科
- **链接**: https://huggingface.co/datasets/ceval/ceval-exam

## 局限性

1. **饱和问题**: 2026年top模型已达94%+，区分度下降
2. **数据污染**: 题目可能出现在训练数据中
3. **仅评估选择题**: 不反映开放式问答能力
4. **英语中心**: 原始版本仅英语（MMMLU部分解决了此问题）
5. **深度不足**: 四选一无法评估深层推理

## 在各公司技术报告中的使用

- **OpenAI**: GPT-4, GPT-4o, o1, o3, GPT-5 系列均报告 MMLU 分数
- **Anthropic**: Claude 3, 3.5, 4 系列均使用
- **Google**: Gemini 1.0/1.5/2.0/3.0 系列均使用
- **Meta**: Llama 1/2/3/4 系列均使用
- **Mistral**: Mistral 7B/8x7B/Large 系列均使用
- **DeepSeek**: V2/V3/R1 系列均使用