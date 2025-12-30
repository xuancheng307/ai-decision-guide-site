---
type: tool
title: "向量檢索與向量庫 (Vector Retrieval & Vector DB)"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
expiry_date: 2025-07-XX
expiry_policy: 6_months
tags: [vector-db, embedding, retrieval, RAG]
status: stable
---

# 向量檢索與向量庫 (Vector Retrieval & Vector DB)

> **一句話**：將文字轉換為向量，透過相似度搜尋找到語義相關的內容。

---

## 核心概念

| 組件 | 功能 | 常見選項 |
|------|------|---------|
| **Embedding Model** | 文字 → 向量 | OpenAI text-embedding-3, BGE, E5 |
| **Vector Database** | 儲存與檢索向量 | Pinecone, Milvus, Weaviate, Qdrant, Chroma |
| **Index Type** | 加速搜尋的資料結構 | HNSW, IVF, Flat |
| **Similarity Metric** | 相似度計算方式 | Cosine, Euclidean, Dot Product |

---

## 工具比較

### Embedding Models

| 模型 | 維度 | MTEB 排名 | 適用場景 | 來源 |
|------|------|-----------|---------|------|
| text-embedding-3-large | 3072 | Top 10 | 通用、高品質 | [^API_OpenAI_Embeddings] |
| text-embedding-3-small | 1536 | - | 成本敏感 | [^API_OpenAI_Embeddings] |
| BGE-large-en-v1.5 | 1024 | Top 5 | 開源首選 | [^EMBED_BGE2023] |
| E5-large-v2 | 1024 | Top 10 | 開源、多語言 | [^EMBED_E52023] |

### Vector Databases

| 資料庫 | 類型 | 特點 | 適用場景 |
|--------|------|------|---------|
| **Pinecone** | Managed | 低延遲、無運維 | 快速部署、團隊小 |
| **Milvus** | Open-source | 11 種索引、高 throughput | 大規模、需彈性 |
| **Weaviate** | Open-source | 原生 Hybrid Search | 需混合檢索 |
| **Qdrant** | Open-source | Rust 實作、高效能 | 效能優先 |
| **Chroma** | Open-source | 輕量、易上手 | PoC、快速驗證 |
| **pgvector** | Extension | 整合 PostgreSQL | 已有 PG 基礎設施 |

---

## 選型決策樹

```
需要向量檢索
├── 是否需要 Production 等級？
│   ├── 是 → 是否有運維能力？
│   │   ├── 是 → Milvus / Qdrant
│   │   └── 否 → Pinecone
│   └── 否（PoC/Pilot）→ Chroma / pgvector
└── 是否需要 Hybrid Search？
    ├── 是 → Weaviate
    └── 否 → 依上述選擇
```

---

## 關鍵參數

| 參數 | 說明 | 建議值 | 備註 |
|------|------|--------|------|
| `top_k` | 返回結果數 | 5-20 | 視下游 context window |
| `similarity_threshold` | 相似度門檻 | 0.7-0.85 | 需根據資料調整 |
| `index_type` | 索引類型 | HNSW | 平衡速度與精度 |
| `ef_construction` | HNSW 建構參數 | 200 | 影響索引品質 |
| `ef_search` | HNSW 搜尋參數 | 100 | 影響搜尋速度 |

---

## 效能參考

[F] Milvus/Zilliz 在 768 維向量上 p50 延遲 <10ms；Pinecone/Qdrant 約 20-50ms[^BENCH_VectorDB2024]。

[I] 對於大多數 RAG 應用，延遲差異在可接受範圍內，選型應優先考慮運維成本與功能需求。

---

## 相關連結

- **能力卡**：[[RAG問答_RAG-QA]]
- **Playbook**：[[RAG_企業知識問答_Playbook]]

---

## 過期政策（Expiry Policy）

| 項目 | 值 |
|------|------|
| **過期週期** | 6 個月 |
| **過期日期** | 2025-07-XX |
| **驗證觸發** | 價格變動 / 新版本發布 / 新產品上市 |

### 需驗證項目

- [ ] 向量資料庫價格是否變動
- [ ] 是否有新的主流向量資料庫
- [ ] Embedding 模型 MTEB 排名變化
- [ ] 各資料庫功能更新

### 更新來源

- 各向量資料庫官方 changelog
- MTEB Leaderboard
- 官方定價頁面

---

## 參考來源

[^API_OpenAI_Embeddings]: OpenAI. Embeddings API Documentation. 參見 [[OpenAI_StructuredOutputs]]

[^BENCH_VectorDB2024]: 向量資料庫比較。參見 [[VectorDB_Comparison_2025]]

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Status | Stable |
| 過期日期 | 2025-07-XX |
| 待補 Evidence | Embedding 模型比較文件 |
