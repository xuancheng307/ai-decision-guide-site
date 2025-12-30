---
type: capability
title: "分類與路由（Classification & Routing）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [classification, routing, LLM, zero-shot, few-shot]
status: stable
evidence_level: E3
---

# 分類與路由（Classification & Routing）

> **一句話**：讓 AI 判斷文本屬於哪個類別，並據此決定下一步處理流程。

---

## 基本資訊

| 項目 | 內容 |
|------|------|
| **輸入** | 文本（問題、工單、郵件、文件） |
| **輸出** | 類別標籤 + 可選的信心度 |
| **成熟度** | **Production-ready**（適當設定下可直接上線） |
| **最後更新** | 2025-01-XX |

---

## 1. 能力定義（Definition）

**分類方法**：

| 方法 | 說明 | 適用場景 |
|------|------|---------|
| **Zero-shot** | 無需訓練資料，直接 prompt | 快速原型、類別常變動 |
| **Few-shot** | 提供少量範例（3-10 個） | 中等精度需求 |
| **Fine-tuned** | 微調專用模型 | 高精度生產環境 |
| **Embedding + Classifier** | LLM embedding + 傳統分類器 | 高效、可解釋 |

[F] 較小的微調 LLM 在文本分類任務上持續且顯著優於較大的 zero-shot prompted 模型[^CLS_FineTuneVsZeroShot2024]。

[F] LLM 可以使用 zero-shot learning 搭配 CoT prompting 進行分類，直接預測已見和未見類別[^CLS_ZeroShotClassifier2023]。

---

## 2. 能做到的範圍（What it can do now）

### 2.1 表現良好的場景

- [x] 客服工單分類（問題類型、優先級）
- [x] 郵件分類（垃圾郵件、類別）
- [x] 情感分析（正面/負面/中性）
- [x] 意圖識別（查詢意圖路由）
- [x] 文件分類（合約類型、報告類型）

### 2.2 表現程度

#### Metrics（評測指標）

| 指標 | 定義 | 適用場景 |
|------|------|---------|
| **Accuracy** | 正確分類比例 | 類別平衡時 |
| **F1-score** | Precision/Recall 調和平均 | 類別不平衡時 |
| **Macro-F1** | 各類別 F1 平均 | 關注少數類別時 |

#### Public Benchmarks（公開基準）

| 方法 | 典型表現 | 條件 | 來源 |
|------|---------|------|------|
| Zero-shot LLM | 在 3/4 資料集有效 | GPT-4 等級 | [^CLS_ZeroShotClassifier2023] |
| Fine-tuned 小模型 | 顯著優於 zero-shot | 有訓練資料 | [^CLS_FineTuneVsZeroShot2024] |
| 小模型 zero-shot | 與大模型相當 | 77M-40B | [^CLS_SmallModels2024] |
| Embedding + LogReg | 等於或優於大 LLM | tens-of-shot | [^CLS_LogisticRegression2024] |

[F] 小型語言模型在 zero-shot 分類上的表現與大型模型相當[^CLS_SmallModels2024]。

#### Domain Baseline Plan（本域基準計畫）

建議使用者：
1. 收集 100+ 標註樣本（每類別至少 20 個）
2. 選擇方法（zero-shot / few-shot / fine-tune）
3. 計算 Accuracy 和 Macro-F1 作為 baseline
4. 記錄到 E4 Evidence Note

---

## 3. 適合的任務特徵（Good fit）

- [x] **類別定義明確**：類別之間邊界清晰
- [x] **類別數量適中**：2-20 個類別最佳
- [x] **可接受 85-95% 準確**：非生死攸關決策
- [x] **類別相對穩定**：不需要頻繁新增類別（或接受 zero-shot）

---

## 4. 不適合/高風險（Bad fit / Red flags）

### 4.1 不適合的場景

- [ ] **類別定義模糊**：人類也難以區分
- [ ] **類別極度不平衡**：某類別樣本 < 1%
- [ ] **需要 99%+ 準確**：安全關鍵應用
- [ ] **類別數量極多**：> 100 個類別需要特殊處理

### 4.2 紅旗警訊

- [x] **邊界案例多**：難以歸類的樣本比例高
- [x] **類別重疊**：一個樣本可能屬於多類別
- [x] **專業領域**：LLM 缺乏領域知識

---

## 5. 常用落地模式（Patterns）

| 模式 | 適用情境 | 成本 | 精度 |
|------|---------|------|------|
| **Zero-shot Prompting** | 快速原型、類別常變 | 低 | 中 |
| **Few-shot Prompting** | 有少量範例 | 低-中 | 中-高 |
| **Embedding + Classifier** | 需要高效和可解釋 | 中 | 高 |
| **Fine-tuned 小模型** | 生產環境、大量資料 | 高（一次性） | 最高 |
| **Self-consistency** | 需要更高可靠性 | 高（多次呼叫） | 高 |

[F] 在 "tens-of-shot" 情境下，小型 LLM embedding + logistic regression 的效能等於或優於大型 LLM[^CLS_LogisticRegression2024]。

---

## 6. 常用工具（Tools）

| 層級 | 工具 | 備註 |
|------|------|------|
| **模型層** | GPT-4o, Claude 3.5 | Zero/few-shot |
| **模型層** | BERT, RoBERTa, DistilBERT | Fine-tuning |
| **框架層** | LangChain, Scikit-learn | 分類 pipeline |
| **Embedding** | OpenAI, Sentence-Transformers | Embedding + Classifier |

---

## 7. 瓶頸與對策（Bottlenecks & Mitigations）

| 瓶頸 | 症狀 | 緩解策略 | 連結 |
|------|------|---------|------|
| **類別不平衡** | 少數類別 recall 低 | 重新採樣、調整 threshold | |
| **邊界案例** | 信心度分散 | 設定「不確定」類別、人工覆核 | |
| **Prompt 敏感** | 微小改動影響大 | Few-shot、prompt 測試 | |
| **成本** | API 費用高 | 使用小模型或 embedding 方案 | |

---

## 8. 成熟度分級（Maturity）

| 階段 | 定義 | 這個能力的狀態 |
|------|------|-----------------|
| **PoC** | 實驗室環境可行 | ✅ 極易達成 |
| **Pilot** | 小規模真實環境可行 | ✅ 需要評測 baseline |
| **Production** | 大規模穩定運行 | ✅ 適當設定即可 |

**Production 需要**：
- 明確的類別定義文件
- 評測集和 baseline 指標
- 監控分類分佈變化
- 邊界案例處理機制

---

## 9. 發展預期（Outlook & Watch signals）

### 9.1 觀測訊號

- [ ] **小模型持續進步**：是否可以用更小模型達到相同效果
- [ ] **多標籤分類**：是否有更好的多標籤處理方法

### 9.2 預期趨勢

| 時間範圍 | 預期變化 | 依據 |
|----------|---------|------|
| 6 個月內 | 小模型 zero-shot 更強 | [I] 模型進化趨勢 |
| 1 年內 | 分類成為基礎能力 | [I] 應用普及 |

---

## 相關連結

- **Playbooks**：[[客服工單自動化_Playbook]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]]
- **領域包**：[[SME_中小企業通用_客服與工單]]

---

## 參考來源

[^CLS_FineTuneVsZeroShot2024]: Fine-Tuned 'Small' LLMs Still Significantly Outperform Zero-Shot Generative AI in Text Classification. arXiv:2406.08660. 參見 [[CLS_FineTuneVsZeroShot_2024]]

[^CLS_ZeroShotClassifier2023]: Large Language Models Are Zero-Shot Text Classifiers. arXiv:2312.01044. 參見 [[CLS_ZeroShotClassifier_2023]]

[^CLS_SmallModels2024]: Small Language Models are Good Too: An Empirical Study of Zero-Shot Classification. arXiv:2404.11122. 參見 [[CLS_SmallModels_2024]]

[^CLS_LogisticRegression2024]: Logistic Regression Makes Small LLMs Strong "Tens-of-Shot" Classifiers. arXiv:2408.03414. 參見 [[CLS_LogisticRegression_2024]]

[^CLS_FewShotFactCheck2025]: Zero-shot and Few-shot Learning with Instruction-following LLMs for Claim Matching. arXiv:2501.10860. 參見 [[CLS_FewShotFactCheck_2025]]

[^SelfConsistency_Wang2022]: Self-Consistency Improves Chain of Thought Reasoning. ICLR 2023. 參見 [[SelfConsistency_Wang_2022]]
