---
type: capability
title: "文件抽取（Information Extraction）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [extraction, NER, structured-output, document-AI]
status: stable
evidence_level: E3
---

# 文件抽取（Information Extraction）

> **一句話**：讓 AI 從文件中抽取結構化資訊（如姓名、日期、金額、實體關係）。

---

## 基本資訊

| 項目 | 內容 |
|------|------|
| **輸入** | 非結構化文件（PDF、圖片、文字） |
| **輸出** | 結構化資料（JSON、表格、資料庫記錄） |
| **成熟度** | **Pilot-ready**（需要 Schema 設計和驗證流程才能 Production） |
| **最後更新** | 2025-01-XX |

---

## 1. 能力定義（Definition）

**抽取任務類型**：

| 類型 | 說明 | 範例 |
|------|------|------|
| **NER** | 命名實體識別 | 人名、地名、組織名 |
| **Relation Extraction** | 實體間關係抽取 | 「張三」是「ABC公司」的「CEO」 |
| **Form/Table Extraction** | 表單/表格資料抽取 | 發票欄位、報表數據 |
| **Key-Value Extraction** | 關鍵字段抽取 | 合約金額、生效日期 |

[F] 儘管 LLM 在多種 NLP 任務上達到 SOTA，其在 NER 上的表現仍顯著低於監督式 baseline[^EXT_GPTNER2023]。

[F] LayoutLMv3 使用統一的文本和圖像遮罩進行 Document AI 預訓練，廣泛用於文件理解任務[^EXT_LayoutLMv3_2022]。

---

## 2. 能做到的範圍（What it can do now）

### 2.1 表現良好的場景

- [x] 發票/收據資訊抽取
- [x] 合約關鍵條款抽取
- [x] 履歷結構化
- [x] 名片資訊抽取
- [x] 表格數據抽取

### 2.2 表現程度

#### Metrics（評測指標）

| 指標 | 定義 | 適用場景 |
|------|------|---------|
| **F1-score** | 抽取準確率 | NER、關係抽取 |
| **Schema Compliance** | 輸出符合預定 schema | 結構化輸出 |
| **Field Accuracy** | 單欄位正確率 | 表單抽取 |

#### Public Benchmarks（公開基準）

| Benchmark | 最佳表現 | 方法 | 來源 |
|-----------|---------|------|------|
| UniversalNER (20 datasets) | F1 84.78% | UniversalNER-7B | [^EXT_UniversalNER2023] |
| OpenAI Structured Outputs | 100% schema compliance | GPT-4o | [^API_OpenAI_StructuredOutputs] |

[F] UniversalNER-7B 在 20 個資料集上達到平均 F1 84.78%，分別超越 BERT-base 和 InstructUIE-11B 4.69% 和 3.62%[^EXT_UniversalNER2023]。

[F] OpenAI Structured Outputs 在 gpt-4o-2024-08-06 上達到 100% schema 遵循率[^API_OpenAI_StructuredOutputs]。

#### Domain Baseline Plan（本域基準計畫）

建議使用者：
1. 定義目標 schema（JSON Schema / Pydantic）
2. 準備 50-100 份標註文件
3. 計算 Field-level Accuracy 作為 baseline
4. 記錄到 E4 Evidence Note

---

## 3. 適合的任務特徵（Good fit）

- [x] **Schema 可預定義**：知道要抽取什麼欄位
- [x] **欄位數量適中**：5-30 個欄位
- [x] **文件格式相對固定**：同類文件結構相似
- [x] **可接受 80-95% 準確**：有人工覆核

---

## 4. 不適合/高風險（Bad fit / Red flags）

### 4.1 不適合的場景

- [ ] **Schema 不明確**：不知道要抽取什麼
- [ ] **高度非結構化**：每份文件格式都不同
- [ ] **需要 99%+ 準確**：金融/法律關鍵數據
- [ ] **手寫文件**：OCR 品質不穩定

### 4.2 紅旗警訊

[F] LLM 在 NER 任務上與專門訓練的模型存在效能差距[^EXT_GPTNER2023]。

- [x] **數字敏感欄位**：金額、日期容易出錯
- [x] **專業術語**：領域特定詞彙可能誤解
- [x] **低品質掃描件**：OCR 錯誤會傳遞到抽取

---

## 5. 常用落地模式（Patterns）

| 模式 | 適用情境 | 工具 |
|------|---------|------|
| **LLM + Structured Output** | 簡單表單、快速原型 | GPT-4o, Claude |
| **LayoutLM + Fine-tune** | 大量同類文件 | LayoutLMv3 |
| **OCR + LLM** | 掃描件/圖片 | Tesseract/Cloud OCR + LLM |
| **Document AI Platform** | 企業級需求 | AWS Textract, Azure Form Recognizer |

---

## 6. 常用工具（Tools）

| 層級 | 工具 | 備註 |
|------|------|------|
| **OCR 層** | Tesseract, EasyOCR, Cloud OCR | 圖片→文字 |
| **模型層** | GPT-4o (Structured Output) | [^API_OpenAI_StructuredOutputs] |
| **模型層** | LayoutLMv3, Donut | Document AI |
| **平台層** | AWS Textract, Azure Form Recognizer | 企業方案 |
| **Schema 定義** | Pydantic (Python), Zod (TS) | 型別安全 |

---

## 7. 瓶頸與對策（Bottlenecks & Mitigations）

| 瓶頸 | 症狀 | 緩解策略 | 連結 |
|------|------|---------|------|
| **Schema 不匹配** | 輸出缺少欄位 | 使用 Structured Outputs + 驗證 | [^API_OpenAI_StructuredOutputs] |
| **數字抽取錯誤** | 金額/日期格式錯誤 | 後處理驗證、正則表達式 | |
| **OCR 錯誤** | 文字辨識錯誤 | 多 OCR 引擎比對、人工覆核 | |
| **領域詞彙** | 專業術語誤解 | 提供 glossary、few-shot | |

---

## 8. 成熟度分級（Maturity）

| 階段 | 定義 | 這個能力的狀態 |
|------|------|-----------------|
| **PoC** | 實驗室環境可行 | ✅ 容易達成 |
| **Pilot** | 小規模真實環境可行 | ✅ 需要 Schema 設計 |
| **Production** | 大規模穩定運行 | ⚠️ 需要驗證流程和人工覆核 |

**Production 需要**：
- 明確的 Schema 定義（JSON Schema）
- 欄位級別的驗證規則
- 人工覆核流程（至少抽樣）
- 錯誤處理和回退機制

---

## 9. 發展預期（Outlook & Watch signals）

### 9.1 觀測訊號

- [ ] **多模態模型改進**：視覺+文字整合抽取
- [ ] **領域 NER 模型**：特定領域預訓練模型

### 9.2 預期趨勢

| 時間範圍 | 預期變化 | 依據 |
|----------|---------|------|
| 6 個月內 | Structured Output 更普及 | [I] API 功能擴展 |
| 1 年內 | 端到端文件理解更成熟 | [I] Document AI 進化 |

---

## 相關連結

- **Playbooks**：[[文件抽取_OCR_Playbook]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]]
- **工具卡**：[[Evaluation_評測與可觀測性]]

---

## 參考來源

[^EXT_LayoutLMv3_2022]: LayoutLMv3: Pre-training for Document AI with Unified Text and Image Masking. arXiv:2204.08387. 參見 [[EXT_LayoutLMv3_2022]]

[^EXT_GPTNER2023]: GPT-NER: Named Entity Recognition via Large Language Models. arXiv:2304.10428. 參見 [[EXT_GPTNER_2023]]

[^EXT_NERSurvey2024]: Recent Advances in Named Entity Recognition: A Comprehensive Survey. arXiv:2401.10825. 參見 [[EXT_NERSurvey_2024]]

[^EXT_UniversalNER2023]: UniversalNER: Targeted Distillation from Large Language Models. 參見 [[EXT_UniversalNER_2023]]

[^EXT_FinancialNER2025]: Financial Named Entity Recognition: How Far Can LLM Go? arXiv:2501.02237. 參見 [[EXT_FinancialNER_2025]]

[^API_OpenAI_StructuredOutputs]: OpenAI Structured Outputs Guide. 參見 [[OpenAI_StructuredOutputs]]
