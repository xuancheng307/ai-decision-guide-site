---
type: capability
title: "RAG 問答（Retrieval-Augmented Generation QA）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [RAG, QA, retrieval, generation, enterprise]
status: stable
evidence_level: E3
---

# RAG 問答（Retrieval-Augmented Generation QA）

> **一句話**：讓 AI 先從知識庫檢索相關資訊，再根據檢索結果回答問題，降低幻覺並支援引用來源。

---

## 基本資訊

| 項目 | 內容 |
|------|------|
| **輸入** | 使用者問題 + 知識庫（文件集合） |
| **輸出** | 答案 + 引用來源（可選） |
| **成熟度** | **Pilot-ready**（需要評測和調優才能 Production） |
| **最後更新** | 2025-01-XX |

---

## 1. 能力定義（Definition）

[F] RAG（Retrieval-Augmented Generation）結合 pre-trained parametric memory（LLM）與 non-parametric memory（外部知識庫），用於 knowledge-intensive 任務。[^RAG_Lewis2020]

**核心流程**：
1. **Indexing**：將知識庫文件切分、向量化、建立索引
2. **Retrieval**：根據使用者問題，檢索相關文件片段
3. **Generation**：將檢索結果作為 context，讓 LLM 生成答案

---

## 2. 能做到的範圍（What it can do now）

### 2.1 表現良好的場景

- [x] 企業內部知識庫問答（SOP、FAQ、文件）
- [x] 客服輔助（回覆建議、知識查詢）
- [x] 文件摘要與查詢
- [x] 需要引用來源的問答

### 2.2 表現程度

| 指標 | 典型範圍 | 條件 | 來源 |
|------|---------|------|------|
| Faithfulness | 70-90% | 取決於 retrieval 品質 | [^RAGAS_Es2023] |
| Answer Relevancy | 75-95% | 取決於 prompt 設計 | [^RAGAS_Es2023] |
| 延遲 | 1-5 秒 | API 模式，含 retrieval | [H] 經驗值 |
| 成本 | $0.01-0.05 / query | GPT-4o 等級 | [^DOC_OpenAI_Pricing] |

[F] RAG 相比純 LLM 可生成更 specific、diverse、factual 的回答。[^RAG_Lewis2020]

---

## 3. 適合的任務特徵（Good fit）

這個能力適合的任務通常有以下特徵：

- [x] **有明確的知識庫**：企業文件、SOP、FAQ、產品資料
- [x] **需要可追溯性**：答案需要引用來源
- [x] **知識會更新**：比 fine-tuning 更容易更新
- [x] **容許一定錯誤**：有人工覆核機制

---

## 4. 不適合/高風險（Bad fit / Red flags）

### 4.1 不適合的場景

- [ ] **需要 100% 正確**：RAG 無法保證不幻覺
- [ ] **知識庫太小**（< 10 篇文件）：可能不需要 RAG
- [ ] **高度專業推理**：需要專業訓練或 fine-tuning
- [ ] **即時資料**：需要 real-time API 整合

### 4.2 紅旗警訊

[F] 即使使用 RAG，系統仍可能產生幻覺，RAG 無法完全消除問題。[^Hallucination_Huang2023]

- [x] **Retrieval 失敗**：找不到相關文件 → 答案可能完全幻覺
- [x] **Context 過長**：[F] LLM 對「中間」資訊處理較差（Lost in the Middle）[^LostInMiddle_Liu2023]
- [x] **權限混亂**：使用者看到不該看的內容

---

## 5. 常用落地模式（Patterns）

| 模式 | 適用情境 | 連結 |
|------|---------|------|
| **Basic RAG** | 單一知識庫問答 | [[RAG_企業知識問答_Playbook]] |
| **RAG + Reranker** | 提升檢索精度 | [[RAG_企業知識問答_Playbook]] |
| **Agentic RAG** | 多來源、多步驟查詢 | [TODO] |

---

## 6. 常用工具（Tools）

| 層級 | 工具 | 備註 |
|------|------|------|
| **模型層** | OpenAI GPT-4o, Claude 3.5 | [^DOC_OpenAI] [^DOC_Anthropic] |
| **Embedding** | OpenAI text-embedding-3, Cohere | |
| **向量資料庫** | Pinecone, Weaviate, Chroma, Qdrant | |
| **編排層** | LangChain, LlamaIndex, Dify | |
| **評測層** | RAGAS, DeepEval | [^RAGAS_Es2023] |

---

## 7. 瓶頸與對策（Bottlenecks & Mitigations）

| 瓶頸 | 症狀 | 緩解策略 | 連結 |
|------|------|---------|------|
| **幻覺** | 答案與 context 不符 | 引用機制、Faithfulness 監控 | [[幻覺與可追溯性_Hallucination-Grounding]] |
| **Retrieval 失敗** | 找不到正確文件 | Hybrid search、Reranker | [[RAG_企業知識問答_Playbook]] |
| **Lost in Middle** | 長 context 漏資訊 | 控制 context 長度、重新排序 | [^LostInMiddle_Liu2023] |
| **權限問題** | 資料外洩 | Document-level RBAC | [[資料治理與權限_Data-Governance-Access-Control]] |

---

## 8. 成熟度分級（Maturity）

| 階段 | 定義 | 這個能力的狀態 |
|------|------|---------------|
| **PoC** | 實驗室環境可行 | ✅ 容易達成 |
| **Pilot** | 小規模真實環境可行 | ✅ 需要評測和調優 |
| **Production** | 大規模穩定運行 | ⚠️ 需要完整的監控、權限、評測 |

**Production 需要**：
- 完整的評測框架（RAGAS 等）[^RAGAS_Es2023]
- 權限控管機制
- 監控和告警
- 回滾機制

---

## 9. 發展預期（Outlook & Watch signals）

### 9.1 觀測訊號

- [ ] **Long-context 模型改進**：是否解決 Lost in Middle 問題
- [ ] **評測標準化**：是否有更成熟的 benchmark
- [ ] **Agentic RAG**：多步驟 RAG 是否成熟

### 9.2 預期趨勢

| 時間範圍 | 預期變化 | 依據 |
|----------|---------|------|
| 6 個月內 | Reranker 成為標配 | [I] 當前最佳實踐趨勢 |
| 1 年內 | 評測框架更標準化 | [I] RAGAS 等框架普及 |

---

## 相關連結

- **Playbooks**：[[RAG_企業知識問答_Playbook]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]], [[資料治理與權限_Data-Governance-Access-Control]]
- **領域包**：[[SME_中小企業通用_客服與工單]]

---

## 參考來源

[^RAG_Lewis2020]: Lewis, P. et al. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. NeurIPS 2020. 參見 [[RAG_Lewis_2020]]

[^LostInMiddle_Liu2023]: Liu, N. F. et al. (2023). Lost in the Middle: How Language Models Use Long Contexts. TACL 2024. 參見 [[LostInTheMiddle_Liu_2023]]

[^RAGAS_Es2023]: Es, S. et al. (2023). RAGAS: Automated Evaluation of Retrieval Augmented Generation. EACL 2024. 參見 [[RAGAS_2023]]

[^Hallucination_Huang2023]: Huang, L. et al. (2023). A Survey on Hallucination in Large Language Models. ACM TOIS 2024. 參見 [[Hallucination_Survey_2023]]

[^DOC_OpenAI]: OpenAI Documentation. https://platform.openai.com/docs

[^DOC_Anthropic]: Anthropic. Claude API Documentation. https://docs.anthropic.com/

[^DOC_OpenAI_Pricing]: OpenAI Pricing. https://openai.com/pricing
