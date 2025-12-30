---
id: SUM_FactualConsistency2024
type: evidence
title: "Factual Consistency Evaluation of Summarization in the Era of LLMs"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [summarization, factual-consistency, evaluation, LLM]
source_type: paper
evidence_level: E3
---

# Factual Consistency Evaluation of Summarization in the Era of LLMs

## Citation

**標題**: Factual Consistency Evaluation of Summarization in the Era of Large Language Models
**arXiv**: [2402.13758](https://arxiv.org/abs/2402.13758)
**時間**: February 2024

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **問題定義**：自動生成摘要中的事實不一致可能導致錯誤資訊或風險。

2. **現有指標局限**：現有事實一致性（FC）指標受限於效能、效率和可解釋性。

3. **LLM 潛力**：LLM 在文本評估上展現顯著潛力，但在摘要 FC 評估的有效性尚待探索。

4. **TreatFact 資料集**：論文引入 TreatFact，包含 LLM 生成的臨床文本摘要，由領域專家標註 FC。

5. **跨領域評測**：論文在新聞和臨床兩個領域評測了 11 個 LLM 的 FC 評估能力。

### [I] 可推論的主張

1. 醫療/臨床領域的摘要 FC 要求更高，需要專家驗證。
2. LLM 可作為 FC 評估工具，但需要領域適配。

---

## Limitations

- 聚焦於新聞和臨床領域，其他領域需驗證
- LLM-as-judge 本身可能有偏差

---

## Where to Use

- [[文件摘要_Summarization]] - 能力卡（評測方法）
- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡
