---
id: SUM_MultiDimEval2025
type: evidence
title: "An Empirical Comparison of Text Summarization: Multi-Dimensional Evaluation of LLMs"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [summarization, evaluation, LLM, metrics]
source_type: paper
evidence_level: E3
---

# An Empirical Comparison of Text Summarization: Multi-Dimensional Evaluation of LLMs

## Citation

**標題**: An Empirical Comparison of Text Summarization: A Multi-Dimensional Evaluation of Large Language Models
**arXiv**: [2504.04534](https://arxiv.org/abs/2504.04534)
**時間**: April 2025

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **ROUGE 局限**：傳統指標如 ROUGE 捕捉詞彙重疊，但無法衡量語義等價或事實準確性。

2. **評估框架權重**：論文的評估框架將事實一致性（Factual Consistency）權重設為 35%，作為摘要品質最關鍵的面向。

3. **高風險應用考量**：對於可能產生重大後果的高風險應用，事實一致性特別重要。

4. **多維度評估**：摘要評估需要多個維度，包括：流暢度、連貫性、相關性、事實一致性。

### [I] 可推論的主張

1. 單一指標不足以評估摘要品質。
2. 生產環境應優先監控事實一致性而非 ROUGE。

---

## Key Data

| 評估維度 | 建議權重 | 說明 |
|----------|---------|------|
| Factual Consistency | 35% | 最高優先級 |
| Relevance | 25% | 與原文相關性 |
| Coherence | 20% | 邏輯連貫性 |
| Fluency | 20% | 語言流暢度 |

---

## Where to Use

- [[文件摘要_Summarization]] - 能力卡（評測指標）
