# SWE-bench — Software Engineering Benchmark

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | SWE-bench: Can Language Models Resolve Real-World GitHub Issues? |
| 创建者 | Princeton NLP (Jimenez et al.) |
| 发布年份 | 2023 |
| 题目数量 | 2,294 (Full), 500 (Verified) |
| 题型 | 真实 GitHub Issue → 生成修复补丁 |
| 数据集链接 | https://www.swebench.com |
| 论文链接 | https://arxiv.org/abs/2310.06770 |
| GitHub | https://github.com/princeton-nlp/SWE-bench |
| 状态 | ✅ 仍有区分度（top 模型 < 80%） |

## 评测维度

SWE-bench 是评估 AI 代码能力最接近真实软件工程的 benchmark：

1. **Issue 理解**: 理解真实 Bug 报告
2. **代码导航**: 在大型仓库中定位问题
3. **代码编辑**: 生成正确的修复补丁
4. **测试通过**: 补丁必须通过相关测试用例

## 工作流程

```
输入: GitHub Issue 描述 + 完整代码仓库
↓
AI 系统: 分析 Issue, 定位代码, 生成补丁
↓
输出: git diff 格式的补丁
↓
评估: 在 Docker 中应用补丁并运行测试
↓
结果: Pass / Fail
```

## 题目示例

### Issue 描述
```
Title: DataFrame.groupby() produces incorrect results with nullable int dtype

When using groupby on a DataFrame with nullable integer dtype (Int64),
the sum aggregation produces incorrect results. The values are off by
a factor related to the number of groups.

Expected behavior:
>>> df.groupby('key')['value'].sum()
key
A    10
B    20
Name: value, dtype: Int64

Actual behavior:
>>> df.groupby('key')['value'].sum()
key
A    30
B    60
Name: value, dtype: Int64

Version: pandas 2.0.3
```

### 正确补丁
```diff
--- a/pandas/core/groupby/groupby.py
+++ b/pandas/core/groupby/groupby.py
@@ -1234,7 +1234,7 @@
- result = self._aggregate_named()
+ result = self._aggregate_named().astype(self.obj.dtype)
```

## 数据集变体

### SWE-bench Full (2,294 题)
- 完整数据集
- 覆盖 12 个 Python 仓库
- 问题：许多题目含糊或无法解决

### SWE-bench Verified (500 题)
- OpenAI 与 Princeton 合作筛选
- 每道题经人类工程师验证可解决
- **最广泛使用的子集**
- **数据集**: https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified

### SWE-bench Lite (300 题)
- 较轻量的子集
- 适合快速评测

### SWE-bench Pro
- 更难的子集，包含更复杂的任务
- 2026年新标准

### SWE-bench Live (1,319+ 题, 持续更新)
- Microsoft 创建的持续更新版本
- 每月新增约 50 道题
- 来自 93+ 个仓库（远超原始 12 个）
- 防止训练数据污染
- **数据集**: https://huggingface.co/datasets/SWE-bench-Live

### SWE-bench Multilingual
- 支持 C/C++, C#, TypeScript/JavaScript, Go, Rust, Java
- 评估多语言 Issue 修复能力

## 各模型表现（2026年4月）

### SWE-bench Verified

| 模型 | 分辨率 |
|------|--------|
| Claude Mythos Preview | 93.9% |
| GPT-5.4 | 79.2% |
| Claude Opus 4.6 | 79.2% |
| Gemini 3 Flash | 76.2% |
| DeepSeek V3.2 | ~60% |
| Llama 4 Maverick | ~40% |

### SWE-bench Pro

| 模型 | 分辨率 |
|------|--------|
| Claude Mythos Preview | 77.8% |
| GPT-5.3 Codex | 77.3% |
| Claude Opus 4.6 | ~70% |
| Gemini 3.1 Pro | ~65% |

### SWE-bench Live (Lite)

| 模型 | 分辨率 |
|------|--------|
| OpenHands + Qwen3-Coder | 24.67% |
| SWE-Agent + GPT-5 | ~19% |
| OpenHands + Claude 4.5 | ~18% |

## 为何 SWE-bench 是最重要的代码 Benchmark

1. **真实性**: 基于 12+ 个真实开源仓库的 GitHub Issue
2. **端到端评估**: 从 Issue 理解到补丁生成的全流程
3. **自动评分**: Docker 环境中运行测试
4. **不可作弊**: 无法通过简单模式匹配解决
5. **仍有空间**: 顶级模型在 Verified 子集上约 80%

## 局限性

1. **仅 Python**: 原始版本仅覆盖 Python 仓库
2. **仓库局限**: 12 个仓库的覆盖面有限
3. **评分偏差**: 不同 agent 框架得分差异大
4. **更新滞后**: 原始数据集已不再更新
5. **计算成本高**: 需要完整 Docker 环境运行评测