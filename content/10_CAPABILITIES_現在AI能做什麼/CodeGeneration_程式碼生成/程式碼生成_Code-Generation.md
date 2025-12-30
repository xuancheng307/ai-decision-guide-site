---
type: capability
title: "程式碼生成（Code Generation）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [code-generation, coding, LLM, copilot, programming]
status: stable
evidence_level: E3
---

# 程式碼生成（Code Generation）

> **一句話**：讓 AI 根據自然語言描述或現有程式碼，生成、補全、解釋或重構程式碼。

---

## 基本資訊

| 項目 | 內容 |
|------|------|
| **輸入** | 自然語言需求、現有程式碼、錯誤訊息 |
| **輸出** | 程式碼、解釋、測試、文件 |
| **成熟度** | **Production-ready**（輔助場景），**Pilot**（自動化場景） |
| **最後更新** | 2025-01-XX |

---

## 1. 能力定義（Definition）

**程式碼生成任務類型**：

| 任務類型 | 說明 | 典型場景 |
|----------|------|---------|
| **Code Completion** | 補全部分程式碼 | IDE 自動補全 |
| **Code Generation** | 從描述生成完整程式碼 | 功能實作 |
| **Code Explanation** | 解釋程式碼邏輯 | 程式碼理解 |
| **Code Refactoring** | 改善程式碼品質 | 程式碼維護 |
| **Bug Fixing** | 找出並修復錯誤 | Debug |
| **Test Generation** | 生成測試案例 | 測試覆蓋 |
| **Code Translation** | 跨語言轉換 | 語言遷移 |

---

## 2. 能做到的範圍（What it can do now）

### 2.1 表現良好的場景

- [x] 常見語言的標準功能實作（Python, JavaScript, Java, etc.）
- [x] Boilerplate 程式碼生成
- [x] 單元測試生成
- [x] 程式碼解釋和文件生成
- [x] 簡單到中等複雜度的 bug 修復
- [x] 正則表達式生成
- [x] SQL 查詢生成
- [x] API 呼叫程式碼生成

### 2.2 表現程度

#### Metrics（評測指標）

| 指標 | 定義 | 適用場景 |
|------|------|---------|
| **Pass@k** | 生成 k 個樣本中至少一個通過測試的比例 | 功能正確性 |
| **CodeBLEU** | 程式碼結構相似度 | 程式碼品質 |
| **Cyclomatic Complexity** | 程式碼複雜度 | 可維護性 |
| **Test Coverage** | 生成測試的覆蓋率 | 測試品質 |

#### Public Benchmarks（公開基準）

| Benchmark | 任務 | 頂尖表現 | 來源 |
|-----------|------|---------|------|
| **HumanEval** | Python 函數生成 | ~90% Pass@1 (GPT-4, Claude 3.5) | OpenAI |
| **MBPP** | Python 基礎程式設計 | ~85% Pass@1 | Google |
| **SWE-bench** | 真實 GitHub issue 修復 | ~50% (GPT-4 + Agent) | Princeton |
| **CodeContests** | 競賽程式設計 | ~30% Pass@1 | DeepMind |

#### 語言支援程度

| 語言 | 支援程度 | 備註 |
|------|---------|------|
| Python | 最佳 | 訓練資料最多 |
| JavaScript/TypeScript | 極佳 | 前端、Node.js |
| Java | 佳 | 企業常用 |
| C/C++ | 佳 | 系統程式設計 |
| Go | 佳 | 雲端原生 |
| Rust | 中 | 相對新，資料較少 |
| SQL | 極佳 | 查詢生成 |

---

## 3. 適合的任務特徵（Good fit）

- [x] **需求明確**：功能描述清晰
- [x] **標準模式**：常見設計模式、CRUD 操作
- [x] **有範例可參考**：類似程式碼存在
- [x] **可測試**：有明確的輸入輸出規格
- [x] **輔助人類**：人工覆核後使用

---

## 4. 不適合/高風險（Bad fit / Red flags）

### 4.1 不適合的場景

- [ ] **高度創新演算法**：需要原創性設計
- [ ] **安全關鍵系統**：無人工覆核直接部署
- [ ] **複雜系統架構**：跨多服務的大規模重構
- [ ] **領域特定語言**：訓練資料極少的語言
- [ ] **效能關鍵**：需要極致優化

### 4.2 紅旗警訊

- [x] **程式碼安全漏洞**：LLM 可能生成不安全程式碼
- [x] **授權問題**：可能複製受版權保護的程式碼
- [x] **過度自信**：看似正確但有細微錯誤
- [x] **上下文遺失**：不了解專案整體架構

---

## 5. 常用落地模式（Patterns）

| 模式 | 適用情境 | 人工介入 | 風險 |
|------|---------|---------|------|
| **IDE Copilot** | 開發時輔助 | 高（每次接受前檢視） | 低 |
| **Chat-based Coding** | 互動式開發 | 高（對話式確認） | 低 |
| **Code Review Assistant** | 程式碼審查 | 中（建議需人工確認） | 低 |
| **Test Generation** | 自動生成測試 | 中（需驗證測試品質） | 中 |
| **Auto-fix Suggestions** | 自動修復建議 | 中（需確認修復） | 中 |
| **Autonomous Coding Agent** | 自動完成任務 | 低（主要審查結果） | 高 |

### 使用模式建議

```
低風險（推薦）：
  IDE 補全 → 開發者逐行審查 → 合併

中風險（需審查）：
  需求描述 → AI 生成 → 人工審查 → 測試 → 合併

高風險（謹慎）：
  Issue → Agent 自動修復 → CI/CD 測試 → 人工審查 → 合併
```

---

## 6. 常用工具（Tools）

| 層級 | 工具 | 備註 |
|------|------|------|
| **IDE 整合** | GitHub Copilot | 最廣泛使用 |
| **IDE 整合** | Cursor | AI-first IDE |
| **IDE 整合** | Codeium | 免費選項 |
| **模型 API** | GPT-4o, Claude 3.5 | 直接 API 呼叫 |
| **Agent 框架** | Aider, Continue | 自動化開發 |
| **程式碼模型** | CodeLlama, StarCoder, DeepSeek | 開源選項 |

---

## 7. 瓶頸與對策（Bottlenecks & Mitigations）

| 瓶頸 | 症狀 | 緩解策略 | 連結 |
|------|------|---------|------|
| **Context 限制** | 大型專案無法完整理解 | RAG、分塊處理 | [[上下文長度限制_Context-Length-Limit]] |
| **幻覺** | 生成不存在的 API | 強制文件參照、測試驗證 | [[幻覺與可追溯性_Hallucination-Grounding]] |
| **安全漏洞** | SQL injection、XSS | 安全掃描、code review | |
| **授權風險** | 複製受保護程式碼 | 授權掃描工具 | |
| **一致性** | 風格不統一 | Linter、格式化工具 | |

---

## 8. 安全考量

### 程式碼安全風險

| 風險類型 | 說明 | 緩解措施 |
|----------|------|---------|
| **Injection** | SQL/Command injection | 參數化查詢、輸入驗證 |
| **認證漏洞** | 弱密碼邏輯 | 安全審查 |
| **敏感資料** | 硬編碼 secrets | Secret 掃描 |
| **依賴風險** | 不安全套件 | 依賴掃描 |

### 必要防護

- [ ] 所有 AI 生成程式碼必須 code review
- [ ] 執行靜態安全掃描（SAST）
- [ ] 敏感專案避免使用雲端 AI 服務
- [ ] 監控異常程式碼提交模式

---

## 9. 成熟度分級（Maturity）

| 階段 | 定義 | 這個能力的狀態 |
|------|------|-----------------|
| **PoC** | 實驗室環境可行 | ✅ 極易達成 |
| **Pilot** | 小規模真實環境可行 | ✅ IDE Copilot 已普及 |
| **Production** | 大規模穩定運行 | ⚠️ 輔助模式可，自動化需謹慎 |

**Production 需要**：
- 強制 code review 流程
- CI/CD 測試覆蓋
- 安全掃描整合
- 使用量和品質監控

---

## 10. 發展預期（Outlook & Watch signals）

### 10.1 觀測訊號

- [ ] **SWE-bench 突破**：真實問題解決能力
- [ ] **多檔案理解**：長 context 和 RAG 進步
- [ ] **Agent 成熟度**：自主開發能力

### 10.2 預期趨勢

| 時間範圍 | 預期變化 | 依據 |
|----------|---------|------|
| 6 個月內 | Agent 能力持續提升 | [I] 技術發展趨勢 |
| 1 年內 | 更多企業採用 Copilot | [I] 採用率增長 |
| 2 年內 | 自動化程度提高 | [I] 技術成熟 |

---

## ROI 估算

### 開發效率提升

| 研究來源 | 效率提升 | 條件 |
|----------|---------|------|
| GitHub (2022) | 55% 更快完成任務 | Copilot 用戶調查 |
| McKinsey (2023) | 20-45% 生產力提升 | 開發任務 |

### 成本效益

| 項目 | 估算 |
|------|------|
| **Copilot 費用** | $19/月/開發者 |
| **效率提升** | 20-40% |
| **Break-even** | 開發者時薪 > $10 即划算 |

---

## 相關連結

- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]], [[上下文長度限制_Context-Length-Limit]]
- **工具卡**：[[Evaluation_評測與可觀測性]]

---

## 參考來源

> 注意：本能力卡的 benchmark 數據來自各模型官方發布和公開測試結果。由於此領域發展快速，建議定期查閱最新 benchmark。

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Status | Stable |
| 待補 Evidence | HumanEval/MBPP/SWE-bench 官方文件 |
| 待驗證 | 效率提升數據需更多來源 |
