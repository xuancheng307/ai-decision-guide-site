# AI 名詞表（Glossary）

> 本知識庫常用術語的定義，按字母排序。

---

## A

### Agent
讓 AI 能夠「行動」的系統架構。Agent 可以思考、使用工具、執行多步驟任務，而不只是回答問題。

### API（Application Programming Interface）
程式之間溝通的介面。使用 AI API 意味著透過網路呼叫別人的 AI 服務。

---

## C

### Chunking
把長文件切成小段落的過程，通常用於 RAG 系統。

### Context Window
模型一次能處理的文字長度上限（以 token 計）。例如 GPT-4 有 128K context window。

---

## E

### Embedding
把文字轉換成向量（一串數字）的過程。語意相近的文字，向量也會相近。

### Eval / Evaluation
評測。用來衡量 AI 系統表現的方法和指標。

---

## F

### Fine-tuning
微調。用自己的資料進一步訓練已有的模型，讓它更適合特定任務。

---

## G

### Gate
門檻。專案進入下一階段前必須達到的條件。例如「PoC Gate」是 PoC 階段的過關條件。

### Grounding
讓 AI 的回答有所依據（如引用來源），而不是憑空生成。用來減少幻覺。

### Guardrails
護欄。用來限制 AI 行為的機制，防止不當輸出或危險操作。

---

## H

### Hallucination
幻覺。AI 生成看起來合理但實際錯誤的內容。

### Human-in-the-loop
人在迴圈中。AI 輸出需要人工覆核才能執行的設計模式。

---

## L

### Latency
延遲。從發出請求到收到回應的時間。

### LLM（Large Language Model）
大型語言模型。如 GPT-4、Claude、Llama 等。

---

## M

### MCP（Model Context Protocol）
Anthropic 提出的讓 AI 連接外部工具和資料的協議。

### MLOps
Machine Learning Operations。管理 ML 系統的開發、部署、監控的實踐。

---

## O

### Orchestration
編排。協調多個 AI 元件、工具、步驟的過程。

---

## P

### Pilot
試運行。在正式上線前，小規模真實環境測試。

### Playbook
劇本。一套完整的落地方法，包含架構、步驟、驗收條件。

### PoC（Proof of Concept）
概念驗證。用最小成本驗證想法可行性的階段。

### Prompt
提示詞。給 AI 的指令或問題。

### Prompt Engineering
提示詞工程。設計和優化 prompt 的技術。

### Prompt Injection
提示詞注入。惡意輸入企圖操控 AI 行為的攻擊方式。

---

## R

### RAG（Retrieval-Augmented Generation）
檢索增強生成。先從資料庫檢索相關資訊，再讓 AI 根據這些資訊回答。

### RBAC（Role-Based Access Control）
基於角色的存取控制。根據使用者角色決定能看什麼資料。

### ROI（Return on Investment）
投資報酬率。衡量投入和產出的比例。

---

## S

### SLA（Service Level Agreement）
服務等級協議。對系統可用性、回應時間等的承諾。

### Serving
模型服務。把訓練好的模型部署成可用的服務。

---

## T

### Token
模型處理文字的最小單位。大約 1 個中文字 = 1-2 tokens，1 個英文單字 = 1-4 tokens。

### Tool Use
工具使用。讓 AI 能呼叫外部工具（搜尋、計算、API...）的能力。

### Tracing
追蹤。記錄 AI 系統每一步執行過程的機制，用於除錯和監控。

---

## V

### Vector Database
向量資料庫。專門儲存和搜尋 embedding 向量的資料庫，用於 RAG。

---

## W

### Workflow
工作流。把多個步驟串起來的自動化流程。

---

## 持續更新

遇到新術語會持續補充。如有建議，歡迎回報。

**最後更新**：2025-01-XX
