# BIG-bench — Beyond the Imitation Game

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | Beyond the Imitation Game Benchmark |
| 创建者 | Google 及 400+ 社区贡献者 |
| 发布年份 | 2022 |
| 任务数量 | 204 个任务 |
| 题型 | 多种（多选、生成、评分等） |
| 数据集链接 | https://huggingface.co/datasets/bigbench |
| 论文链接 | https://arxiv.org/abs/2206.04615 |
| GitHub | https://github.com/google/BIG-bench |

## 评测维度

覆盖极其广泛的能力：

### 核心大类
1. **逻辑推理**: 逻辑谜题、演绎推理、归纳推理
2. **数学**: 算术、代数、数论
3. **语言理解**: 语法、语义、语用
4. **常识**: 物理常识、社会常识
5. **知识**: 科学、历史、文化
6. **创造力**: 生成、联想
7. **偏见与安全**: 社会偏见、伦理判断

### BIG-bench Hard (BBH)
- 从 204 个任务中精选 23 个最具挑战性的任务
- 这些任务是当时大模型表现低于人类平均水平的子集
- 已成为独立的标准 benchmark
- **数据集链接**: https://huggingface.co/datasets/lukaemon/bbh

## BBH 包含的 23 个困难任务

| 任务名 | 描述 |
|--------|------|
| boolean_expressions | 布尔表达式求值 |
| causal_judgement | 因果判断 |
| date_understanding | 日期理解 |
| disambiguation_qa | 消歧问答 |
| dyck_languages | Dyck 语言（括号匹配） |
| formal_fallacies | 形式谬误识别 |
| geometric_shapes | 几何形状推理 |
| hyperbaton | 词序判断 |
| logical_deduction | 逻辑演绎 |
| mathematical_induction | 数学归纳 |
| multistep_arithmetic | 多步算术 |
| navigate | 空间导航 |
| object_counting | 物体计数 |
| penguins_in_a_table | 表格推理 |
| reasoning_about_colored_objects | 颜色物体推理 |
| ruin_names | 名字识别 |
| salient_translation_error_detection | 翻译错误检测 |
| snarks | 讽刺识别 |
| sports_understanding | 体育理解 |
| temporal_sequences | 时间序列推理 |
| tracking_shuffled_objects | 追踪打乱物体 |
| word_sorting | 单词排序 |

## 题目示例

### 逻辑演绎
```
The following paragraphs each describe a set of three objects arranged in a fixed order. The statements are logically consistent within each paragraph.
On a shelf, there are three books: a white book, a green book, and a blue book. The white book is to the left of the green book. The blue book is the rightmost.
Options:
A) The white book is the leftmost
B) The green book is the leftmost
C) The blue book is the leftmost
Answer: A
```

### 因果判断
```
How would a typical person answer the following question about cause and effect?
A military coup overthrew the government. The country's GDP decreased.
Options:
A) The coup caused the GDP decrease
B) The GDP decrease caused the coup
C) Neither caused the other
Answer: A
```

## 评分方式

- 每个任务独立评分
- BBH 使用 3-shot prompting
- 主要指标：各任务准确率的平均值
- 对比基线：人类表现、随机基线

## 各模型表现

| 模型 | BBH 准确率 |
|------|-----------|
| GPT-4 | ~83% |
| Claude 3.5 Sonnet | ~80% |
| Gemini 1.5 Pro | ~75% |
| Llama 3 70B | ~70% |
| 随机基线 | ~25-50% |

## 局限性

1. 任务质量参差不齐（社区贡献）
2. 部分任务过于小众
3. BBH 子集已成为更流行的使用方式
4. 与 MMLU 有重叠

## 使用场景

- **Google**: Gemini 技术报告中广泛使用
- **Meta**: Llama 系列报告部分 BBH 分数
- **学术界**: 作为综合推理能力评估的重要参考