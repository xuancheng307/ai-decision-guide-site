---
id: SUM_ROUGELimitations2024
type: evidence
title: "Do Automatic Factuality Metrics Measure Factuality? A Critical Evaluation"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [summarization, ROUGE, factuality, metrics]
source_type: paper
evidence_level: E3
---

# Do Automatic Factuality Metrics Measure Factuality? A Critical Evaluation

## Citation

**標題**: Do Automatic Factuality Metrics Measure Factuality? A Critical Evaluation
**arXiv**: [2411.16638](https://arxiv.org/abs/2411.16638)
**時間**: November 2024

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **ROUGE 飽和**：現代 LLM 可以生成高度可讀的摘要，傳統指標如 ROUGE 已經飽和。

2. **LLM 仍有不準確**：LLM 仍然會在摘要中引入不準確之處。

3. **事實不一致難以自動測量**：測量這些通常微妙的事實不一致已證明具有挑戰性，推動了新事實性指標的發展。

4. **指標演進**：評估方法已從粗粒度的摘要級評分演進到細粒度的句子級評估。

5. **指標類型演進**：自動指標從傳統相似度指標（ROUGE、BERTScore）演進到 NLI/QA 基礎方法，再到 LLM 基礎方法。

### [I] 可推論的主張

1. ROUGE 不應作為唯一的摘要評估指標。
2. 需要結合多種指標進行綜合評估。

---

## Key Data

| 指標類型 | 代表方法 | 局限性 |
|----------|---------|--------|
| 傳統相似度 | ROUGE, BERTScore | 無法捕捉事實性 |
| NLI/QA 基礎 | - | 需要額外模型 |
| LLM 基礎 | GPT-4 評估 | 成本高、可能有偏差 |

---

## Where to Use

- [[文件摘要_Summarization]] - 能力卡（評測限制）
