---
id: RAG_HybridSearch2024
type: evidence
title: "Blended RAG: Improving RAG Accuracy with Semantic Search and Hybrid Query-Based Retrievers"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [RAG, hybrid-search, BM25, dense-retrieval]
source_type: paper
evidence_level: E3
---

# Blended RAG: Improving RAG Accuracy with Semantic Search and Hybrid Query-Based Retrievers

## Citation

**標題**: Blended RAG: Improving RAG Accuracy with Semantic Search and Hybrid Query-Based Retrievers
**arXiv**: [2404.07220](https://arxiv.org/abs/2404.07220)
**時間**: April 2024

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **三種搜尋策略**：研究探索三種不同搜尋策略：關鍵字相似度搜尋、dense vector 搜尋、sparse encoder 語義搜尋。

2. **混合查詢整合**：將這三種策略整合形成混合查詢（hybrid queries）。

3. **三種索引評測**：系統評測三種主要索引：BM25（關鍵字）、KNN（向量）、ELSER（sparse encoder 語義搜尋）。

4. **IBM 研究結論**：三向檢索（BM25 + dense + sparse）是 RAG 的最佳選項。

5. **Blended RAG 效能**：使用全文、dense vector 和 sparse vector 搜尋的 Blended RAG 優於純 vector 和雙向混合搜尋。

6. **Reranker 加成**：進一步加入 ColBERT 作為 reranker 可獲得更顯著改進。

### [I] 可推論的主張

1. 單一檢索策略通常不是最佳選擇。
2. Hybrid search 應成為 RAG 的標準配置。

---

## Where to Use

- [[RAG_企業知識問答_Playbook]] - Playbook（架構設計）
- [[VectorRetrieval_向量檢索與向量庫]] - 工具卡
