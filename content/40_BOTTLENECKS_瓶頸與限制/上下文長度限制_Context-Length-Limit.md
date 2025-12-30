---
type: bottleneck
title: "上下文長度限制（Context Length Limit）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [context-length, token-limit, long-context, chunking]
status: stable
evidence_level: E3
---

# 上下文長度限制（Context Length Limit）

> **一句話**：每個 LLM 都有 token 上限，且長 context 會導致效能下降和成本增加。

---

## 風險分類

### 硬性限制

| 模型 | Context Window | 輸出上限 | 備註 |
|------|---------------|---------|------|
| **GPT-4o** | 128K tokens | 16K | 主流選擇 |
| **GPT-4o-mini** | 128K tokens | 16K | 成本友善 |
| **Claude 3.5 Sonnet** | 200K tokens | 8K | 最長 context |
| **Claude 3.5 Haiku** | 200K tokens | 8K | 快速且長 |
| **Gemini 1.5 Pro** | 2M tokens | 8K | 實驗性超長 |

### 軟性限制（效能下降）

| 問題 | 描述 | 影響 |
|------|------|------|
| **Lost in the Middle** | 中間資訊效能最差 | 關鍵資訊遺漏 |
| **注意力稀釋** | Context 過長導致注意力分散 | 回答品質下降 |
| **成本線性增長** | Token 數 × 單價 | 成本失控 |
| **延遲增加** | 處理時間增加 | 用戶體驗差 |

[F] LLM 在處理長 context 時，對「中間」的資訊表現最差（U-shaped curve）[^LostInMiddle_Liu2023]。

---

## 症狀識別

### 常見症狀

| 症狀 | 描述 | 檢測方式 |
|------|------|---------|
| **回答不完整** | 遺漏重要資訊 | 比對 context 內容 |
| **忽略指令** | 不遵守 prompt 中的要求 | 指令追蹤測試 |
| **重複內容** | 生成重複段落 | 輸出分析 |
| **Token 超限錯誤** | API 回傳錯誤 | 錯誤日誌監控 |
| **回答品質下降** | 長 context 時準確率降低 | A/B 測試 |

### 位置效應

```
Context 位置效能分佈（U-shaped）：

開頭 ████████████ 高效能
中段 ████         低效能（Lost in the Middle）
結尾 ██████████   中高效能
```

---

## 根因分析

### 架構限制

- **Transformer 注意力機制**：計算複雜度 O(n²)
- **位置編碼限制**：超出訓練長度效能下降
- **記憶體限制**：GPU 記憶體隨 context 增加

### 訓練限制

- **訓練資料長度分佈**：多數訓練樣本較短
- **長 context 訓練成本高**：難以充分訓練
- **位置泛化問題**：超出訓練分佈表現差

---

## 緩解策略

### 策略 1：智能分塊（Smart Chunking）

[F] 小 chunk（64-128 tokens）適合事實查詢，大 chunk（512-1024 tokens）適合分析查詢[^RAG_ChunkSize2025]。

| 場景 | 建議 Chunk Size | 原因 |
|------|----------------|------|
| 事實查詢 | 64-128 tokens | 精確定位 |
| 分析查詢 | 512-1024 tokens | 保留上下文 |
| 長文件 | 分層摘要 | 減少 token |

### 策略 2：檢索增強（RAG）

```
完整文件 → 分塊 + Embedding → 向量庫
                ↓
查詢 → 檢索相關 chunk → 只送相關內容到 LLM
```

**效益**：將 10 萬 token 文件壓縮到 2-5K tokens

### 策略 3：分層摘要（Hierarchical Summarization）

| 層級 | 內容 | Token 數 |
|------|------|---------|
| L0 | 原始文件 | 100K |
| L1 | 章節摘要 | 10K |
| L2 | 全文摘要 | 2K |

**流程**：先用 L2 判斷相關性 → 再檢索 L1/L0 細節

### 策略 4：Map-Reduce

```
長文件 → 分割成 N 塊
      → 每塊獨立處理（Map）
      → 合併結果（Reduce）
```

**適用**：摘要、資訊抽取、分析報告

### 策略 5：重要資訊置前/置後

```
Prompt 結構建議：
[系統指令]           ← 開頭，高注意力
[最重要的 context]   ← 開頭附近
[次要 context]       ← 中間
[用戶問題]           ← 結尾，高注意力
```

### 策略 6：Context 壓縮

| 方法 | 說明 | 壓縮率 |
|------|------|--------|
| **LLMLingua** | 移除低資訊量 token | 2-10x |
| **Selective Context** | 選擇性保留 | 2-5x |
| **摘要替代** | 用摘要取代原文 | 5-20x |

---

## 可觀測指標

### 必須監控

| 指標 | 定義 | 告警閾值（建議） |
|------|------|--------------------|
| **avg_input_tokens** | 平均輸入 token 數 | 接近上限 80% |
| **max_input_tokens** | 最大輸入 token 數 | 超過上限 |
| **truncation_rate** | 被截斷請求比例 | > 1% |
| **context_utilization** | 實際使用/可用 context | > 80% 需警示 |

### 建議監控

| 指標 | 定義 | 用途 |
|------|------|------|
| **chunk_hit_rate** | RAG 檢索命中率 | 檢索品質 |
| **position_distribution** | 關鍵資訊在 context 中的位置 | 優化提示 |
| **compression_ratio** | 壓縮前後比例 | 壓縮效果 |

---

## 反模式（Anti-patterns）

| 反模式 | 描述 | 後果 | 修正 |
|--------|------|------|------|
| **塞滿 Context** | 把可用 context 塞滿 | Lost in Middle、成本高 | 只送必要資訊 |
| **固定 Chunk Size** | 所有場景用同一 size | 效果不佳 | 依場景調整 |
| **忽略位置效應** | 重要資訊放中間 | 資訊遺漏 | 置前或置後 |
| **無 RAG 直送** | 整份文件直接送入 | Token 超限、成本高 | 加入 RAG |
| **Top-K 過大** | 檢索太多 chunk | Context 爆 | 減少 + rerank |
| **不監控 token** | 不知道用了多少 token | 成本失控 | 加監控 |

---

## 驗收 Gate

| 階段 | 指標要求 |
|------|---------|
| **PoC** | Context 使用 < 80% 上限，無截斷 |
| **Pilot** | 有 RAG 或分塊機制，truncation_rate < 1% |
| **Production** | 有 token 監控，有超限告警 |

### 不准上 Production 的條件

- [ ] 無 token 使用監控
- [ ] truncation_rate > 5%
- [ ] 平均 context 使用 > 90% 上限
- [ ] 無 context 管理策略（RAG/分塊/摘要）

---

## 模型選擇指南

| 需求 | 建議模型 | 原因 |
|------|---------|------|
| 超長文件（>100K） | Claude 3.5 Sonnet | 200K context |
| 一般長度（<50K） | GPT-4o / GPT-4o-mini | 性價比 |
| 極長文件（>500K） | Gemini 1.5 Pro | 2M context（實驗性） |
| 成本敏感 | GPT-4o-mini + RAG | 減少 token 使用 |

---

## 相關連結

- **能力卡**：[[RAG問答_RAG-QA]], [[文件摘要_Summarization]]
- **Playbook**：[[RAG_企業知識問答_Playbook]]
- **瓶頸卡**：[[延遲與成本_Latency-Cost]], [[幻覺與可追溯性_Hallucination-Grounding]]
- **工具卡**：[[VectorRetrieval_向量檢索與向量庫]]

---

## 參考來源

[^LostInMiddle_Liu2023]: Lost in the Middle: How Language Models Use Long Contexts. TACL 2024. 參見 [[LostInTheMiddle_Liu_2023]]

[^RAG_ChunkSize2025]: The Impact of Chunk Size on RAG System Performance. arXiv:2501.09345. 參見 [[RAG_ChunkSize_2025]]

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Status | Stable |
| 待補 Evidence | 各模型官方 context window 文件 |
| 待驗證 | Context 壓縮工具效果 |
