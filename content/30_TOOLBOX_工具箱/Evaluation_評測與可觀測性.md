---
type: tool
title: "評測與可觀測性 (Evaluation & Observability)"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
expiry_date: 2025-07-XX
expiry_policy: 6_months
tags: [evaluation, observability, metrics, monitoring, RAGAS]
status: stable
---

# 評測與可觀測性 (Evaluation & Observability)

> **一句話**：測量 LLM 應用的品質，並在生產環境中持續監控。

---

## 評測 vs 可觀測性

| 階段 | 目的 | 時機 | 工具類型 |
|------|------|------|---------|
| **Evaluation（評測）** | 驗證品質是否達標 | 開發/部署前 | Offline Eval |
| **Observability（可觀測性）** | 監控生產環境行為 | 部署後 | Tracing, Monitoring |

---

## 評測框架

### 通用 LLM 評測

| 框架 | 特點 | 適用場景 | 來源 |
|------|------|---------|------|
| **RAGAS** | RAG 專用、指標完整 | RAG 評測 | [^RAGAS_Es2023] |
| **DeepEval** | 多指標、易整合 CI | 通用 LLM | [^DOC_DeepEval] |
| **TruLens** | 回饋迴圈、可解釋 | 迭代優化 | [^DOC_TruLens] |
| **LangSmith** | LangChain 整合 | LangChain 專案 | [^DOC_LangSmith] |

### RAG 專用指標（RAGAS）

| 指標 | 測量什麼 | 公式概念 | 典型範圍 |
|------|---------|---------|---------|
| **Faithfulness** | 答案與 context 一致性 | 答案中可被 context 支持的比例 | 70-90% |
| **Answer Relevancy** | 答案與問題相關性 | 答案能回應問題的程度 | 75-95% |
| **Context Precision** | 檢索精度 | 檢索結果中相關的比例 | 60-85% |
| **Context Recall** | 檢索召回 | 所需資訊被檢索到的比例 | 65-90% |

---

## 可觀測性工具

### Tracing（追蹤）

| 工具 | 特點 | 整合方式 |
|------|------|---------|
| **LangSmith** | LangChain 原生 | SDK 自動 |
| **Langfuse** | 開源、自建可行 | SDK / API |
| **Arize Phoenix** | 向量可視化 | SDK |
| **Weights & Biases** | ML 全流程 | SDK |

### Monitoring（監控）

| 指標類型 | 範例 | 監控方式 |
|----------|------|---------|
| **Latency** | P50/P95/P99 延遲 | Time-series |
| **Token Usage** | Input/Output tokens | Counter |
| **Error Rate** | 失敗/拒答比例 | Rate |
| **Faithfulness** | 線上抽樣評測 | Batch Eval |

---

## 評測流程建議

### 1. 開發階段（Offline Eval）

```
定義評測集（100+ 問答對）
    ↓
選擇指標（依任務類型）
    ↓
建立 Baseline（無 RAG / 簡單 prompt）
    ↓
迭代改進 → 比較指標變化
    ↓
達到 Gate 標準 → 進入 Pilot
```

### 2. 生產階段（Online Monitoring）

```
全量 Tracing（延遲、token、錯誤）
    ↓
抽樣評測（每日 1-5% 樣本）
    ↓
告警設定（指標下降 > 10%）
    ↓
回饋迴圈 → 持續優化
```

---

## Gate 標準範例

| 階段 | 指標 | 門檻 | 備註 |
|------|------|------|------|
| PoC → Pilot | Faithfulness | > 70% | 100 題測試集 |
| Pilot → Prod | Faithfulness | > 80% | 500 題 + 真實用戶回饋 |
| Prod 維護 | Faithfulness 變化 | < -5% | 持續監控 |

---

## 常見陷阱

| 陷阱 | 症狀 | 解法 |
|------|------|------|
| **評測集過小** | 指標不穩定 | 至少 100 題，覆蓋多場景 |
| **評測集洩漏** | 過擬合評測集 | 定期更新評測集 |
| **只看平均值** | 忽略 tail case | 檢視 P95/P99 與錯誤分布 |
| **無 baseline** | 無法判斷改進幅度 | 先建立 baseline |

---

## 相關連結

- **能力卡**：[[RAG問答_RAG-QA]]
- **Playbook**：[[RAG_企業知識問答_Playbook]]
- **瓶頸卡**：[[幻覺與可追溯性_Hallucination-Grounding]]

---

## 過期政策（Expiry Policy）

| 項目 | 值 |
|------|------|
| **過期週期** | 6 個月 |
| **過期日期** | 2025-07-XX |
| **驗證觸發** | 新評測框架出現 / 指標定義變化 / 工具更新 |

### 需驗證項目

- [ ] RAGAS 版本和指標定義變化
- [ ] 是否有新的評測框架
- [ ] 可觀測性工具更新
- [ ] 業界最佳實踐變化

### 更新來源

- RAGAS 官方文檔和 changelog
- 評測工具官方 blog
- ML 可觀測性社群趨勢

---

## 參考來源

[^RAGAS_Es2023]: Es, S. et al. (2023). RAGAS: Automated Evaluation of Retrieval Augmented Generation. 參見 [[RAGAS_2023]]

[^DOC_DeepEval]: DeepEval Documentation. https://docs.deepeval.com

[^DOC_TruLens]: TruLens Documentation. https://www.trulens.org/docs

[^DOC_LangSmith]: LangSmith Documentation. https://docs.smith.langchain.com

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Status | Stable |
| 過期日期 | 2025-07-XX |
| 待補 Evidence | 各評測工具詳細比較 |
