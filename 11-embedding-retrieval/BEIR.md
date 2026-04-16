# BEIR — Zero-Shot Information Retrieval Benchmark

## Basic Information

| Attribute | Value |
|-----------|-------|
| Full Name | Benchmark for Information Retrieval (BEIR) |
| Creators | University of Cambridge (Thakur, Reimers, Rücklé, Srivastava, Gurevych) |
| Year Published | 2021 |
| Number of Datasets | 18 datasets, covering 9 retrieval tasks |
| Task Type | Zero-shot information retrieval (Query → relevant document ranking) |
| Dataset Link | https://huggingface.co/datasets/BeIR |
| Paper Link | https://arxiv.org/abs/2104.08663 |
| GitHub | https://github.com/beir-cellar/beir |
| Status | ✅ Widely used; retrieval subset incorporated into MTEB |

## Overview

BEIR is the first heterogeneous benchmark that systematically evaluates the zero-shot generalization ability of retrieval models. Its core design philosophy is: can retrieval models trained on large-scale supervised data like MSMARCO maintain good performance on unseen domains and task types? BEIR covers a wide range of scenarios from biomedicine to finance, from fact-checking to argument retrieval, imposing strict requirements on models' cross-domain generalization capabilities.

## Dataset Composition

### 9 Task Types and 18 Datasets

| Task Type | Dataset | Number of Queries | Corpus Size | Avg. Relevant Docs/Query |
|-----------|---------|-------------------|-------------|--------------------------|
| Question Answering | NQ | 3,452 | 2.68M | 1.2 |
| Question Answering | HotpotQA | 7,405 | 5.23M | 2.0 |
| Question Answering | FiQA-2018 | 648 | 57K | 2.6 |
| Fact Verification | FEVER | 6,666 | 5.42M | 1.2 |
| Fact Verification | Climate-FEVER | 1,535 | 5.42M | 3.0 |
| Fact Verification | SciFact | 300 | 5K | 1.1 |
| Argument Retrieval | ArguAna | 1,406 | 8.67K | 1.0 |
| Argument Retrieval | Touche-2020 | 49 | 382K | 19.0 |
| Duplicate Question Retrieval | Quora | 10,000 | 523K | 1.6 |
| Duplicate Question Retrieval | CQADupstack | 13,145 | 457K | 1.4 |
| Entity Retrieval | DBPedia-Entity | 400 | 4.63M | 38.2 |
| Citation Prediction | SCIDOCS | 1,000 | 25K | 4.9 |
| Tweet Retrieval | Signal-1M(RT) | 97 | 2.86M | 19.6 |
| News Retrieval | TREC-NEWS | 57 | 595K | 19.6 |
| News Retrieval | Robust04 | 249 | 528K | 69.9 |
| Biomedical Retrieval | TREC-COVID | 50 | 171K | 493.5 |
| Biomedical Retrieval | NFCorpus | 323 | 3.6K | 38.2 |
| Biomedical Retrieval | BioASQ | 500 | 14.91M | 4.7 |

> Note: MSMARCO is provided as a training dataset and is not used as an evaluation task. BioASQ, Signal-1M, TREC-NEWS, and Robust04 require additional data access agreements.

## Evaluation Method

- **Primary Metric**: NDCG@10 (Normalized Discounted Cumulative Gain)
- **Auxiliary Metrics**: Recall@k, MAP, Precision@k
- **Evaluation Mode**: Zero-shot; models must not be fine-tuned on any evaluation dataset
- **Evaluation Process**: Given a query, the model ranks documents in the corpus; ranking quality is evaluated by NDCG@10
- **Baseline**: BM25 (Anserini) as the lexical retrieval baseline; most neural retrieval models need to surpass this baseline to have practical value

## Model Performance (April 2026)

### BEIR Zero-Shot Average NDCG@10

| Model | Average NDCG@10 | Type | Parameters |
|-------|----------------|------|------------|
| Gemini Embedding 2 | ~67.7 | Dense (multimodal) | — |
| Voyage 4 Large | ~66.0 | Dense (MoE) | — |
| NV-Embed-v2 | ~62.7 | Dense | 7.84B |
| Qwen3-Embedding-8B | ~62.0 | Dense | 8B |
| Cohere Embed v4 | ~61.0 | Dense | — |
| OpenAI text-embedding-3-large | ~59.0 | Dense | — |
| BGE-M3 | ~58.0 | Dense+Sparse | 568M |
| ColBERT-v2 | ~55.0 | Late Interaction | 110M |
| BM25 (baseline) | ~42.0 | Sparse (lexical) | — |

> Note: The above scores are approximate values, estimated from a combination of the MTEB retrieval leaderboard and BEIR-related evaluation reports. Dense retrieval models lead BM25 by approximately 15-25%; hybrid retrieval (BM25 + Dense) can still provide an additional 2-5% improvement.

### Domain Generalization Gap

| Domain | General-Purpose Model | Domain Fine-Tuned Model | Improvement |
|--------|----------------------|------------------------|-------------|
| Medical | ~48% | ~62% | +29% |
| Code | ~44% | ~59% | +34% |
| Legal | ~46% | ~57% | +24% |

## Example Tasks

### TREC-COVID (Biomedical Retrieval)
```
Query: "what is the origin of COVID-19"
Corpus: 171,332 CORD-19 scientific papers
Task: Retrieve scientific literature related to the origin of COVID-19
Relevance: 3-level annotation (fully relevant, partially relevant, not relevant)
```

### FiQA-2018 (Financial QA Retrieval)
```
Query: "What is the PEG ratio? How is the PEG ratio calculated?"
Corpus: 57,638 StackExchange financial Q&A posts
Task: Retrieve relevant posts that answer the financial question
```

### ArguAna (Argument Retrieval)
```
Query: "Gun control laws should be stricter to reduce violence"
Corpus: 8,674 argument texts
Task: Retrieve arguments opposing the given argument (counter-retrieval)
```

## Variants and Related Benchmarks

### MTEB (Massive Text Embedding Benchmark)
- BEIR's retrieval subset has been incorporated into the MTEB evaluation framework
- MTEB expands evaluation dimensions, covering 8 task types including classification, clustering, and STS
- See [MTEB.md](./MTEB.md)

### BRIGHT (2025)
- Reasoning-intensive retrieval evaluation, published at ICLR 2025
- Top MTEB models achieve only ~18.3 on BRIGHT
- Exposes the shortcomings of current embedding models in complex reasoning scenarios

### COIR (2025)
- Code information retrieval benchmark, published at ACL 2025
- 10 datasets covering 8 code-related retrieval tasks

### MMTEB (2025)
- Multilingual extension of MTEB
- Covers 250+ languages, with evaluation tasks in 112+ languages

## Limitations and Controversies

1. **Annotation Bias**: Datasets like TREC-COVID have annotation selection bias; many unlabeled documents exist in the top-10 results of dense retrieval models, unfairly depressing NDCG scores
2. **Strong BM25 Baseline**: In some domains (e.g., biomedicine), BM25 remains a hard-to-beat strong baseline, and many dense retrieval models lack generalization capability
3. **Domain Imbalance**: Datasets are skewed toward English and technology domains, lacking coverage of professional fields like law and creative writing
4. **Training Data Contamination**: Some top models may have been trained on BEIR-related data, undermining the fairness of zero-shot evaluation
5. **Metric Limitations**: NDCG@10 focuses on the top 10 ranked results and may overlook long-tail retrieval quality
6. **Overlap with MTEB**: BEIR's retrieval datasets have been incorporated into MTEB, and standalone usage frequency is declining

## Data Sources / References

- Thakur et al., "BEIR: A Heterogeneous Benchmark for Zero-shot Evaluation of Information Retrieval Models", NeurIPS 2021 [[Paper]](https://arxiv.org/abs/2104.08663)
- BEIR GitHub repository: https://github.com/beir-cellar/beir
- BEIR dataset: https://huggingface.co/datasets/BeIR
- BEIR leaderboard and scores: https://docs.google.com/spreadsheets/d/1_ZyYkPJ_K0st9FJBrjbZqX14nmCCPVlE_y3a_y5KkYI/
- MTEB leaderboard: https://huggingface.co/spaces/mteb/leaderboard