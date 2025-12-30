---
type: bottleneck
title: "資料治理與權限（Data Governance & Access Control）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [data-governance, access-control, security, privacy, GDPR]
status: stable
evidence_level: E3
---

# 資料治理與權限（Data Governance & Access Control）

> **一句話**：LLM 應用可能導致敏感資料外洩、權限混亂、合規風險。

---

## 風險分類

### 資料安全風險

| 風險類型 | 描述 | 嚴重度 |
|----------|------|--------|
| **資料外洩** | 敏感資料被未授權存取 | 高 |
| **權限混亂** | 使用者看到不該看的內容 | 高 |
| **資料中毒** | 惡意資料污染知識庫 | 中 |
| **Prompt Injection** | 惡意輸入控制 LLM 行為 | 高 |

### 合規風險

| 法規 | 適用範圍 | 關鍵要求 |
|------|---------|---------|
| **GDPR** | 歐盟 | 資料最小化、刪除權、同意 |
| **EU AI Act** | 歐盟 | AI 系統風險分級、透明度 |
| **個資法** | 台灣 | 蒐集、處理、利用規範 |

[F] EU AI Act（Regulation EU 2024/1689）於 2024 年 8 月 1 日生效，是全球首個全面性 AI 法規框架[^EU_AI_Act_2024]。

---

## 症狀識別

### 常見症狀

| 症狀 | 描述 | 檢測方式 |
|------|------|---------|
| **跨部門資料洩漏** | A 部門看到 B 部門資料 | 存取日誌分析 |
| **敏感詞出現** | 回答中包含 PII/機密 | 輸出過濾 |
| **知識庫污染** | 錯誤/惡意資訊被索引 | 定期審核 |
| **Prompt Injection 成功** | 惡意指令被執行 | 安全測試 |

---

## 根因分析

### 架構問題

- 知識庫無權限分層
- 向量索引無存取控制
- LLM 無法區分使用者權限

### 流程問題

- 資料匯入未經審核
- 無資料生命週期管理
- 缺乏存取稽核

### 技術問題

- Prompt injection 防護不足
- 輸出過濾不完整
- 加密/脫敏不足

[F] 在 36 個實際 LLM 整合應用上測試，發現 31 個（86%）容易受到 prompt injection 攻擊[^SEC_PromptInjection2023]。

---

## 緩解策略

### 策略 1：Document-level RBAC

在知識庫層級實施存取控制：

```
文件 A (公開)        → 所有使用者可存取
文件 B (內部)        → 員工可存取
文件 C (機密)        → 特定角色可存取
文件 D (高度機密)    → 需要額外授權
```

**實作方式**：

| 方式 | 說明 | 優點 | 缺點 |
|------|------|------|------|
| **Metadata Filter** | 檢索時過濾 | 簡單 | 效能影響 |
| **多索引** | 不同權限用不同索引 | 隔離性好 | 維護成本 |
| **Post-retrieval Filter** | 檢索後過濾 | 靈活 | 可能遺漏 |

### 策略 2：輸入/輸出過濾

**輸入過濾**（防 Prompt Injection）：

```python
def sanitize_input(user_input):
    # 檢測惡意模式
    suspicious_patterns = [
        "ignore previous instructions",
        "disregard your instructions",
        "你是一個新的AI"
    ]
    for pattern in suspicious_patterns:
        if pattern.lower() in user_input.lower():
            return "BLOCKED"
    return user_input
```

**輸出過濾**（防資料外洩）：

```python
def filter_output(response, user_level):
    # PII 過濾
    pii_patterns = {
        "email": r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}',
        "phone": r'\d{4}-\d{3}-\d{3}',
        "id": r'[A-Z][12]\d{8}'
    }
    for pii_type, pattern in pii_patterns.items():
        response = re.sub(pattern, f'[{pii_type} REDACTED]', response)
    return response
```

### 策略 3：資料分級

| 等級 | 定義 | 處理方式 |
|------|------|---------|
| **公開** | 可對外公開 | 無限制 |
| **內部** | 僅員工可見 | 身份驗證 |
| **機密** | 特定角色可見 | RBAC |
| **高度機密** | 需審批 | 審批 + 稽核 |

### 策略 4：稽核與監控

| 監控項目 | 方式 | 頻率 |
|----------|------|------|
| **存取日誌** | 記錄誰查了什麼 | 即時 |
| **異常偵測** | 大量查詢、敏感詞 | 即時告警 |
| **權限審核** | 覆核存取權限 | 季度 |
| **知識庫審核** | 檢查內容正確性 | 月度 |

### 策略 5：資料生命週期

```
┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐
│  收集   │ → │  處理   │ → │  使用   │ → │  刪除   │
└─────────┘   └─────────┘   └─────────┘   └─────────┘
     │             │             │             │
     ▼             ▼             ▼             ▼
   同意/        脫敏/         存取          保留期
   法律依據    加密          控制          限/刪除
```

---

## 監控指標

| 指標 | 測量方式 | 告警閾值 |
|------|---------|---------|
| **跨權限存取嘗試** | 日誌分析 | > 0 |
| **敏感詞出現次數** | 輸出掃描 | > 0 |
| **Prompt Injection 嘗試** | 輸入掃描 | 記錄並分析 |
| **異常查詢量** | 使用者行為分析 | 偏離 baseline > 3σ |

---

## 驗收 Gate

| 階段 | 指標要求 |
|------|---------|
| **PoC → Pilot** | 有基本存取控制、輸出過濾 |
| **Pilot → Prod** | RBAC 完整、稽核日誌、安全測試通過 |
| **Prod 維護** | 定期安全審計、合規檢查 |

---

## 反模式（Anti-patterns）

| 反模式 | 描述 | 修正 |
|--------|------|------|
| **全員可存取** | 知識庫無權限控制 | 實施 RBAC |
| **信任使用者輸入** | 不驗證/過濾輸入 | 輸入過濾 |
| **無輸出過濾** | 敏感資料直接輸出 | 輸出過濾 |
| **無稽核日誌** | 無法追蹤存取 | 建立稽核機制 |
| **敏感資料未脫敏** | PII 直接入庫 | 脫敏/加密 |
| **忽略合規** | 未考慮法規要求 | 法規評估 |

---

## 合規檢查清單

### GDPR 相關

- [ ] 資料處理有法律依據（同意/合約/合法利益）
- [ ] 實施資料最小化原則
- [ ] 可執行刪除權（被遺忘權）
- [ ] 資料處理活動紀錄
- [ ] 資料保護影響評估（DPIA）

### EU AI Act 相關

[F] EU AI Act 採用風險導向方法，將 AI 系統分為四個風險等級[^EU_AI_Act_2024]。

- [ ] 確認系統風險等級
- [ ] 高風險系統需符合透明度要求
- [ ] 禁止的 AI 實務已於 2025/2/2 生效

---

## 相關連結

- **能力卡**：[[RAG問答_RAG-QA]]
- **Playbook**：[[RAG_企業知識問答_Playbook]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]]

---

## 參考來源

[^SEC_PromptInjection2023]: Prompt Injection attack against LLM-integrated Applications (HouYi). arXiv:2306.05499. 參見 [[SEC_PromptInjection_2023]]

[^EU_AI_Act_2024]: EU AI Act (Regulation EU 2024/1689). 參見 [[EU_AI_Act_2024]]

[^GDPR_2016]: General Data Protection Regulation (2016/679). 參見 [[GDPR_2016]]
