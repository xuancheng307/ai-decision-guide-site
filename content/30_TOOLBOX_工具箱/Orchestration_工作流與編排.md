---
type: tool
title: "工作流與編排 (Orchestration & Workflow)"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
expiry_date: 2025-07-XX
expiry_policy: 6_months
tags: [orchestration, workflow, LangChain, LlamaIndex, agent]
status: stable
---

# 工作流與編排 (Orchestration & Workflow)

> **一句話**：將 LLM 呼叫、檢索、工具使用等步驟串聯成可控的工作流程。

---

## 核心概念

| 概念 | 說明 | 範例 |
|------|------|------|
| **Chain** | 線性串聯多個步驟 | Query → Retrieve → Generate |
| **Agent** | LLM 自主決定下一步行動 | ReAct, Tool-use Agent |
| **Router** | 根據輸入分流到不同處理路徑 | 分類後路由到專門模組 |
| **Memory** | 維護對話歷史與狀態 | ConversationBuffer, Summary |

---

## 主要框架比較

| 框架 | 定位 | 優點 | 缺點 | 適用場景 |
|------|------|------|------|---------|
| **LangChain** | 通用編排 | 生態豐富、文件完整 | 抽象層多、學習曲線 | 複雜工作流 |
| **LlamaIndex** | 資料索引優先 | RAG 原生支援強 | Agent 功能較弱 | 資料密集型 RAG |
| **Semantic Kernel** | 企業整合 | Microsoft 生態整合 | 社群較小 | .NET/Azure 環境 |
| **Haystack** | Pipeline 導向 | 模組化清晰 | 彈性略低 | 標準 NLP Pipeline |
| **Dify** | Low-code | 視覺化、快速部署 | 客製化受限 | 快速 PoC |

---

## LangChain vs LlamaIndex 選擇

```
你的核心需求是什麼？
├── 複雜 Agent / 多工具協作 → LangChain
├── 純 RAG / 資料索引查詢 → LlamaIndex
├── 兩者都需要 → 可混用（各取所長）
└── 快速 PoC / 非工程師 → Dify / Flowise
```

---

## 關鍵設計模式

### 1. 基礎 RAG Chain

```
User Query
    ↓
Embedding → Vector Search → Top-K Documents
    ↓
Prompt Template + Retrieved Context
    ↓
LLM Generation → Response
```

### 2. RAG + Reranker

```
User Query
    ↓
Embedding → Vector Search → Top-20 Documents
    ↓
Reranker → Top-5 Documents
    ↓
LLM Generation → Response
```

### 3. Agentic RAG

```
User Query
    ↓
Router (分類查詢類型)
    ↓
├── 簡單查詢 → 基礎 RAG
├── 多步查詢 → Decompose → 多次檢索 → 合成
└── 需外部資料 → Tool Call → 整合結果
    ↓
LLM Generation → Response
```

---

## 常見陷阱

| 陷阱 | 症狀 | 解法 |
|------|------|------|
| **過度抽象** | 簡單任務用複雜 Agent | 從 Chain 開始，需要時才升級 |
| **Memory 爆炸** | 長對話 token 超限 | 使用 Summary Memory 或滑動窗口 |
| **Agent 迴圈** | Agent 重複呼叫同一工具 | 設定 max_iterations、改進 prompt |
| **延遲累積** | 多步驟導致回應慢 | 並行化、streaming、快取 |

---

## 相關連結

- **能力卡**：[[RAG問答_RAG-QA]]
- **Playbook**：[[RAG_企業知識問答_Playbook]], [[客服工單自動化_Playbook]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]]

---

## 過期政策（Expiry Policy）

| 項目 | 值 |
|------|------|
| **過期週期** | 6 個月 |
| **過期日期** | 2025-07-XX |
| **驗證觸發** | 框架重大版本更新 / API 變更 / 新框架出現 |

### 需驗證項目

- [ ] LangChain 版本更新和 API 變化
- [ ] LlamaIndex 版本更新和 API 變化
- [ ] 是否有新的主流框架
- [ ] 框架功能比較是否仍準確

### 更新來源

- LangChain / LlamaIndex 官方 changelog
- 框架官方 blog
- 社群討論和採用趨勢

---

## 參考來源

[^DOC_LangChain]: LangChain Documentation. 參見 [[Framework_Comparison_2025]]

[^DOC_LlamaIndex]: LlamaIndex Documentation. 參見 [[Framework_Comparison_2025]]

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Status | Stable |
| 過期日期 | 2025-07-XX |
| 待補 Evidence | Agent 工作流論文 |
