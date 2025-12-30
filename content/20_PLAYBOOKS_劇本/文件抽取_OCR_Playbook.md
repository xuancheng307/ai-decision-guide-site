---
type: playbook
title: "文件抽取 OCR+Extraction Playbook"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [extraction, OCR, document-AI, structured-output]
status: stable
evidence_level: E3
---

# 文件抽取 OCR+Extraction Playbook

> **目標**：從掃描件、PDF、圖片中自動抽取結構化資訊（如發票欄位、合約條款）。

---

## 適用場景與前提條件

### 適用場景

- [x] 發票/收據自動錄入
- [x] 合約關鍵條款抽取
- [x] 表單數位化
- [x] 名片資訊抽取
- [x] 報表數據抽取

### 前提條件

| 條件 | 說明 | 檢查方式 |
|------|------|---------|
| 文件品質 | 掃描解析度 > 200 DPI | 抽樣檢查 |
| 格式相對固定 | 同類文件結構相似 | 樣本分析 |
| Schema 可定義 | 知道要抽取哪些欄位 | 需求確認 |
| 可接受人工覆核 | 關鍵欄位需驗證 | 流程確認 |

---

## 參考架構

```
┌─────────────────────────────────────────────────────────────┐
│                     文件輸入                                 │
│              (PDF / 圖片 / 掃描件)                           │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   預處理層                                   │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                   │
│  │ 圖片增強 │→ │ 傾斜校正 │→ │ 頁面分割 │                   │
│  └──────────┘  └──────────┘  └──────────┘                   │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   OCR 層                                     │
│  ┌──────────────────────────────────────┐                   │
│  │     文字辨識 (OCR Engine)             │                   │
│  │  Tesseract / EasyOCR / Cloud OCR     │                   │
│  └──────────────────────────────────────┘                   │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   抽取層                                     │
│  選項 A: LLM + Structured Output                            │
│  ┌──────────────────────────────────────┐                   │
│  │   OCR 文字 + Schema → LLM → JSON      │                   │
│  └──────────────────────────────────────┘                   │
│                                                              │
│  選項 B: Document AI Model                                  │
│  ┌──────────────────────────────────────┐                   │
│  │   圖片 → LayoutLM/Donut → JSON        │                   │
│  └──────────────────────────────────────┘                   │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   後處理層                                   │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                   │
│  │ 格式驗證 │→ │ 商業規則 │→ │ 信心度   │                   │
│  │          │  │ 檢查     │  │ 評估     │                   │
│  └──────────┘  └──────────┘  └──────────┘                   │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│              人工覆核（依信心度）                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 分步實作指南

### Step 1：Schema 設計

#### 1.1 定義抽取欄位

```json
// 發票抽取 Schema 範例
{
  "invoice_number": {"type": "string", "required": true},
  "date": {"type": "date", "format": "YYYY-MM-DD", "required": true},
  "vendor_name": {"type": "string", "required": true},
  "total_amount": {"type": "number", "required": true},
  "tax_amount": {"type": "number", "required": false},
  "line_items": {
    "type": "array",
    "items": {
      "description": "string",
      "quantity": "number",
      "unit_price": "number"
    }
  }
}
```

#### 1.2 使用 Pydantic（Python）

```python
from pydantic import BaseModel
from typing import List, Optional
from datetime import date

class LineItem(BaseModel):
    description: str
    quantity: float
    unit_price: float

class Invoice(BaseModel):
    invoice_number: str
    date: date
    vendor_name: str
    total_amount: float
    tax_amount: Optional[float]
    line_items: List[LineItem]
```

---

### Step 2：OCR 選型

| OCR 方案 | 適用場景 | 語言支援 | 成本 |
|----------|---------|---------|------|
| **Tesseract** | 一般印刷體、開源 | 100+ | 免費 |
| **EasyOCR** | 多語言、手寫體 | 80+ | 免費 |
| **Google Vision** | 高品質、手寫體 | 100+ | $1.5/1000頁 |
| **AWS Textract** | 表格/表單專用 | 多語言 | $1.5/1000頁 |
| **Azure Form Recognizer** | 企業整合 | 多語言 | $1/1000頁 |

[H] 建議：PoC 用 Tesseract/EasyOCR，生產環境用 Cloud OCR。

---

### Step 3：抽取方案選擇

#### 方案 A：OCR + LLM Structured Output

[F] OpenAI Structured Outputs 在 gpt-4o-2024-08-06 上達到 100% schema 遵循率[^API_OpenAI_StructuredOutputs]。

**適用**：文件類型多樣、快速原型

```python
# 偽代碼
from openai import OpenAI

client = OpenAI()

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "Extract invoice information from the following text."},
        {"role": "user", "content": ocr_text}
    ],
    response_format={
        "type": "json_schema",
        "json_schema": {
            "name": "invoice",
            "schema": invoice_schema
        }
    }
)
```

#### 方案 B：Document AI Model

[F] LayoutLMv3 使用統一的文本和圖像遮罩進行 Document AI 預訓練[^EXT_LayoutLMv3_2022]。

**適用**：大量同類文件、需要高精度

| 模型 | 特點 | 適用場景 |
|------|------|---------|
| **LayoutLMv3** | 文本+圖像+佈局 | 表單、發票 |
| **Donut** | 端到端、無需 OCR | 收據、文件 |
| **PaddleOCR** | 中文優化 | 中文文件 |

#### 方案 C：雲端 Document AI

| 平台 | 特點 | 適用場景 |
|------|------|---------|
| **AWS Textract** | 表格專用、高精度 | 表格、表單 |
| **Azure Form Recognizer** | 預建模型、客製化 | 企業文件 |
| **Google Document AI** | 通用、多語言 | 通用文件 |

---

### Step 4：後處理驗證

#### 4.1 格式驗證

```python
# 日期格式驗證
import re
from datetime import datetime

def validate_date(date_str):
    patterns = [
        r'\d{4}-\d{2}-\d{2}',
        r'\d{2}/\d{2}/\d{4}',
        r'\d{4}年\d{1,2}月\d{1,2}日'
    ]
    for pattern in patterns:
        if re.match(pattern, date_str):
            return True
    return False

# 金額驗證
def validate_amount(amount_str):
    try:
        amount = float(amount_str.replace(',', '').replace('$', ''))
        return amount > 0
    except:
        return False
```

#### 4.2 商業規則檢查

```python
def validate_invoice(invoice):
    errors = []

    # 金額一致性
    calculated_total = sum(
        item.quantity * item.unit_price
        for item in invoice.line_items
    )
    if abs(calculated_total - invoice.total_amount) > 1:
        errors.append("Total amount mismatch")

    # 日期合理性
    if invoice.date > date.today():
        errors.append("Future date")

    return errors
```

#### 4.3 信心度評估

| 信心度 | 處理方式 |
|--------|---------|
| 高（> 90%） | 自動通過 |
| 中（70-90%） | 人工抽查 |
| 低（< 70%） | 人工覆核 |

---

## 評測指標與 Baseline

### 欄位級評測

| 指標 | 定義 | 目標 |
|------|------|------|
| **Field Accuracy** | 單欄位正確率 | > 90% |
| **Document Accuracy** | 整份文件正確率 | > 80% |
| **Schema Compliance** | 輸出格式正確 | 100% |

### 測試方法

```
1. 準備 100+ 份標註文件
2. 執行抽取
3. 逐欄位比對
4. 計算 Field Accuracy
5. 分析錯誤類型
```

---

## 成本估算方法

### 每文件成本

| 方案 | OCR 成本 | 抽取成本 | 總計 |
|------|---------|---------|------|
| Tesseract + GPT-4o | $0 | $0.02-0.05 | $0.02-0.05 |
| Cloud OCR + GPT-4o | $0.001-0.003 | $0.02-0.05 | $0.02-0.05 |
| AWS Textract | $0.015 | - | $0.015 |
| LayoutLM (自建) | $0 | GPU 成本 | 依規模 |

---

## 常見陷阱與修法

| 陷阱 | 症狀 | 修法 |
|------|------|------|
| **OCR 品質差** | 文字辨識錯誤 | 圖片預處理、換 OCR 引擎 |
| **手寫體** | 辨識率低 | 使用專門模型、人工處理 |
| **表格錯位** | 欄位對應錯誤 | 使用 Textract/LayoutLM |
| **數字混淆** | 0/O, 1/l/I | 後處理驗證、上下文推斷 |
| **多頁文件** | 跨頁資訊 | 頁面合併處理 |
| **Schema 太複雜** | 抽取不完整 | 簡化 Schema、分步抽取 |

[F] 儘管 LLM 在多種 NLP 任務上達到 SOTA，其在 NER 上的表現仍顯著低於監督式 baseline[^EXT_GPTNER2023]。

---

## Gate 標準

| 階段 | 指標要求 | 檢查項目 |
|------|---------|---------|
| **PoC → Pilot** | Field Accuracy > 80% | 50 份文件 |
| **Pilot → Prod** | Field Accuracy > 90%, 關鍵欄位 > 95% | 200 份 + 人工驗證 |
| **Prod 維護** | Field Accuracy 變化 < -3% | 持續監控 |

---

## 相關連結

- **能力卡**：[[文件抽取_Information-Extraction]]
- **工具卡**：[[Evaluation_評測與可觀測性]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]]

---

## 參考來源

[^EXT_LayoutLMv3_2022]: LayoutLMv3: Pre-training for Document AI. arXiv:2204.08387. 參見 [[EXT_LayoutLMv3_2022]]

[^EXT_GPTNER2023]: GPT-NER: Named Entity Recognition via Large Language Models. arXiv:2304.10428. 參見 [[EXT_GPTNER_2023]]

[^API_OpenAI_StructuredOutputs]: OpenAI Structured Outputs Guide. 參見 [[OpenAI_StructuredOutputs]]

[^EXT_UniversalNER2023]: UniversalNER: Targeted Distillation from LLMs. 參見 [[EXT_UniversalNER_2023]]
