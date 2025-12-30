---
type: bottleneck
title: "延遲與成本（Latency & Cost）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [latency, cost, token, optimization, caching]
status: draft
evidence_level: E3
---

# 延遲與成本（Latency & Cost）

> **一句話**：LLM 應用的延遲和成本會隨著規模快速增長，不控制會讓 ROI 翻負。

---

## 風險分類

### 成本風險

| 風險類型 | 描述 | 影響 |
|----------|------|------|
| **Token 爆炸** | Context 過長、重複查詢 | 成本失控 |
| **模型選錯** | 用 GPT-4 做 GPT-4o-mini 能做的事 | 成本 10-50x |
| **快取缺失** | 相同查詢重複呼叫 | 冗餘成本 |
| **Retrieval 過度** | Top-K 過大、不必要的 rerank | 額外成本 |

### 延遲風險

| 風險類型 | 描述 | 影響 |
|----------|------|------|
| **冷啟動** | 首次請求延遲高 | 用戶體驗差 |
| **串接延遲** | 多步驟 pipeline 累加 | 總延遲超標 |
| **網路延遲** | 跨區域 API 呼叫 | 不穩定 |
| **Token 生成** | 長輸出逐 token 生成 | 等待時間長 |

---

## 成本估算模型

### 基礎公式

```
單次請求成本 = (Input Tokens × Input Price) + (Output Tokens × Output Price)
              + Embedding Cost (if RAG)
              + Reranker Cost (if used)
              + Vector DB Cost (per query)
```

### 常見模型價格（2025-01 參考）

| 模型 | Input ($/1M tokens) | Output ($/1M tokens) | 適用場景 |
|------|---------------------|----------------------|---------|
| **GPT-4o** | $2.50 | $10.00 | 複雜推理、高品質 |
| **GPT-4o-mini** | $0.15 | $0.60 | 一般任務、成本敏感 |
| **Claude 3.5 Sonnet** | $3.00 | $15.00 | 長 context、高品質 |
| **Claude 3.5 Haiku** | $0.25 | $1.25 | 快速回應、成本敏感 |
| **text-embedding-3-small** | $0.02 | - | Embedding |

### RAG 系統成本模型

```
每查詢成本 = Embedding($0.02/1M × query_tokens)
           + Vector Search($0.01-0.05/query，依 DB)
           + Reranker($0.02-0.10/query，依方案)
           + LLM Generation(見上表)
```

**範例：10,000 查詢/月的 RAG 系統**

| 組件 | 單價 | 月成本 |
|------|------|--------|
| Query Embedding | $0.02/1M × 500 tokens × 10K | ~$0.10 |
| Vector DB (Pinecone) | $70/月起 | $70 |
| Reranker (Cohere) | $0.05/query | $500 |
| GPT-4o-mini Generation | $0.15/1M × 2K tokens × 10K | ~$3 |
| **月總成本** | | **~$573** |

---

## 延遲分解

### 典型 RAG Pipeline 延遲

| 階段 | 典型延遲 | 可優化空間 |
|------|---------|-----------|
| Query Embedding | 50-100ms | 快取、批次 |
| Vector Search | 20-100ms | 索引優化 |
| Reranking | 100-300ms | 減少候選數 |
| LLM Generation | 500-3000ms | 模型選擇、Streaming |
| **總延遲** | **700-3500ms** | |

### 延遲目標建議

| 場景 | P50 目標 | P95 目標 |
|------|---------|---------|
| 即時客服 | < 2s | < 5s |
| 內部工具 | < 3s | < 8s |
| 批次處理 | N/A | N/A |

---

## 可觀測指標清單

### 必須監控

| 指標 | 定義 | 告警閾值（建議） |
|------|------|-----------------|
| **p50_latency** | 50% 請求的延遲 | 依場景 |
| **p95_latency** | 95% 請求的延遲 | > 目標 1.5x |
| **tokens_per_request** | 每請求 token 數 | 突增 > 50% |
| **cost_per_request** | 每請求成本 | 超預算 |
| **daily_cost** | 每日總成本 | 超預算 |
| **error_rate** | 錯誤率 | > 1% |

### 建議監控

| 指標 | 定義 | 用途 |
|------|------|------|
| **cache_hit_rate** | 快取命中率 | 優化機會 |
| **retrieval_recall** | 檢索召回率（proxy） | 品質監控 |
| **token_waste_ratio** | Context 中未使用比例 | 成本優化 |
| **model_distribution** | 不同模型使用比例 | 成本分析 |

---

## 緩解策略

### 策略 1：模型分層（Model Tiering）

```
簡單問題 → GPT-4o-mini / Haiku
複雜問題 → GPT-4o / Sonnet
判斷邏輯 → 先用小模型分類，再決定路由
```

**效益**：可降低 60-80% 成本

### 策略 2：智能快取

| 快取類型 | 適用場景 | 實作方式 |
|----------|---------|---------|
| **Semantic Cache** | 相似查詢 | Embedding 相似度 > 0.95 |
| **Exact Cache** | 完全相同查詢 | Hash key |
| **Prompt Cache** | 固定 system prompt | OpenAI Prompt Caching |

**效益**：命中率 30-50% 可降低等比例成本

### 策略 3：Context 優化

| 方法 | 說明 | 效益 |
|------|------|------|
| **減少 Top-K** | 從 20 降到 5-10 | 減少 token |
| **摘要 Context** | 先摘要再送入 | 減少 50%+ token |
| **動態 Chunk** | 依查詢調整 chunk 數 | 精準使用 |

### 策略 4：Streaming

```
啟用 streaming 不降低總延遲，但改善感知延遲
首 token 時間：100-500ms（vs 全部生成 2-3s）
```

### 策略 5：批次處理

| 場景 | 方法 | 效益 |
|------|------|------|
| 非即時任務 | 累積後批次送出 | 減少 overhead |
| 大量文件 | 並行處理 + 限流 | 提升吞吐 |

---

## 反模式（Anti-patterns）

| 反模式 | 描述 | 後果 | 修正 |
|--------|------|------|------|
| **一律用最強模型** | 所有請求都用 GPT-4 | 成本爆炸 | 模型分層 |
| **Context 塞滿** | 把 128K context 塞滿 | 成本 + Lost in Middle | 控制 context |
| **無快取設計** | 相同問題反覆呼叫 API | 冗餘成本 | 加 cache |
| **同步阻塞** | 等 LLM 完成才回應 | 延遲差 | Streaming |
| **無監控** | 不知道花了多少錢 | 月底帳單驚嚇 | 加監控 |
| **Top-K 過大** | 檢索 50 個 chunk | Context 爆、成本高 | 減少 + rerank |

---

## 驗收 Gate

| 階段 | 成本指標 | 延遲指標 |
|------|---------|---------|
| **PoC** | 單次成本 < $0.10 | P95 < 10s |
| **Pilot** | 日成本有預算 | P95 < 5s |
| **Production** | 月成本 < 預算 | P95 < 3s（即時場景） |

### 不准上 Production 的條件

- [ ] 無成本監控
- [ ] 無延遲監控
- [ ] 單次請求成本 > $1（非特殊場景）
- [ ] P95 延遲 > 10s（即時場景）
- [ ] 無快取機制（高頻場景）

---

## 監控 Dashboard 建議欄位

```
┌─────────────────────────────────────────────────────────┐
│  Daily Cost: $XX.XX    MTD Cost: $XXX.XX               │
│  Budget Used: XX%      Projected: $X,XXX               │
├─────────────────────────────────────────────────────────┤
│  Requests: XX,XXX      Avg Latency: X.Xs               │
│  P95 Latency: X.Xs     Error Rate: X.X%                │
├─────────────────────────────────────────────────────────┤
│  Cache Hit Rate: XX%   Tokens/Request: X,XXX           │
│  Model: GPT-4o-mini XX% / GPT-4o XX%                   │
└─────────────────────────────────────────────────────────┘
```

---

## 相關連結

- **能力卡**：[[RAG問答_RAG-QA]], [[文件摘要_Summarization]]
- **Playbook**：[[RAG_企業知識問答_Playbook]], [[客服工單自動化_Playbook]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]]
- **工具卡**：[[Evaluation_評測與可觀測性]]

---

## 參考來源

[^API_OpenAI_Pricing]: OpenAI API Pricing. [TODO: 建立 Evidence Note - 官方文件]

[^API_Anthropic_Pricing]: Anthropic API Pricing. [TODO: 建立 Evidence Note - 官方文件]

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Status | Draft |
| 待補 Evidence | OpenAI/Anthropic 價格官方文件 |
| 待驗證 | 延遲數據需實測確認 |
