---
id: RAG_ChunkSize2025
type: evidence
title: "Rethinking Chunk Size for Long-Document Retrieval: A Multi-Dataset Analysis"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [RAG, chunking, retrieval, optimization]
source_type: paper
evidence_level: E3
---

# Rethinking Chunk Size for Long-Document Retrieval: A Multi-Dataset Analysis

## Citation

**標題**: Rethinking Chunk Size For Long-Document Retrieval: A Multi-Dataset Analysis
**arXiv**: [2505.21700](https://arxiv.org/abs/2505.21700)
**時間**: May 2025

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **小 chunk 適用場景**：較小的 chunk（64-128 tokens）對於需要簡潔、事實性答案的資料集最佳。

2. **大 chunk 適用場景**：較大的 chunk（512-1024 tokens）在需要更廣泛上下文理解的資料集上改善檢索效果。

3. **模型敏感性差異**：不同 embedding 模型展現不同的 chunking 敏感性：
   - Stella 模型：較大 chunk 有利於長距離檢索
   - Snowflake 模型：較小 chunk 有利於細粒度、實體匹配

### [I] 可推論的主張

1. Chunk size 應根據任務類型和資料特性調整。
2. 沒有「萬能」的 chunk size。

---

## Key Data

| 查詢類型 | 建議 chunk size |
|----------|----------------|
| Factoid 查詢 | 256-512 tokens |
| 分析型查詢 | 1024+ tokens |
| 實體匹配 | 64-128 tokens |

---

## Where to Use

- [[RAG_企業知識問答_Playbook]] - Playbook（參數調優）
- [[RAG問答_RAG-QA]] - 能力卡
