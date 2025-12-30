# Iteration 1 Claim List（主張清單）

> 這是 Iteration 1 所有文件的核心主張清單。
> 每個主張標記類型：[F] Fact / [I] Inference / [H] Heuristic
> 並標記需要的證據等級和狀態。

---

## 1. 能力卡：摘要_Summarization

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 1.1 | LLM 在單文件摘要任務上已達 Production-ready 成熟度 | [F] | E3 論文 | [TODO] |
| 1.2 | 摘要任務的 ROUGE 分數在特定 benchmark 上可達 XX | [F] | E3 評測 | [TODO] |
| 1.3 | 長文件摘要（>100K tokens）仍有 lost-in-the-middle 問題 | [F] | E3 論文 | [TODO] |
| 1.4 | 抽取式 vs 生成式摘要各有適用場景 | [I] | 依據 1.1-1.3 | - |
| 1.5 | 摘要幻覺率在無 grounding 時約 X%-Y% | [F] | E3/E2 評測 | [TODO] |
| 1.6 | 加入引用機制可降低幻覺至 X% 以下 | [F] | E3 論文 | [TODO] |

### 待搜尋的 Evidence

- [ ] 摘要 benchmark 論文（SummEval, FRANK...）
- [ ] Lost-in-the-middle 論文（Liu et al. 2023）
- [ ] 摘要幻覺率評測論文

---

## 2. 能力卡：分類與路由_Classification-Routing

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 2.1 | 文字分類是 LLM 最成熟的能力之一，可達 Production-ready | [F] | E3 評測 | [TODO] |
| 2.2 | Zero-shot 分類在常見類別可達 80%+ 準確率 | [F] | E3 論文 | [TODO] |
| 2.3 | Few-shot 可提升 5-15% 準確率 | [F] | E3 論文 | [TODO] |
| 2.4 | 細粒度分類（>50 類）需要微調或 RAG 輔助 | [H] | 工程經驗 | [標記] |
| 2.5 | 分類延遲通常 <1s（API 模式） | [F] | E2 測試 | [TODO] |

### 待搜尋的 Evidence

- [ ] LLM 分類 benchmark（GLUE, SuperGLUE 相關）
- [ ] Zero-shot / Few-shot 分類論文
- [ ] 官方 API 延遲文檔

---

## 3. 能力卡：RAG問答_RAG-QA

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 3.1 | RAG 是企業知識問答的主流解法 | [F] | E2 產業報告 | [TODO] |
| 3.2 | RAG 可降低幻覺率 30-50% | [F] | E3 論文 | [TODO] |
| 3.3 | 檢索品質是 RAG 效果的關鍵瓶頸 | [F] | E3 論文 | [TODO] |
| 3.4 | Chunk size 建議 256-1024 tokens | [H] | 工程經驗 | [標記] |
| 3.5 | Hybrid search（向量+關鍵字）優於純向量 | [F] | E3 論文 | [TODO] |
| 3.6 | Reranker 可提升 5-10% 準確率 | [F] | E3 論文 | [TODO] |
| 3.7 | RAG 需要評測框架（RAGAS 等） | [F] | E3 文檔 | [TODO] |

### 待搜尋的 Evidence

- [ ] RAG 原始論文（Lewis et al. 2020）
- [ ] RAG 評測論文（RAGAS, ARES...）
- [ ] Hybrid search 論文
- [ ] Lost-in-the-middle 論文

---

## 4. 能力卡：文件抽取_Information-Extraction

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 4.1 | 結構化資訊抽取（NER, RE）已相對成熟 | [F] | E3 評測 | [TODO] |
| 4.2 | 表格/表單抽取仍有挑戰（Layout 理解） | [F] | E3 論文 | [TODO] |
| 4.3 | LLM + JSON mode 可做 schema-based 抽取 | [F] | E3 官方文檔 | [TODO] |
| 4.4 | 抽取準確率高度依賴欄位明確性 | [H] | 工程經驗 | [標記] |
| 4.5 | 多模態模型（GPT-4V, Claude Vision）改善文件理解 | [F] | E3 官方文檔 | [TODO] |

### 待搜尋的 Evidence

- [ ] NER/IE benchmark 論文
- [ ] LayoutLM 論文
- [ ] OpenAI JSON mode 文檔
- [ ] Claude Vision 文檔

---

## 5. Playbook：RAG_企業知識問答

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 5.1 | RAG 架構包含：Indexing → Retrieval → Generation | [F] | E3 論文 | [TODO] |
| 5.2 | PoC 可用 managed service（OpenAI API + Pinecone） | [H] | 工程經驗 | [標記] |
| 5.3 | 評測需要 offline（測試集）+ online（監控） | [I] | 依據最佳實踐 | - |
| 5.4 | 常見失敗：檢索失敗 > 生成幻覺 > context 過長 | [H] | 工程經驗 | [標記] |
| 5.5 | 成本模型：API calls + embedding + storage | [F] | E3 官方定價 | [TODO] |

### 待搜尋的 Evidence

- [ ] RAG 架構論文
- [ ] RAG 評測框架（RAGAS）
- [ ] OpenAI/Anthropic 定價文檔

---

## 6. Playbook：客服工單自動化

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 6.1 | 客服分類是高 ROI quick win | [I] | 依據成熟度 | - |
| 6.2 | 回覆草稿需要 human-in-the-loop | [H] | 風險考量 | [標記] |
| 6.3 | 整合 CRM/工單系統是主要技術難點 | [H] | 工程經驗 | [標記] |
| 6.4 | 可用 LangChain/Dify 做 PoC | [F] | E3 官方文檔 | [TODO] |

### 待搜尋的 Evidence

- [ ] 客服 AI 案例研究
- [ ] LangChain/Dify 文檔

---

## 7. Playbook：文件抽取_OCR+Extraction

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 7.1 | 現代 OCR（Tesseract, Cloud Vision）準確率 >95% | [F] | E3 評測 | [TODO] |
| 7.2 | Layout 理解需要專門模型（LayoutLM, Donut） | [F] | E3 論文 | [TODO] |
| 7.3 | LLM 可做 post-OCR 校正和結構化 | [I] | 依據能力 | - |
| 7.4 | 需要 validation pipeline 確保抽取品質 | [H] | 工程經驗 | [標記] |

### 待搜尋的 Evidence

- [ ] OCR benchmark
- [ ] LayoutLM / Donut 論文
- [ ] Document AI 官方文檔

---

## 8. 瓶頸卡：幻覺與可追溯性

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 8.1 | LLM 幻覺是固有特性，無法完全消除 | [F] | E3 論文 | [TODO] |
| 8.2 | 不同任務幻覺率差異大（摘要 vs 創意寫作） | [F] | E3 論文 | [TODO] |
| 8.3 | Grounding（RAG/引用）是主要緩解策略 | [F] | E3 論文 | [TODO] |
| 8.4 | Self-consistency / CoT 可提升可靠性 | [F] | E3 論文 | [TODO] |
| 8.5 | 需要持續監控和人工抽查 | [H] | 工程經驗 | [標記] |

### 待搜尋的 Evidence

- [ ] 幻覺定義與分類論文
- [ ] TruthfulQA benchmark
- [ ] Self-consistency 論文（Wang et al.）
- [ ] RAG 降低幻覺的評測

---

## 9. 瓶頸卡：資料治理與權限

### 核心主張

| # | 主張 | 類型 | 需要證據 | 狀態 |
|---|------|------|---------|------|
| 9.1 | 資料送外部 API 有隱私風險 | [F] | E3 政策/法規 | [TODO] |
| 9.2 | 需要資料分級（公開/內部/機密/個資） | [H] | 最佳實踐 | [標記] |
| 9.3 | 可用私有部署（Azure OpenAI, Bedrock）緩解 | [F] | E3 官方文檔 | [TODO] |
| 9.4 | RAG 需要 document-level 權限控管 | [H] | 工程經驗 | [標記] |
| 9.5 | GDPR/個資法對 AI 處理有要求 | [F] | E3 法規 | [TODO] |

### 待搜尋的 Evidence

- [ ] OpenAI/Anthropic 資料政策
- [ ] Azure OpenAI 合規文檔
- [ ] GDPR AI 相關條款

---

## 10. Domain Pack：SME 客服與工單

### 核心主張

此 Domain Pack 的主張主要來自上述能力卡和 Playbook，需要交叉引用。

| # | 主張 | 來源 | 狀態 |
|---|------|------|------|
| 10.1 | 分類是 Quick Win | 來自 2.x | [連結] |
| 10.2 | RAG 問答需要資料準備 | 來自 3.x | [連結] |
| 10.3 | 回覆草稿需要 human-in-the-loop | 來自 6.x | [連結] |
| 10.4 | 幻覺是主要風險 | 來自 8.x | [連結] |
| 10.5 | 資料權限需要處理 | 來自 9.x | [連結] |

---

## Evidence 收集優先級

根據上述 Claim List，需要優先搜尋的 Evidence：

### 高優先（支撐多個主張）

1. [ ] RAG 論文（Lewis et al. 2020）- 支撐 3.1, 5.1
2. [ ] Lost-in-the-middle 論文 - 支撐 1.3, 3.3
3. [ ] LLM 幻覺論文 - 支撐 8.1, 8.2
4. [ ] Self-consistency 論文 - 支撐 8.4
5. [ ] OpenAI API 官方文檔 - 支撐多個工具和成本相關
6. [ ] Anthropic Claude 官方文檔 - 同上
7. [ ] RAGAS 評測框架 - 支撐 3.7, 5.3

### 中優先

8. [ ] LayoutLM 論文 - 支撐 4.2, 7.2
9. [ ] Zero-shot 分類論文 - 支撐 2.2, 2.3
10. [ ] Azure OpenAI 合規文檔 - 支撐 9.3

---

## 下一步

1. 使用 WebSearch 驗證上述來源
2. 建立 Evidence Notes
3. 回填到各卡片
4. 標記無法驗證的為 [TODO: evidence]

**最後更新**：2025-01-XX
