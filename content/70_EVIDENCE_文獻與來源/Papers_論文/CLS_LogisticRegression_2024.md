---
id: CLS_LogisticRegression2024
type: evidence
title: "Logistic Regression Makes Small LLMs Strong Tens-of-Shot Classifiers"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [classification, few-shot, embedding, logistic-regression]
source_type: paper
evidence_level: E3
---

# Logistic Regression Makes Small LLMs Strong and Explainable "Tens-of-Shot" Classifiers

## Citation

**標題**: Logistic Regression makes small LLMs strong and explainable "tens-of-shot" classifiers
**arXiv**: [2408.03414](https://arxiv.org/abs/2408.03414)
**時間**: August 2024

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **方法**：在小型 LLM 的 embedding 上使用 penalised logistic regression 進行分類。

2. **評測規模**：在 17 個句子分類任務（2-4 類別）上進行實驗。

3. **核心發現**：在 "tens-of-shot" 情境下，小型 LLM + logistic regression 的效能等於（通常優於）大型 LLM。

4. **樣本效率**：所需標註樣本數不超過驗證大型 LLM 效能所需的數量。

### [I] 可推論的主張

1. 結合傳統 ML 和 LLM embedding 可能是高效的分類方案。
2. 少量標註資料即可達成良好分類效能。

---

## Where to Use

- [[分類與路由_Classification-Routing]] - 能力卡（實作模式）
