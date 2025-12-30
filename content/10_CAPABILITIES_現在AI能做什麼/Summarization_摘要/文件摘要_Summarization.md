---
type: capability
title: "文件摘要（Text Summarization）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [summarization, LLM, document, generation]
status: stable
evidence_level: E3
---

# 文件摘要（Text Summarization）

> **一句話**：讓 AI 閱讀長文件並產出精簡摘要，保留關鍵資訊。

---

## 基本資訊

| 項目 | 內容 |
|------|------|
| **輸入** | 長文件（文章、報告、會議紀錄、郵件串） |
| **輸出** | 精簡摘要（可控制長度） |
| **成熟度** | **Pilot-ready**（需要 Factual Consistency 監控才能 Production） |
| **最後更新** | 2025-01-XX |

---

## 1. 能力定義（Definition）

**摘要類型**：

| 類型 | 說明 | 適用場景 |
|------|------|---------|
| **Extractive** | 從原文選取重要句子 | 需要精確引用 |
| **Abstractive** | 重新生成摘要文字 | 需要流暢閱讀 |
| **Hybrid** | 結合兩者 | 平衡精確與流暢 |

[F] 現代 LLM 可以生成高度可讀的 abstractive 摘要，傳統指標如 ROUGE 已經飽和[^SUM_ROUGELimitations2024]。

---

## 2. 能做到的範圍（What it can do now）

### 2.1 表現良好的場景

- [x] 會議紀錄摘要
- [x] 新聞/文章摘要
- [x] 長郵件串摘要
- [x] 報告重點提取
- [x] 多文件綜合摘要

### 2.2 表現程度

#### Metrics（評測指標）

| 指標 | 定義 | 適用場景 |
|------|------|---------|
| **Factual Consistency** | 摘要與原文事實一致性 | 所有摘要任務（權重 35%）[^SUM_MultiDimEval2025] |
| **Relevance** | 摘要與原文相關性 | 所有摘要任務（權重 25%） |
| **Coherence** | 摘要邏輯連貫性 | 所有摘要任務（權重 20%） |
| **Fluency** | 語言流暢度 | 所有摘要任務（權重 20%） |
| **ROUGE** | N-gram 重疊度 | 參考用，已飽和 |

#### Public Benchmarks（公開基準）

| Benchmark | 最佳模型表現 | 來源 |
|-----------|------------|------|
| SummExecEdit FC 檢測 | Claude 3.5 Sonnet ~73% | [^SUM_SummExecEdit2024] |

[F] 在 SummExecEdit 上表現最佳的 Claude 3.5 Sonnet 準確率僅約 73%，顯示 FC 檢測仍具挑戰性[^SUM_SummExecEdit2024]。

#### Domain Baseline Plan（本域基準計畫）

建議使用者：
1. 準備 50-100 篇代表性文件
2. 人工撰寫參考摘要（或評估 AI 摘要的 FC）
3. 使用 LLM-as-judge 評估 Factual Consistency
4. 記錄 baseline 到 E4 Evidence Note

---

## 3. 適合的任務特徵（Good fit）

- [x] **文件有明確主題**：會議、報告、新聞
- [x] **可接受 70-80% 準確**：有人工覆核
- [x] **需要快速理解**：大量文件需要篩選
- [x] **長度可控**：可以指定摘要長度

---

## 4. 不適合/高風險（Bad fit / Red flags）

### 4.1 不適合的場景

- [ ] **法律/醫療文件**：事實錯誤代價高[^SUM_FactualConsistency2024]
- [ ] **需要 100% 準確**：AI 摘要無法保證
- [ ] **高度技術文件**：可能遺漏關鍵細節
- [ ] **需要精確數字**：容易出錯

### 4.2 紅旗警訊

[F] 即使是先進的 LLM，許多仍在檢測事實錯誤上有困難[^SUM_SummExecEdit2024]。

- [x] **長文件中間段落**：可能遺漏（Lost in the Middle 效應）[^LostInMiddle_Liu2023]
- [x] **數字和日期**：容易產生幻覺
- [x] **專有名詞**：可能誤解或混淆

---

## 5. 常用落地模式（Patterns）

| 模式 | 適用情境 | 備註 |
|------|---------|------|
| **單文件摘要** | 會議紀錄、報告 | 最基礎模式 |
| **多文件摘要** | 新聞聚合、研究綜述 | 需要去重和整合 |
| **漸進式摘要** | 超長文件（>100K tokens） | 分段摘要再整合 |
| **結構化摘要** | 需要特定格式 | 使用 Structured Output |

---

## 6. 常用工具（Tools）

| 層級 | 工具 | 備註 |
|------|------|------|
| **模型層** | GPT-4o, Claude 3.5, Gemini | 長 context 支援重要 |
| **框架層** | LangChain, LlamaIndex | 支援 map-reduce 摘要 |
| **評測層** | DeepEval, TruLens | Factual Consistency 評估 |

---

## 7. 瓶頸與對策（Bottlenecks & Mitigations）

| 瓶頸 | 症狀 | 緩解策略 | 連結 |
|------|------|---------|------|
| **事實不一致** | 摘要與原文矛盾 | FC 監控、人工覆核 | [[幻覺與可追溯性_Hallucination-Grounding]] |
| **Lost in Middle** | 漏掉中間段落 | 分段摘要、重新排序 | [^LostInMiddle_Liu2023] |
| **長度失控** | 摘要太長或太短 | 明確指定字數、few-shot |  |
| **專業術語誤解** | 錯誤解讀術語 | 提供術語表、領域 prompt |  |

---

## 8. 成熟度分級（Maturity）

| 階段 | 定義 | 這個能力的狀態 |
|------|------|-----------------|
| **PoC** | 實驗室環境可行 | ✅ 容易達成 |
| **Pilot** | 小規模真實環境可行 | ✅ 需要 FC 監控 |
| **Production** | 大規模穩定運行 | ⚠️ 需要完整評測和人工覆核流程 |

**Production 需要**：
- Factual Consistency 監控（抽樣評測）
- 人工覆核機制（至少抽樣）
- 使用者回饋收集
- 錯誤案例分析

---

## 9. 發展預期（Outlook & Watch signals）

### 9.1 觀測訊號

- [ ] **Long-context 改進**：是否解決 Lost in Middle
- [ ] **FC 評測標準化**：是否有更可靠的自動評測
- [ ] **多模態摘要**：圖表+文字整合摘要

### 9.2 預期趨勢

| 時間範圍 | 預期變化 | 依據 |
|----------|---------|------|
| 6 個月內 | FC 評測工具更成熟 | [I] 研究趨勢 |
| 1 年內 | 長文件處理更可靠 | [I] 模型進化 |

---

## 相關連結

- **Playbooks**：[[RAG_企業知識問答_Playbook]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]]
- **工具卡**：[[Evaluation_評測與可觀測性]]

---

## 參考來源

[^SUM_ROUGELimitations2024]: Do Automatic Factuality Metrics Measure Factuality? A Critical Evaluation. arXiv:2411.16638. 參見 [[SUM_ROUGELimitations_2024]]

[^SUM_MultiDimEval2025]: An Empirical Comparison of Text Summarization: Multi-Dimensional Evaluation of LLMs. arXiv:2504.04534. 參見 [[SUM_MultiDimEval_2025]]

[^SUM_SummExecEdit2024]: SummExecEdit: A Factual Consistency Benchmark in Summarization. arXiv:2412.13378. 參見 [[SUM_SummExecEdit_2024]]

[^SUM_FactualConsistency2024]: Factual Consistency Evaluation of Summarization in the Era of LLMs. arXiv:2402.13758. 參見 [[SUM_FactualConsistency_2024]]

[^LostInMiddle_Liu2023]: Lost in the Middle: How Language Models Use Long Contexts. TACL 2024. 參見 [[LostInTheMiddle_Liu_2023]]

[^SUM_ZeroShotFC2024]: Zero-shot Factual Consistency Evaluation Across Domains. arXiv:2408.04114. 參見 [[SUM_ZeroShotFC_2024]]
