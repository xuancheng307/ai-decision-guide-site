---
type: bottleneck
title: "幻覺與可追溯性（Hallucination & Grounding）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [hallucination, grounding, faithfulness, citation]
status: stable
evidence_level: E3
---

# 幻覺與可追溯性（Hallucination & Grounding）

> **一句話**：LLM 會生成看似合理但事實錯誤的內容，且難以追溯來源。

---

## 風險分類

### 幻覺類型

[F] 幻覺分為兩大類：Factuality Hallucination（事實錯誤）和 Faithfulness Hallucination（不忠於輸入/context）[^Hallucination_Huang2023]。

| 類型 | 定義 | 範例 |
|------|------|------|
| **Factuality Hallucination** | 與世界知識矛盾 | 「台北是日本首都」 |
| **Faithfulness Hallucination** | 與輸入 context 矛盾 | Context 說「合約金額 100 萬」，回答「50 萬」 |
| **Instruction Inconsistency** | 不遵守指令 | 要求 JSON 輸出，給出純文字 |

### 風險等級

| 領域 | 風險等級 | 原因 |
|------|---------|------|
| 醫療/健康 | **高** | 錯誤資訊可能危害生命 |
| 法律/合規 | **高** | 錯誤建議可能導致法律風險 |
| 金融 | **高** | 錯誤數字可能造成財務損失 |
| 客服 | **中** | 錯誤資訊影響客戶體驗 |
| 內容創作 | **低** | 有人工覆核 |

---

## 症狀識別

### 常見症狀

| 症狀 | 描述 | 檢測方式 |
|------|------|---------|
| **憑空捏造** | 生成不存在的事實 | 事實查核 |
| **數字錯誤** | 金額、日期、比例錯誤 | 數值驗證 |
| **引用杜撰** | 引用不存在的來源 | 引用驗證 |
| **張冠李戴** | 混淆不同實體的資訊 | 實體對齊檢查 |
| **過度自信** | 對錯誤答案高度確定 | 不確定性檢測 |

[F] 在 SummExecEdit 上表現最佳的 Claude 3.5 Sonnet 準確率僅約 73%，顯示 LLM 在檢測事實錯誤上仍有困難[^SUM_SummExecEdit2024]。

---

## 根因分析

### 訓練資料問題

- 訓練資料包含錯誤資訊
- 過時資訊（知識截止日期）
- 訓練資料偏差

### 模型架構問題

- 參數記憶 vs 檢索的權衡
- 長 context 處理能力有限
- 解碼策略影響（temperature 等）

[F] LLM 在處理長 context 時，對「中間」的資訊表現最差（U-shaped curve）[^LostInMiddle_Liu2023]。

### 任務特性

- 開放式問題更容易幻覺
- 需要推理的任務更容易出錯
- 領域專業度影響

---

## 緩解策略

### 策略 1：RAG（檢索增強）

[F] RAG 結合 pre-trained parametric memory 與 non-parametric memory，用於 knowledge-intensive 任務[^RAG_Lewis2020]。

| 優點 | 限制 |
|------|------|
| 可更新知識 | 檢索失敗時仍可能幻覺 |
| 可追溯來源 | 增加延遲和成本 |
| 減少參數記憶依賴 | 需要建立知識庫 |

[F] 即使使用 RAG，系統仍可能產生幻覺，RAG 無法完全消除問題[^Hallucination_Huang2023]。

### 策略 2：引用機制

強制要求輸出引用來源：

```
回答時請：
1. 只根據提供的資料回答
2. 用 [來源: 文件名] 格式標註引用
3. 如果資料不足，明確說明
```

### 策略 3：Self-Consistency

[F] Self-consistency 透過 sampling 多條 reasoning paths，選擇最一致的答案，在多個 benchmark 上顯著提升效能[^SelfConsistency_Wang2022]。

| 方法 | 成本增加 | 效果 |
|------|---------|------|
| 3 次採樣 + 投票 | 3x | 顯著提升 |
| 5 次採樣 + 投票 | 5x | 邊際遞減 |

### 策略 4：不確定性表達

訓練/提示模型表達不確定性：

```
如果你不確定，請回答：
「根據我的理解...，但建議進一步確認」
```

### 策略 5：後處理驗證

| 驗證類型 | 方法 | 適用場景 |
|----------|------|---------|
| **格式驗證** | 正則表達式、Schema | 結構化輸出 |
| **數值驗證** | 範圍檢查、一致性檢查 | 數字敏感 |
| **事實驗證** | LLM-as-judge、外部 API | 關鍵事實 |

---

## 監控指標

### Offline 評測

| 指標 | 來源 | 目標 |
|------|------|------|
| **Faithfulness** | RAGAS | > 80% |
| **Hallucination Rate** | 人工標註 | < 10% |
| **Citation Accuracy** | 引用驗證 | > 95% |

[F] RAGAS 提供不需要人工標註 ground truth 的 RAG 評測方法[^RAGAS_Es2023]。

### Online 監控

| 指標 | 測量方式 | 告警閾值 |
|------|---------|---------|
| **「不確定」回答比例** | 關鍵詞計數 | 突增 > 20% |
| **用戶回報錯誤率** | 回饋機制 | > 5% |
| **引用缺失率** | 輸出分析 | > 10% |

---

## 驗收 Gate

| 階段 | 指標要求 |
|------|---------|
| **PoC → Pilot** | Faithfulness > 70%，有引用機制 |
| **Pilot → Prod** | Faithfulness > 80%，有監控告警 |
| **Prod 維護** | Faithfulness 下降 < 5% |

---

## 反模式（Anti-patterns）

| 反模式 | 描述 | 修正 |
|--------|------|------|
| **盲目信任 LLM** | 不驗證直接使用 | 建立驗證流程 |
| **忽略 RAG 失敗** | 檢索失敗時仍生成 | 設定回退機制 |
| **無引用要求** | 不要求標註來源 | 強制引用 |
| **過長 Context** | 塞入過多資料 | 控制 context，用 reranker |
| **單次採樣** | 只取一次結果 | 關鍵場景用 self-consistency |

---

## 相關連結

- **能力卡**：[[RAG問答_RAG-QA]], [[文件摘要_Summarization]]
- **Playbook**：[[RAG_企業知識問答_Playbook]]
- **工具卡**：[[Evaluation_評測與可觀測性]]

---

## 參考來源

[^Hallucination_Huang2023]: A Survey on Hallucination in Large Language Models. ACM TOIS 2024. 參見 [[Hallucination_Survey_2023]]

[^RAG_Lewis2020]: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. NeurIPS 2020. 參見 [[RAG_Lewis_2020]]

[^RAGAS_Es2023]: RAGAS: Automated Evaluation of Retrieval Augmented Generation. EACL 2024. 參見 [[RAGAS_2023]]

[^SelfConsistency_Wang2022]: Self-Consistency Improves Chain of Thought Reasoning. ICLR 2023. 參見 [[SelfConsistency_Wang_2022]]

[^LostInMiddle_Liu2023]: Lost in the Middle: How Language Models Use Long Contexts. TACL 2024. 參見 [[LostInTheMiddle_Liu_2023]]

[^TruthfulQA_Lin2022]: TruthfulQA: Measuring How Models Mimic Human Falsehoods. ACL 2022. 參見 [[TruthfulQA_Lin_2022]]

[^SUM_SummExecEdit2024]: SummExecEdit: A Factual Consistency Benchmark. arXiv:2412.13378. 參見 [[SUM_SummExecEdit_2024]]
