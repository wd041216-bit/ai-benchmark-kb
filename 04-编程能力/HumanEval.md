# HumanEval — 人类级代码生成评测

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | HumanEval: Hand-Written Code Evaluation |
| 创建者 | OpenAI (Chen et al.) |
| 发布年份 | 2021 |
| 题目数量 | 164 |
| 题型 | 函数级代码生成 |
| 数据集链接 | https://huggingface.co/datasets/openai/openai_humaneval |
| 论文链接 | https://arxiv.org/abs/2107.03374 |
| GitHub | https://github.com/openai/human-eval |
| 状态 | ⚠️ 已饱和（top 模型 > 95%） |

## 评测维度

每道题包含：
1. **函数签名**: Python 函数声明
2. **文档字符串**: 详细的功能描述和示例
3. **测试用例**: 用于验证正确性的单元测试

模型需要根据签名和文档字符串生成完整的函数实现。

## 题目示例

### 简单题
```python
from typing import List

def has_close_elements(numbers: List[float], threshold: float) -> bool:
    """Check if in given list of numbers, are any two numbers closer to each other than
    given threshold.
    >>> has_close_elements([1.0, 2.0, 3.0], 0.5)
    False
    >>> has_close_elements([1.0, 2.8, 3.0, 4.0, 5.0, 2.0], 0.3)
    True
    """
```

### 中等题
```python
def truncate_number(number: float) -> float:
    """Given a positive floating point number, it can be decomposed into
    an integer part and a decimal part. Return the decimal part.
    >>> truncate_number(3.5)
    0.5
    """
```

### 复杂题
```python
from typing import List

def string_xor(a: str, b: str) -> str:
    """Input are two strings a and b consisting only of 1s and 0s.
    Perform binary XOR on these inputs and return result also as a string.
    >>> string_xor('010', '110')
    '100'
    """
```

## 评分方式

- **主要指标**: Pass@k
  - Pass@1: 一次生成通过的概率
  - Pass@10: 10次生成中至少通过一次的概率
  - Pass@100: 100次生成中至少通过一次的概率
- **评分方法**: 在独立 Python 环境中运行测试用例
- **最常用指标**: Pass@1

## 各模型表现（2026年4月）

| 模型 | Pass@1 |
|------|--------|
| Claude Opus 4.6 | ~96% |
| GPT-5 | ~95% |
| Gemini 3 Pro | ~94% |
| DeepSeek V3 | ~89% |
| GPT-4 (2023) | ~67% |
| Codex (2021) | ~29% |

## 变体

### HumanEval+
- 扩展测试用例数量（平均 10x 测试）
- 更严格的验证，防止模型通过简单实现"碰运气"
- **链接**: https://github.com/evalplus/evalplus

### MBPP (Most Basic Python Problems)
- 1,000 道基础 Python 编程题
- Google Research 创建
- 题目比 HumanEval 更简单
- **数据集**: https://huggingface.co/datasets/google-research-datasets/mbpp

### LiveCodeBench
- 实时从编程竞赛平台抓取新题
- 防止训练数据污染
- **数据集**: https://huggingface.co/datasets/LiveCodeBench

### BigCodeBench
- 大规模代码生成 benchmark
- 1,140+ 道真实场景编程题
- 覆盖更多 Python 库和 API

## 局限性

1. **已饱和**: 2026年顶级模型已达 95%+
2. **仅 Python**: 不覆盖其他编程语言
3. **函数级**: 不测试项目级代码能力
4. **简单任务**: 大部分题目是简单函数
5. **数据污染**: 题目可能出现在训练集中

## 推荐替代

| 替代 | 优势 | 链接 |
|------|------|------|
| SWE-bench | 真实 Issue 修复 | swebench.com |
| LiveCodeBench | 防污染，持续更新 | livecodebench.org |
| SWE-bench Live | 多语言，持续更新 | swe-bench-live.github.io |
| BigCodeBench | 更大规模，更多 API | bigcode-bench.github.io |