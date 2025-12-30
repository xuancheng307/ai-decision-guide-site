---
id: Hallucination_Huang2023
type: evidence
title: "A Survey on Hallucination in Large Language Models"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [hallucination, LLM, survey, ACM-TOIS]
source_type: paper
evidence_level: E3
---

# A Survey on Hallucination in Large Language Models

## Citation

**標題**: A Survey on Hallucination in Large Language Models: Principles, Taxonomy, Challenges, and Open Questions
**作者**: Lei Huang et al. (11 位作者)
**發表**: ACM Transactions on Information Systems, 2024
**arXiv**: [2311.05232](https://arxiv.org/abs/2311.05232)
**ACM**: [dl.acm.org/doi/10.1145/3703155](https://dl.acm.org/doi/10.1145/3703155)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **幻覺分類法**：幻覺分為兩大類：
   - **Factuality Hallucination**：事實錯誤
   - **Faithfulness Hallucination**：不忠於輸入/context

2. **幻覺成因**：論文詳細分析了導致幻覺的因素（訓練資料、模型架構、解碼策略等）。

3. **RAG 的局限**：即使使用 RAG，系統仍可能產生幻覺，RAG 無法完全消除問題。

4. **檢測方法**：論文整理了多種 hallucination detection 方法和 benchmark。

### [I] 可推論的主張

1. 幻覺是 LLM 的固有特性，需要多層緩解策略。
2. 不同任務的幻覺類型和風險不同，需要針對性處理。

---

## Limitations（限制與假設）

- Survey 論文，不提供新方法
- 領域發展快，需要持續追蹤更新

---

## Where to Use（應連結到）

- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡
- [[RAG問答_RAG-QA]] - 能力卡
- [[SME_中小企業通用_客服與工單]] - Domain Pack

---

## Related Paper

**Hallucination is Inevitable: An Innate Limitation of Large Language Models**
- arXiv: [2401.11817](https://arxiv.org/abs/2401.11817)
- 主張：從計算理論角度證明 LLM 幻覺無法完全消除

---

## 短評

這是目前最全面的 LLM 幻覺 survey 之一。對於理解幻覺的本質、分類、檢測和緩解非常有價值。Factuality vs Faithfulness 的分類對實務設計很有幫助。
