---
id: CLS_ZeroShotClassifier2023
type: evidence
title: "Large Language Models Are Zero-Shot Text Classifiers"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [classification, zero-shot, LLM, CoT]
source_type: paper
evidence_level: E3
---

# Large Language Models Are Zero-Shot Text Classifiers

## Citation

**標題**: Large Language Models Are Zero-Shot Text Classifiers
**arXiv**: [2312.01044](https://arxiv.org/abs/2312.01044)
**時間**: December 2023

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **CoT 應用於分類**：隨著 Chain of Thought（CoT）prompting 的提出，LLM 可以使用 zero-shot learning 搭配逐步推理 prompt 進行分類。

2. **Zero-shot 優勢**：Zero-shot LLM 分類可以直接使用預訓練模型預測已見和未見類別，緩解傳統方法的限制。

3. **實驗結果**：實驗結果顯示 LLM 在分析的四個資料集中有三個上是有效的 zero-shot 文本分類器。

### [I] 可推論的主張

1. LLM 可以處理動態類別，不需要為新類別重新訓練。
2. Zero-shot 分類適合類別經常變動的場景。

---

## Where to Use

- [[分類與路由_Classification-Routing]] - 能力卡（Zero-shot 方法）
