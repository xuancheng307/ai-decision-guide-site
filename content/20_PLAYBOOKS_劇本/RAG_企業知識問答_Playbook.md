---
type: playbook
title: "RAG 企業知識問答 Playbook"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [RAG, knowledge-base, QA, enterprise]
status: stable
evidence_level: E3
---

# RAG 企業知識問答 Playbook

> **目標**：建立企業內部知識庫問答系統，讓員工能用自然語言查詢 SOP、FAQ、產品文件等。

---

## 適用場景與前提條件

### 適用場景

- [x] 企業內部知識庫（SOP、FAQ、政策文件）
- [x] 客服知識輔助
- [x] 產品文件查詢
- [x] 新人 onboarding 輔助

### 前提條件

| 條件 | 說明 | 檢查方式 |
|------|------|---------|
| 知識庫規模 | > 10 篇文件 | 文件清單 |
| 文件品質 | 內容正確、結構清晰 | 人工抽查 |
| 更新頻率 | 可定期同步 | 確認流程 |
| 查詢類型 | 以事實查詢為主 | 樣本分析 |

---

## 參考架構

```
┌─────────────────────────────────────────────────────────────┐
│                     使用者介面                               │
│                   (Chat / API)                              │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   Query 處理層                               │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                   │
│  │ 意圖分類 │→ │ Query    │→ │ Query    │                   │
│  │          │  │ 改寫     │  │ Embedding│                   │
│  └──────────┘  └──────────┘  └──────────┘                   │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   檢索層                                     │
│  ┌──────────────────────────────────────┐                   │
│  │        Hybrid Search                  │                   │
│  │   (BM25 + Dense Vector)               │                   │
│  └──────────────────────────────────────┘                   │
│                      │                                       │
│                      ▼                                       │
│  ┌──────────────────────────────────────┐                   │
│  │           Reranker                    │                   │
│  │    (Cross-Encoder / ColBERT)          │                   │
│  └──────────────────────────────────────┘                   │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   生成層                                     │
│  ┌──────────────────────────────────────┐                   │
│  │    Prompt + Retrieved Context         │                   │
│  │              ↓                         │                   │
│  │           LLM                          │                   │
│  │              ↓                         │                   │
│  │    Answer + Citations                  │                   │
│  └──────────────────────────────────────┘                   │
└─────────────────────────────────────────────────────────────┘
```

---

## 分步實作指南

### Step 1：文件準備與索引（Indexing）

#### 1.1 文件收集

```
- 確認文件來源（SharePoint / Confluence / 本地）
- 確認文件格式（PDF / Word / Markdown）
- 建立文件清單和元資料
```

#### 1.2 文件處理

| 步驟 | 工具選項 | 備註 |
|------|---------|------|
| PDF 解析 | PyMuPDF, pdfplumber | 保留結構 |
| Chunking | LangChain, LlamaIndex | 見下方參數 |
| Metadata 抽取 | 自訂邏輯 | 標題、日期、來源 |

#### 1.3 Chunking 參數

[F] 較小的 chunk（64-128 tokens）對於事實性答案最佳；較大的 chunk（512-1024 tokens）對於需要上下文理解的查詢更好[^RAG_ChunkSize2025]。

| 查詢類型 | 建議 chunk size | overlap |
|----------|----------------|---------|
| Factoid（事實查詢） | 256-512 tokens | 50-100 |
| Analytical（分析查詢） | 512-1024 tokens | 100-200 |
| [H] 一般建議 | 512 tokens | 100 |

#### 1.4 Embedding 與索引

| 組件 | 建議選項 | 備註 |
|------|---------|------|
| Embedding Model | text-embedding-3-small | 成本效益 |
| Vector DB（PoC） | Chroma | 本地、快速 |
| Vector DB（Prod） | Pinecone / Weaviate | 託管或自建 |

---

### Step 2：檢索設計

#### 2.1 基礎檢索

```python
# 偽代碼
query_embedding = embed(query)
results = vector_db.search(query_embedding, top_k=20)
```

#### 2.2 Hybrid Search（建議）

[F] 使用全文、dense vector 和 sparse vector 搜尋的 Blended RAG 優於純 vector 和雙向混合搜尋[^RAG_HybridSearch2024]。

| 組件 | 權重（建議起始值） | 備註 |
|------|-------------------|------|
| BM25（關鍵字） | 30% | 精確匹配 |
| Dense Vector | 70% | 語義匹配 |

#### 2.3 Reranker

[F] 進一步加入 ColBERT 作為 reranker 可獲得更顯著改進[^RAG_HybridSearch2024]。

| Reranker 選項 | 特點 |
|--------------|------|
| BGE-reranker | 開源、效果好 |
| Cohere Rerank | API、簡單 |
| ColBERT | 效率與效果平衡 |

---

### Step 3：生成設計

#### 3.1 Prompt 模板

```
你是企業知識助手。根據以下參考資料回答問題。

規則：
1. 只根據參考資料回答，不要編造
2. 如果資料不足以回答，說明「根據現有資料無法回答」
3. 引用來源文件

參考資料：
{context}

問題：{query}

回答：
```

#### 3.2 模型選擇

| 場景 | 建議模型 | 備註 |
|------|---------|------|
| 一般企業 | GPT-4o-mini | 成本效益 |
| 高品質需求 | GPT-4o / Claude 3.5 | 更準確 |
| 隱私優先 | Llama 3 (自建) | 資料不出境 |

---

### Step 4：評測與優化

#### 4.1 評測指標

[F] RAGAS 提供不需要人工標註 ground truth 的 RAG 評測方法[^RAGAS_Es2023]。

| 指標 | 目標 | 測量方式 |
|------|------|---------|
| **Faithfulness** | > 80% | RAGAS |
| **Answer Relevancy** | > 85% | RAGAS |
| **Context Precision** | > 70% | RAGAS |
| **延遲** | < 3 秒 | 端到端測量 |

#### 4.2 評測流程

```
1. 準備 100+ 測試問答對
2. 執行評測（RAGAS / DeepEval）
3. 分析錯誤案例
4. 調整參數（chunk size, top_k, prompt）
5. 重新評測
```

---

## 成本估算方法

### 一次性成本

| 項目 | 估算方式 | 範例（10,000 頁文件） |
|------|---------|---------------------|
| Embedding | $0.02 / 1M tokens | ~$1-5 |
| 開發人力 | 依團隊 | 2-4 週 |

### 運營成本（月度）

| 項目 | 估算方式 | 範例（10,000 查詢/月） |
|------|---------|----------------------|
| LLM API | $0.01-0.05 / query | $100-500 |
| Vector DB | 依選項 | $0-100（Pinecone） |
| Reranker | 依選項 | $0-50 |

---

## 常見陷阱與修法

| 陷阱 | 症狀 | 修法 |
|------|------|------|
| **Chunk 太大** | 檢索到的 context 不精確 | 減小 chunk size |
| **Chunk 太小** | 缺少上下文 | 增加 chunk size 或 overlap |
| **只用 Dense** | 精確關鍵字查不到 | 加入 BM25 混合搜尋 |
| **Top-K 太小** | 遺漏相關資料 | 增加 top_k + reranker |
| **Top-K 太大** | Lost in Middle | 限制 context，用 reranker |
| **Prompt 不當** | 幻覺、答非所問 | 迭代優化 prompt |
| **無引用機制** | 無法驗證答案 | 強制引用來源 |

[F] LLM 在處理長 context 時，對「中間」的資訊表現最差（U-shaped curve）[^LostInMiddle_Liu2023]。

---

## Gate 標準

| 階段 | 指標要求 | 檢查項目 |
|------|---------|---------|
| **PoC → Pilot** | Faithfulness > 70% | 100 題測試 |
| **Pilot → Prod** | Faithfulness > 80%, 延遲 < 3s | 500 題 + 真實用戶 |
| **Prod 維護** | Faithfulness 變化 < -5% | 持續監控 |

---

## 相關連結

- **能力卡**：[[RAG問答_RAG-QA]]
- **工具卡**：[[VectorRetrieval_向量檢索與向量庫]], [[Orchestration_工作流與編排]], [[Evaluation_評測與可觀測性]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]], [[資料治理與權限_Data-Governance-Access-Control]]

---

## 參考來源

[^RAG_Lewis2020]: Lewis, P. et al. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. 參見 [[RAG_Lewis_2020]]

[^RAGAS_Es2023]: RAGAS: Automated Evaluation of Retrieval Augmented Generation. 參見 [[RAGAS_2023]]

[^LostInMiddle_Liu2023]: Lost in the Middle: How Language Models Use Long Contexts. 參見 [[LostInTheMiddle_Liu_2023]]

[^RAG_ChunkSize2025]: Rethinking Chunk Size for Long-Document Retrieval. arXiv:2505.21700. 參見 [[RAG_ChunkSize_2025]]

[^RAG_HybridSearch2024]: Blended RAG: Improving RAG Accuracy with Hybrid Query-Based Retrievers. arXiv:2404.07220. 參見 [[RAG_HybridSearch_2024]]

[^Hallucination_Huang2023]: A Survey on Hallucination in Large Language Models. 參見 [[Hallucination_Survey_2023]]
