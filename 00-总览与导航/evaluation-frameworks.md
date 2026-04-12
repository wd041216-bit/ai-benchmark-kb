# 评测框架与工具

## 主流评测框架

### 1. EleutherAI lm-evaluation-harness

- **仓库**: https://github.com/EleutherAI/lm-evaluation-harness
- **地位**: 业界标准的开源 LLM 评测框架
- **支持 Benchmark**: 60+（MMLU, HellaSwag, GSM8K, ARC, BBH, TruthfulQA 等）
- **特点**: 统一评测协议，支持 few-shot/zero-shot，社区驱动
- **使用方式**:
```bash
pip install lm-eval
lm_eval --model hf --model_args pretrained=meta-llama/Llama-3-8B --tasks mmlu,hellaswag,gsm8k
```

### 2. HELM (Holistic Evaluation of Language Models)

- **网站**: https://crfm.stanford.edu/helm/
- **机构**: Stanford CRFM
- **特点**: 全面覆盖，包含场景、适配器、指标三层评估
- **覆盖维度**: 准确性、校准性、鲁棒性、公平性、偏见、毒性、效率

### 3. DeepEval

- **网站**: https://deepeval.com
- **特点**: 集成 Benchmark 评测与自定义指标
- **支持**: MMLU, GSM8K, HumanEval, TruthfulQA, HellaSwag, BBH
- **代码示例**:
```python
from deepeval.benchmarks import MMLU, GSM8K
benchmark = MMLU(tasks=[...], n_shots=3)
benchmark.evaluate(model=my_model)
```

### 4. rLLM

- **网站**: https://docs.rllm-project.com
- **特点**: 50+ benchmark 数据集，自动拉取与评测
- **覆盖**: 数学、代码、多选、问答、长上下文、多模态

### 5. Scale AI Leaderboards

- **网站**: https://scale.com/leaderboard
- **特点**: 提供私有评测集，防止数据污染
- **主要基准**: HLE, Chatbot Arena

### 6. Chatbot Arena (LMSYS)

- **网站**: https://chat.lmsys.org
- **特点**: 基于 Elo 评分的人类偏好评测
- **覆盖**: 文本、代码、视觉、长上下文
- **评分**: 基于 500万+ 真实用户对比

## 评测工具对比

| 框架 | 开源 | Benchmark 数 | 易用性 | 防污染 | 社区活跃度 |
|------|------|-------------|--------|--------|-----------|
| lm-eval-harness | ✅ | 60+ | 高 | ❌ | ⭐⭐⭐⭐⭐ |
| HELM | ✅ | 40+ | 中 | ❌ | ⭐⭐⭐⭐ |
| DeepEval | ✅ | 10+ | 高 | ❌ | ⭐⭐⭐⭐ |
| rLLM | ✅ | 50+ | 中 | ❌ | ⭐⭐⭐ |
| Scale AI | ❌ | 少量 | 高 | ✅ | ⭐⭐⭐⭐ |
| Chatbot Arena | 半开 | N/A | 高 | ✅ | ⭐⭐⭐⭐⭐ |

## 关键评测指标

| 指标 | 说明 | 适用场景 |
|------|------|---------|
| Accuracy | 准确率，最基本指标 | 多选题、事实性问答 |
| Pass@k | k 次采样中至少通过一次的比例 | 代码生成（HumanEval） |
| Exact Match | 完全匹配率 | 数学题（GSM8K, MATH） |
| F1 Score | 精确率与召回率的调和平均 | 问答、信息抽取 |
| Elo Rating | 基于对比的动态评分 | Chatbot Arena |
| BLEU/ROUGE | 生成文本与参考的重叠度 | 翻译、摘要 |
| Brier Score | 校准误差 | 模型置信度评估 |