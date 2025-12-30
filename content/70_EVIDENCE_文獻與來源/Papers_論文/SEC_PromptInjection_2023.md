---
id: SEC_PromptInjection2023
type: evidence
title: "Prompt Injection Attack against LLM-integrated Applications (HouYi)"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [security, prompt-injection, attack, LLM]
source_type: paper
evidence_level: E3
---

# Prompt Injection attack against LLM-integrated Applications

## Citation

**標題**: Prompt Injection attack against LLM-integrated Applications
**arXiv**: [2306.05499](https://arxiv.org/abs/2306.05499)
**時間**: June 2023

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **HouYi 技術**：HouYi 是一種黑盒 prompt injection 攻擊技術，包含三個關鍵元素：
   - 無縫整合的預構建 prompt
   - 誘導 context 分隔的注入 prompt
   - 設計達成攻擊目標的惡意 payload

2. **實際測試結果**：在 36 個實際 LLM 整合應用上部署 HouYi，發現 31 個應用容易受到 prompt injection 攻擊。

3. **廠商確認**：10 個廠商驗證了研究發現，包括 Notion。

### [I] 可推論的主張

1. Prompt injection 是 LLM 應用的重要安全風險。
2. 生產環境需要 prompt injection 防禦機制。

---

## Key Data

| 指標 | 數值 |
|------|------|
| 測試應用數 | 36 |
| 易受攻擊應用 | 31 (86%) |
| 廠商確認 | 10 |

---

## Where to Use

- [[資料治理與權限_Data-Governance-Access-Control]] - 瓶頸卡（安全風險）
- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡
