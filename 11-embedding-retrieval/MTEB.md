# MTEB — Massive Text Embedding Benchmark

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | Massive Text Embedding Benchmark |
| Creators | Hugging Face & Cohere (Muennighoff et al.) |
| Year Published | 2022 (v1), 2025 (v2 refactor) |
| Number of Tasks | 56 datasets, covering 8 task types (v1); v2 expanded further |
| Dataset Link | https://huggingface.co/spaces/mteb/leaderboard |
| Paper Link | https://arxiv.org/abs/2210.07316 |
| GitHub | https://github.com/embeddings-benchmark/mteb |
| Status | ✅ Actively maintained, de facto standard for embedding model evaluation |

## Overview

MTEB is currently the most widely used evaluation benchmark for text embedding models, designed to provide a comprehensive and heterogeneous evaluation framework for embedding models. Unlike traditional single-task evaluation (e.g., only STS or retrieval), MTEB covers 8 task types including classification, clustering, retrieval, and reranking, revealing models' true capabilities across different dimensions of semantic understanding. Since its release in 2022, MTEB has become the de facto standard leaderboard for embedding models, with major models using MTEB average scores as their core metric.

## Dataset Composition

### 8 Task Types

| Task Type | Number of Datasets | Description | Primary Metric |
|-----------|-------------------|-------------|----------------|
| Classification | 12 | Text classification embedding quality | Accuracy, F1 |
| Clustering | 11 | Text clustering embedding quality | V-measure |
| Pair Classification | 3 | Sentence pair relation classification | Average Precision |
| Reranking | 3 | Search result reranking | MAP |
| Retrieval | 15 | Information retrieval | NDCG@10 |
| Semantic Textual Similarity (STS) | 6 | Semantic equivalence | Spearman ρ |
| Summarization | 2 | Summary quality evaluation | Spearman ρ |
| Bitext Mining | 5 | Cross-lingual sentence pair matching | F1 |

### Task Examples

**Classification**: Train a kNN or logistic regression classifier using embeddings
```
Input: "Why was I charged twice?"
Label: card_payment_wrong_exchange_rate
Evaluation: Accuracy on the Banking77 77-class fine-grained intent classification dataset
```

**Retrieval**: Retrieve relevant documents from a corpus given a query
```
Query: "What is the capital of France?"
Corpus: Hundreds of thousands of documents
Evaluation: Ranking quality by NDCG@10
Covers: MSMARCO, NQ, HotpotQA, FiQA, TREC-COVID, etc.
```

**Clustering**: Group semantically similar texts together
```
Input: ["quantum computing advances", "new qubit architecture", "stock market rally", "GDP growth forecast"]
Labels: {Science: [0,1], Finance: [2,3]}
Evaluation: V-measure of clustering results against ground truth labels
Covers: ArXiv, BioRxiv, MedRxiv, Reddit, StackExchange, etc.
```

**STS**: Predict semantic similarity of sentence pairs
```
Sentence A: "A plane is taking off."
Sentence B: "An air plane is taking off."
Human rating: 5.0 (fully equivalent)
Evaluation: Spearman correlation between model cosine similarity and human ratings
```

**Bitext Mining**: Cross-lingual translation pair matching
```
English: "The cat sat on the mat."
German: "Die Katze saß auf der Matte."
Evaluation: F1 of cross-lingual nearest neighbor matching
```

## Evaluation Method

- **Evaluation Framework**: Unified execution of all tasks via the `mteb` Python library
- **Overall Ranking**: Multi-task weighted average score, using Borda Count ranking method
- **Evaluation Process**: Evaluate each dataset separately, then average by task type, and finally compute the weighted average across all task types
- **Zero-Shot Principle**: Evaluation data must not appear in the model's training set; the leaderboard annotates model training data transparency
- **v2 Improvements**: Refactored to modular architecture in 2025, adding CrossEncoder support, SearchProtocol interface, and ResultCache mechanism

```python
import mteb

# Run MTEB evaluation
tasks = mteb.get_tasks(task_types=["Classification", "Retrieval", "STS"])
evaluation = mteb.MTEB(tasks=tasks)
evaluation.run("BAAI/bge-m3", output_folder="results")
```

## Model Performance (April 2026)

### MTEB English Average Score (All Task Types)

| Model | MTEB Average | Retrieval | Classification | Clustering | STS | Parameters | Open Source |
|-------|-------------|-----------|----------------|------------|-----|------------|------------|
| Gemini Embedding 2 | ~72.5 | ~67.7 | ~88.0 | ~57.0 | ~87.0 | — | No |
| KaLM-Gemma3-12B | 72.32 | — | — | — | — | 12B | Yes |
| NV-Embed-v2 | ~72.3 | ~62.7 | ~87.5 | ~57.0 | ~85.5 | 7.84B | Yes |
| GTE-Qwen2-7B | ~71.3 | ~61.5 | ~87.0 | ~56.5 | ~85.0 | 7B | Yes |
| Voyage-3-large | ~67.2 | ~58.2 | ~86.1 | ~54.3 | ~84.5 | — | No |
| E5-mistral-7b | ~65.9 | ~56.3 | ~85.0 | ~53.5 | ~83.0 | 7B | Yes |
| Cohere embed v4 | ~65.2 | ~56.8 | ~87.3 | ~55.1 | ~85.2 | — | No |
| OpenAI text-embedding-3-large | ~62.0 | ~55.4 | ~85.9 | ~52.1 | ~82.7 | — | No |
| BGE-M3 | ~63.0 | ~55.3 | ~85.7 | ~53.8 | ~83.9 | 568M | Yes |
| all-MiniLM-L6-v2 | ~56.0 | ~42.0 | ~78.0 | ~42.0 | ~78.0 | 22M | Yes |

> Note: The above scores are approximate values (marked with ~), estimated from a combination of the MTEB leaderboard and various model technical reports. The leaderboard is updated frequently; please refer to real-time data at https://huggingface.co/spaces/mteb/leaderboard. Large-parameter models (7B+) significantly lead in English evaluation, but their inference cost also increases proportionally.

### MTEB Retrieval Subset (NDCG@10)

| Model | Retrieval NDCG@10 |
|-------|--------------------|
| Gemini Embedding 2 | ~67.7 |
| Voyage 4 Large | ~66.0 |
| NV-Embed-v2 | ~62.7 |
| Cohere embed v4 | ~56.8 |
| BGE-M3 | ~55.3 |
| BM25 (baseline) | ~42.0 |

## Variants and Related Benchmarks

### MTEB-Multilingual (MMTEB)
- **Full Name**: Massive Multilingual Text Embedding Benchmark
- **Paper**: Enevoldsen et al., 2025 (arXiv:2502.13595)
- **Coverage**: 250+ languages, with complete evaluation tasks in 112+ languages
- **Features**: Extends MTEB's language coverage, incorporating cross-lingual retrieval and multilingual classification tasks
- **Link**: https://huggingface.co/collections/mteb/mmteb
- **Note**: BGE-M3 and Cohere embed v4 perform notably well in multilingual evaluation, benefiting from multilingual training data

### MTEB v2 (2025 Refactor)
- **Improvements**: Modular architecture, supporting multimodal evaluation (MIEB), CrossEncoder, and SearchProtocol
- **Data Format**: Unified to Parquet format, removing `trust_remote_code` dependency
- **Version Management**: Strict semantic versioning, avoiding the breaking change issues of the v1 era
- **Evaluation Simplification**: `mteb.evaluate()` replaces the old `mteb.MTEB.run()` interface

### MIEB (Massive Image Embedding Benchmark)
- **Full Name**: Massive Image Embedding Benchmark
- **Paper**: Xiao et al., 2025 (arXiv:2504.10471)
- **Coverage**: Image/multimodal embedding evaluation
- **Relationship to MTEB**: MTEB v2 natively supports multimodal input via `EncoderProtocol`

### BEIR
- **Full Name**: Benchmark for Information Retrieval
- **Creators**: University of Cambridge (Thakur et al.)
- **Features**: 9 retrieval tasks covering multiple domains, zero-shot evaluation
- **Relationship to MTEB**: BEIR's retrieval datasets have been incorporated into MTEB as the retrieval subset
- **See**: [BEIR.md](./BEIR.md)

### LongEval
- Evaluates long document retrieval capability
- Tests retrieval performance degradation at different document lengths

## Limitations and Controversies

1. **Training Data Contamination**: Some top models on the leaderboard have been trained on BEIR/MTEB-related data, raising questions about the fairness of zero-shot evaluation; MTEB v2 has introduced training data transparency annotations to mitigate this issue
2. **Model Size Bias**: Large-parameter models (7B+) occupy the top of the leaderboard, but their inference cost is high; the practical utility of small models (e.g., all-MiniLM-L6-v2) in resource-constrained scenarios is not fully reflected
3. **Uneven Domain Coverage**: The original MTEB(eng, v1) is skewed toward news, web pages, and encyclopedia-style content, with insufficient coverage in law, finance, creative writing, and other domains
4. **Skewed Language Distribution**: MMTEB has 290 English tasks, while many low-resource languages have fewer than 10 tasks
5. **Aggregation Method Controversy**: The methodological soundness of averaging scores across heterogeneous task types (e.g., clustering V-measure and retrieval NDCG@10) is questionable; Borda Count ranking is sensitive to the model set
6. **Bias Not Evaluated**: The framework does not assess social bias (gender, race, etc.) in text embedding models; Rakivnenko et al. (2024) have pointed out this issue
7. **Reproducibility Challenges**: Different models use different prefixes (e.g., E5's "query:" / "passage:"), normalization methods, etc., making fair comparison difficult; self-reported scores have sometimes been irreproducible
8. **Evaluation Cost**: Running the full MTEB(eng, v2) on a 7B model requires approximately 3 hours (H100 GPU), creating a resource barrier for the research community

## Data Sources / References

- Muennighoff et al., "MTEB: Massive Text Embedding Benchmark", 2022 [[Paper]](https://arxiv.org/abs/2210.07316)
- Enevoldsen et al., "MMTEB: Massive Multilingual Text Embedding Benchmark", ICLR 2025 [[Paper]](https://arxiv.org/abs/2502.13595)
- Chung et al., "Maintaining MTEB: Towards Long Term Usability and Reproducibility of Embedding Benchmarks", 2025 [[Paper]](https://arxiv.org/abs/2506.21182)
- MTEB Leaderboard: https://huggingface.co/spaces/mteb/leaderboard
- MTEB GitHub repository: https://github.com/embeddings-benchmark/mteb
- MTEB official website: https://mteb.info/