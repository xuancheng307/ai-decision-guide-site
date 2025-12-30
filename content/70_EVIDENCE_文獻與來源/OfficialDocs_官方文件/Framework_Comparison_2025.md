---
id: Framework_Comparison_2025
type: evidence
title: "LLM 框架比較（LangChain vs LlamaIndex）"
source_type: official_doc
source_org: Multiple (Official Documentation)
publication_date: 2025-01-XX
evidence_level: E2
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
expiry_date: 2025-07-XX
tags: [framework, LangChain, LlamaIndex, orchestration, RAG]
---

# LLM 框架比較（LangChain vs LlamaIndex）

## 來源資訊

| 項目 | 內容 |
|------|------|
| **標題** | 主流 LLM 開發框架官方文檔比較 |
| **來源** | 各框架官方文檔 |
| **整理日期** | 2025-01-XX |
| **過期日期** | 2025-07-XX（6 個月後需重新驗證） |

---

## 摘要

本文件比較主流 LLM 開發框架 LangChain 和 LlamaIndex 的設計理念、功能特性和適用場景。

---

## 框架概覽

### 基本資訊

| 項目 | LangChain | LlamaIndex |
|------|-----------|------------|
| **官網** | https://langchain.com | https://llamaindex.ai |
| **文檔** | https://python.langchain.com/docs | https://docs.llamaindex.ai |
| **GitHub** | langchain-ai/langchain | run-llama/llama_index |
| **語言** | Python, JavaScript | Python, TypeScript |
| **開源** | 是（MIT） | 是（MIT） |
| **核心定位** | 通用 LLM 應用框架 | 資料索引和查詢框架 |

### 設計理念

| 面向 | LangChain | LlamaIndex |
|------|-----------|------------|
| **核心抽象** | Chain, Agent, Tool | Index, Query Engine, Retriever |
| **設計焦點** | 組合性、模組化 | 資料處理、檢索優化 |
| **適用範圍** | 廣泛 LLM 應用 | 專注 RAG 和資料查詢 |
| **學習曲線** | 中等 | 較低（RAG 場景） |

---

## 功能比較

### 核心功能

| 功能 | LangChain | LlamaIndex | 備註 |
|------|-----------|------------|------|
| **RAG** | ✅ | ✅ | LlamaIndex 更專注 |
| **Agent** | ✅ | ✅ | LangChain 更成熟 |
| **多模態** | ✅ | ✅ | 都支援 |
| **Structured Output** | ✅ | ✅ | 都支援 |
| **Streaming** | ✅ | ✅ | 都支援 |
| **Memory** | ✅ | ✅ | LangChain 更豐富 |
| **Callbacks/Tracing** | ✅ (LangSmith) | ✅ (Arize, etc.) | 生態不同 |

### 資料處理

| 功能 | LangChain | LlamaIndex | 備註 |
|------|-----------|------------|------|
| **文件載入** | 廣泛支援 | 廣泛支援 | LlamaIndex Hub 更豐富 |
| **分塊策略** | 基本 | 豐富 | LlamaIndex 更多選項 |
| **索引類型** | 基本 | 豐富 | LlamaIndex 專長 |
| **查詢優化** | 中等 | 豐富 | LlamaIndex 專長 |
| **評測工具** | 中等 | 豐富 | LlamaIndex 內建 |

### 向量庫整合

| 向量庫 | LangChain | LlamaIndex |
|--------|-----------|------------|
| Pinecone | ✅ | ✅ |
| Milvus | ✅ | ✅ |
| Weaviate | ✅ | ✅ |
| Qdrant | ✅ | ✅ |
| Chroma | ✅ | ✅ |
| pgvector | ✅ | ✅ |

### LLM 整合

| 模型 | LangChain | LlamaIndex |
|------|-----------|------------|
| OpenAI | ✅ | ✅ |
| Anthropic | ✅ | ✅ |
| Google (Gemini) | ✅ | ✅ |
| Azure OpenAI | ✅ | ✅ |
| 本地模型 (Ollama) | ✅ | ✅ |
| HuggingFace | ✅ | ✅ |

---

## 架構差異

### LangChain 架構

```
LangChain 核心概念：

┌─────────────────────────────────────────┐
│  Application                            │
├─────────────────────────────────────────┤
│  Chains / Agents / Graphs (LCEL/LangGraph) │
├─────────────────────────────────────────┤
│  Components (LLMs, Retrievers, Tools)   │
├─────────────────────────────────────────┤
│  Integrations (向量庫、API、資料源)       │
└─────────────────────────────────────────┘

特點：
- LCEL (LangChain Expression Language) 聲明式組合
- LangGraph 支援複雜工作流
- 強調組件的可組合性
```

### LlamaIndex 架構

```
LlamaIndex 核心概念：

┌─────────────────────────────────────────┐
│  Application                            │
├─────────────────────────────────────────┤
│  Query Engine / Chat Engine             │
├─────────────────────────────────────────┤
│  Index (VectorIndex, TreeIndex, etc.)   │
├─────────────────────────────────────────┤
│  Data Connectors (Loaders, Readers)     │
└─────────────────────────────────────────┘

特點：
- 專注資料索引和檢索
- 多種索引類型優化不同查詢
- 內建評測和優化工具
```

---

## 選型建議

### 依場景推薦

| 場景 | 推薦 | 理由 |
|------|------|------|
| **純 RAG 應用** | LlamaIndex | 專為 RAG 設計，更多優化選項 |
| **複雜 Agent** | LangChain | Agent 生態更成熟 |
| **工作流編排** | LangChain (LangGraph) | 更完整的編排能力 |
| **快速原型** | 兩者皆可 | 依熟悉度選擇 |
| **企業生產** | 兩者皆可 | 依需求和團隊選擇 |
| **多資料源整合** | LlamaIndex | LlamaHub 整合豐富 |

### 決策樹

```
開始
├─ 主要是 RAG/知識問答？
│   ├─ 是 → LlamaIndex（更專精）
│   └─ 否 → 繼續
├─ 需要複雜 Agent/工作流？
│   ├─ 是 → LangChain（更靈活）
│   └─ 否 → 繼續
├─ 團隊熟悉度？
│   ├─ 有 LangChain 經驗 → LangChain
│   ├─ 有 LlamaIndex 經驗 → LlamaIndex
│   └─ 都沒有 → 依場景選擇或兩者結合
```

### 可以結合使用

```python
# LangChain 和 LlamaIndex 可以結合
from llama_index.core import VectorStoreIndex
from langchain.agents import AgentExecutor

# 使用 LlamaIndex 建立索引
index = VectorStoreIndex.from_documents(documents)
query_engine = index.as_query_engine()

# 將 LlamaIndex 查詢引擎作為 LangChain 工具
from langchain.tools import Tool
tool = Tool(
    name="knowledge_base",
    func=query_engine.query,
    description="Search the knowledge base"
)

# 在 LangChain Agent 中使用
```

---

## 可引用事實

### [F] 基本事實

1. **LangChain** 是通用 LLM 應用開發框架，支援 Chain、Agent、Tool 等抽象
2. **LlamaIndex** 專注於資料索引和查詢，提供多種索引類型
3. 兩者都是開源框架（MIT 授權）
4. 兩者都支援主流向量資料庫和 LLM 提供者
5. 兩者可以結合使用

### 版本資訊（2025-01）

- LangChain: v0.3.x（Python）
- LlamaIndex: v0.11.x（Python）

> 注意：版本更新頻繁，功能可能變動

---

## 生態系統

### LangChain 生態

| 產品 | 說明 |
|------|------|
| **LangChain** | 核心框架 |
| **LangGraph** | 工作流編排 |
| **LangSmith** | 追蹤、評測、監控 |
| **LangServe** | API 部署 |

### LlamaIndex 生態

| 產品 | 說明 |
|------|------|
| **LlamaIndex** | 核心框架 |
| **LlamaHub** | 資料連接器市集 |
| **LlamaParse** | 文件解析服務 |
| **LlamaCloud** | 託管服務 |

---

## 相關連結

- **工具卡**：[[Orchestration_工作流與編排]]
- **能力卡**：[[RAG問答_RAG-QA]]
- **Playbook**：[[RAG_企業知識問答_Playbook]]
- **相關 Evidence**：[[VectorDB_Comparison_2025]]

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Evidence Level | E2（官方文檔整理） |
| 過期日期 | 2025-07-XX（需定期更新） |
| 備註 | 框架發展快速，功能和 API 可能變動 |
