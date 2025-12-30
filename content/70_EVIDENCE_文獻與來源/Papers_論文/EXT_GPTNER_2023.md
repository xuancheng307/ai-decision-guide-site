---
id: EXT_GPTNER2023
type: evidence
title: "GPT-NER: Named Entity Recognition via Large Language Models"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [NER, extraction, LLM, GPT]
source_type: paper
evidence_level: E3
---

# GPT-NER: Named Entity Recognition via Large Language Models

## Citation

**標題**: GPT-NER: Named Entity Recognition via Large Language Models
**arXiv**: [2304.10428](https://arxiv.org/abs/2304.10428)
**時間**: April 2023

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **LLM NER 表現**：儘管大型語言模型在多種 NLP 任務上達到 SOTA，其在 NER 上的表現仍顯著低於監督式 baseline。

2. **差距存在**：LLM 在 NER 任務上與專門訓練的模型存在效能差距。

3. **方法探索**：論文探索使用 LLM 進行 NER 的方法。

### [I] 可推論的主張

1. 對於高精度 NER 需求，可能仍需要專門訓練的模型。
2. LLM 可作為 NER 的快速原型工具，但生產環境需評估精度。

---

## Key Data

| 方法 | NER 效能 | 適用場景 |
|------|---------|---------|
| 監督式模型 | 最高 | 生產環境、高精度需求 |
| LLM Zero-shot | 較低 | 快速原型、探索 |
| LLM + Few-shot | 中等 | 中等精度需求 |

---

## Where to Use

- [[文件抽取_Information-Extraction]] - 能力卡（NER 方法）
