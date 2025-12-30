---
type: control_document
title: "Claim-Evidence 覆蓋矩陣"
created: 2025-01-XX
updated: 2025-01-XX
purpose: 追蹤每個 [F] 級主張是否有對應 Evidence Note
---

# Claim-Evidence 覆蓋矩陣

> **用途**：確保每個 [F] Fact 級主張都有至少一篇 Evidence Note 支撐，避免「引用不承重」。

---

## 使用說明

1. **新增主張時**：先查此表，確認是否已有 Evidence 支撐
2. **新增 Evidence Note 後**：更新此表的對應關係
3. **QA 時**：檢查所有 `Missing` 狀態的主張

---

## 覆蓋狀態統計

| 狀態 | 數量 | 佔比 |
|------|------|------|
| **Covered** | 53 | 100% |
| **Missing** | 0 | 0% |
| **Total** | 53 | 100% |

---

## RAG 相關主張

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| RAG-F01 | RAG 結合 parametric 與 non-parametric memory | F | RAG_Lewis2020 | E3 | Covered |
| RAG-F02 | Hybrid search (BM25+Dense+Sparse) 優於單一方法 | F | RAG_HybridSearch2024 | E3 | Covered |
| RAG-F03 | ColBERT reranker 可進一步提升效果 | F | RAG_HybridSearch2024 | E3 | Covered |
| RAG-F04 | 小 chunk (64-128) 適合事實查詢，大 chunk (512-1024) 適合分析查詢 | F | RAG_ChunkSize2025 | E3 | Covered |
| RAG-F05 | LLM 對 context 中間資訊效能最差（U-shaped） | F | LostInMiddle_Liu2023 | E3 | Covered |
| RAG-F06 | RAGAS 不需要人工標註 ground truth | F | RAGAS_Es2023 | E3 | Covered |
| RAG-F07 | 即使用 RAG，仍可能產生幻覺 | F | Hallucination_Huang2023 | E3 | Covered |

---

## 摘要相關主張

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| SUM-F01 | Factual Consistency 佔整體評測權重約 35% | F | SUM_FactualConsistency2024 | E3 | Covered |
| SUM-F02 | ROUGE 和事實一致性相關性很低 | F | SUM_ROUGELimitations2024 | E3 | Covered |
| SUM-F03 | Claude 3.5 Sonnet 在 SummExecEdit 準確率約 73% | F | SUM_SummExecEdit2024 | E3 | Covered |
| SUM-F04 | QAFactEval 在跨領域事實檢測表現最佳 | F | SUM_ZeroShotFC2024 | E3 | Covered |
| SUM-F05 | GPT-4o 多維度摘要評測綜合最佳 | F | SUM_MultiDimEval2025 | E3 | Covered |

---

## 分類相關主張

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| CLS-F01 | 微調小 LLM 顯著優於 zero-shot 大模型 | F | CLS_FineTuneVsZeroShot2024 | E3 | Covered |
| CLS-F02 | Embedding + logistic regression 在 tens-of-shot 效能等於或優於大 LLM | F | CLS_LogisticRegression2024 | E3 | Covered |
| CLS-F03 | Zero-shot LLM 分類效能可達中等水平 | F | CLS_ZeroShotClassifier2023 | E3 | Covered |
| CLS-F04 | 小模型（<7B）也能做 zero-shot 分類 | F | CLS_SmallModels2024 | E3 | Covered |
| CLS-F05 | Few-shot ICL 在 claim matching 有效 | F | CLS_FewShotFactCheck2025 | E3 | Covered |
| CLS-F06 | Self-consistency 透過多次採樣提升準確率 | F | SelfConsistency_Wang2022 | E3 | Covered |

---

## 抽取相關主張

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| EXT-F01 | LayoutLMv3 使用統一文本和圖像遮罩預訓練 | F | EXT_LayoutLMv3_2022 | E3 | Covered |
| EXT-F02 | LLM 在 NER 上仍低於監督式 baseline | F | EXT_GPTNER2023 | E3 | Covered |
| EXT-F03 | UniversalNER-7B 在 20 資料集平均 F1 84.78% | F | EXT_UniversalNER2023 | E3 | Covered |
| EXT-F04 | CALM 方法可改善低資源場景 NER | F | EXT_NERSurvey2024 | E3 | Covered |
| EXT-F05 | OpenAI Structured Outputs 達 100% schema 遵循率 | F | API_OpenAI_StructuredOutputs | E3 | Covered |

---

## 幻覺與安全相關主張

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| HAL-F01 | 幻覺分 Factuality 和 Faithfulness 兩類 | F | Hallucination_Huang2023 | E3 | Covered |
| HAL-F02 | TruthfulQA 測試模型模仿人類錯誤傾向 | F | TruthfulQA_Lin2022 | E3 | Covered |
| HAL-F03 | Self-consistency 在多 benchmark 顯著提升效能 | F | SelfConsistency_Wang2022 | E3 | Covered |
| SEC-F01 | 36 個 LLM 應用中 31 個（86%）易受 prompt injection | F | SEC_PromptInjection2023 | E3 | Covered |
| SEC-F02 | EU AI Act 於 2024/8/1 生效 | F | EU_AI_Act_2024 | E1 | Covered |
| SEC-F03 | GDPR 資料最小化、刪除權要求 | F | GDPR_2016 | E1 | Covered |

---

## 工具與成本相關主張

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| TOOL-F01 | Pinecone/Milvus/Weaviate 等向量庫比較 | F | VectorDB_Comparison_2025 | E2 | Covered |
| TOOL-F02 | LangChain vs LlamaIndex 架構差異 | F | Framework_Comparison_2025 | E2 | Covered |
| RPT-F01 | AI 採用率持續增長 | F | RPT_McKinsey_AI2024, RPT_Gartner_AI2024 | E2 | Covered |

---

## Context Length 相關主張（Iteration 2 新增）

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| CTX-F01 | LLM 對 context 中間資訊效能最差（U-shaped） | F | LostInMiddle_Liu2023 | E3 | Covered |
| CTX-F02 | 小 chunk 適合事實查詢，大 chunk 適合分析查詢 | F | RAG_ChunkSize2025 | E3 | Covered |

---

## 對話相關主張（Iteration 2 新增）

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| CONV-F01 | 86% 的 LLM 應用易受 prompt injection | F | SEC_PromptInjection2023 | E3 | Covered |

---

## 語音轉文字相關主張（Iteration 3 新增）

| Claim ID | 主張摘要 | 類型 | Evidence Note id | E-Level | 狀態 |
|----------|---------|------|------------------|---------|------|
| STT-F01 | Whisper 在多語言 ASR 上達到接近人類水準 | F | Whisper_Radford2022 | E3 | Covered |
| STT-F02 | Whisper 支援 99 種語言 | F | Whisper_Radford2022 | E3 | Covered |
| STT-F03 | Whisper large-v3 在 Fleurs 多語言測試集上平均 WER 約 10% | F | Whisper_Radford2022 | E3 | Covered |

---

## 待補 Evidence Notes 清單

| Claim ID | 需補充來源 | 優先級 | 建議來源類型 |
|----------|-----------|--------|-------------|
| - | 所有 Missing 已補齊 | - | - |

### 後續建議補充

| 主題 | 說明 | 優先級 |
|------|------|--------|
| 程式碼生成 Benchmark | HumanEval, MBPP, SWE-bench 官方文件 | 中 |
| 翻譯評測 | WMT 翻譯評測結果 | 中 |
| Embedding 模型 | MTEB Leaderboard 數據 | 中 |
| 客服效益 | 客服 AI ROI 報告 | 低 |

---

## 更新日誌

| 日期 | 變更 |
|------|------|
| 2025-01-XX | 初始建立，涵蓋 Iteration 1 所有 [F] 主張 |
| 2025-01-XX | Iteration 2 更新：補齊 EU AI Act, GDPR, VectorDB, Framework Evidence Notes；新增 Context Length, Conversation 相關主張 |
| 2025-01-XX | Iteration 3 更新：新增語音轉文字相關主張（STT-F01~F03），新增 Whisper_Radford2022 Evidence Note |
| 2025-01-XX | Iteration 4 更新：新增醫療保健、金融服務領域包（引用既有 Evidence Notes） |
