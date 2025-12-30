---
id: CLS_SmallModels2024
type: evidence
title: "Small Language Models are Good Too: An Empirical Study of Zero-Shot Classification"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [classification, small-models, zero-shot, benchmark]
source_type: paper
evidence_level: E3
---

# Small Language Models are Good Too: An Empirical Study of Zero-Shot Classification

## Citation

**標題**: Small Language Models are Good Too: An Empirical Study of Zero-Shot Classification
**arXiv**: [2404.11122](https://arxiv.org/abs/2404.11122)
**時間**: April 2024

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **研究目標**：評估小型語言模型在 zero-shot 文本分類上的表現，挑戰大型模型主導的現狀。

2. **評測規模**：在 15 個資料集上評測從 77M 到 40B 參數的語言模型，使用不同架構和評分函數。

3. **核心發現**：提供強有力的證據表明小型模型在 zero-shot 分類上是有效的。

4. **效能比較**：小型模型在許多資料集上的表現與大型模型相當。

### [I] 可推論的主張

1. 不一定需要最大的模型來達成分類任務。
2. 小型模型可顯著降低推論成本。

---

## Key Data

| 模型規模 | Zero-shot 分類效能 | 推論成本 |
|----------|-------------------|---------|
| 77M-1B | 在多數任務上接近大模型 | 極低 |
| 1B-7B | 良好 | 低 |
| 7B-40B | 最佳 | 中等 |
| 40B+ | 邊際提升有限 | 高 |

---

## Where to Use

- [[分類與路由_Classification-Routing]] - 能力卡（模型選擇）
