# C-Eval — 中文综合评测

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | C-Eval: A Multi-Level Multi-Discipline Chinese Evaluation |
| 创建者 | 上海交通大学等 |
| 发布年份 | 2023 |
| 题目数量 | 13,948（52个学科） |
| 题型 | 四选一多项选择题 |
| 数据集链接 | https://huggingface.co/datasets/ceval/ceval-exam |
| 论文链接 | https://arxiv.org/abs/2305.08322 |
| GitHub | https://github.com/SJTU-LIT/C-Eval |
| 状态 | 中文模型评测标准 |

## 评测维度

覆盖 52 个中文大学学科，分为四个难度级别：

1. **初中**: 基础学科
2. **高中**: 进阶学科
3. **大学**: 专业学科
4. **研究生**: 高级学科

### 核心学科
- 数学、物理、化学、生物
- 计算机科学、电气工程
- 历史、政治、法律
- 经济、管理、会计
- 医学、心理学

## 与 MMLU 的关系

- C-Eval 是中文版 MMLU
- 覆盖类似的知识维度但全部使用中文
- 两者可以对比模型的中英文能力差异