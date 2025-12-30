---
id: TruthfulQA_Lin2022
type: evidence
title: "TruthfulQA: Measuring How Models Mimic Human Falsehoods"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [truthfulness, benchmark, evaluation, ACL]
source_type: paper
evidence_level: E3
---

# TruthfulQA: Measuring How Models Mimic Human Falsehoods

## Citation

**標題**: TruthfulQA: Measuring How Models Mimic Human Falsehoods
**作者**: Stephanie Lin, Jacob Hilton, Owain Evans
**發表**: ACL 2022, pages 3214–3252
**arXiv**: [2109.07958](https://arxiv.org/abs/2109.07958)
**ACL Anthology**: [aclanthology.org/2022.acl-long.229](https://aclanthology.org/2022.acl-long.229/)
**GitHub**: [github.com/sylinrl/TruthfulQA](https://github.com/sylinrl/TruthfulQA)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **Benchmark 規模**：817 個問題，涵蓋 38 個類別（健康、法律、金融、政治等）。

2. **人類 vs 模型表現**：
   - 最佳模型（GPT-3）truthfulness: 58%
   - 人類表現: 94%

3. **Inverse Scaling**：更大的模型在 TruthfulQA 上反而更不 truthful（與其他 NLP 任務相反）。

4. **原因分析**：模型會學習並模仿人類的常見誤解（imitative falsehoods）。

5. **自動評測**：論文 finetune 了 GPT-judge 來自動評測，與人類評估有 90-96% 一致性。

### [I] 可推論的主張

1. LLM 可能傳播人類常見的錯誤認知。
2. 模型規模增大不等於更 truthful。
3. 特定領域（健康、法律）的幻覺風險更高。

---

## Limitations（限制與假設）

- 主要測試英文
- 問題設計針對「人類常見誤解」，不涵蓋所有類型的錯誤

---

## Where to Use（應連結到）

- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡
- [[SME_中小企業通用_客服與工單]] - Domain Pack（風險評估）

---

## 短評

TruthfulQA 揭示了 LLM 的重要局限：會學習並傳播人類的錯誤認知。對於高風險領域（醫療、法律、金融）的 AI 應用設計非常重要。
