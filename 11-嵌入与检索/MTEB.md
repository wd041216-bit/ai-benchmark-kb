# MTEB — 大规模文本嵌入评测

## 基本信息

| 属性 | 值 |
|------|-----|
| 全称 | Massive Text Embedding Benchmark |
| 创建者 | Hugging Face & Cohere |
| 发布年份 | 2023 |
| 任务数量 | 56 个数据集, 覆盖 8 个任务类型 |
| 数据集链接 | https://huggingface.co/spaces/mteb/leaderboard |
| 论文链接 | https://arxiv.org/abs/2210.07316 |
| GitHub | https://github.com/embeddings-benchmark/mteb |

## 评测维度

| 任务类型 | 数据集数 | 说明 |
|---------|--------|------|
| 分类 | 12 | 文本分类嵌入质量 |
| 聚类 | 11 | 文本聚类嵌入质量 |
| 成对分类 | 3 | 语义相似度 |
| 重排序 | 3 | 搜索重排序 |
| 检索 | 15 | 信息检索 |
| 语义文本相似度 | 3 | STS 评估 |
| 摘要 | 2 | 摘要质量 |
| Bitext Mining | 5 | 跨语言检索 |

## 评测指标

- **分类**: Accuracy, F1
- **检索**: NDCG@10
- **聚类**: V-measure
- **STS**: Spearman correlation
- **综合排名**: 多指标加权平均

## 关联 Benchmark

### BEIR
- **全称**: Benchmark for Information Retrieval
- **创建者**: University of Cambridge
- **特点**: 9 个检索任务，覆盖多种领域
- **链接**: https://github.com/beir-cellar/beir

### LongEval
- 评估长文档检索能力
- 测试不同文档长度下的检索性能