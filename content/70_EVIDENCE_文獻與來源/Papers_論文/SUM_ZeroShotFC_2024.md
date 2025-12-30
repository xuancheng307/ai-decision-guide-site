---
id: SUM_ZeroShotFC2024
type: evidence
title: "Zero-shot Factual Consistency Evaluation Across Domains"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [summarization, factual-consistency, zero-shot, NLI]
source_type: paper
evidence_level: E3
---

# Zero-shot Factual Consistency Evaluation Across Domains

## Citation

**標題**: Zero-shot Factual Consistency Evaluation Across Domains
**arXiv**: [2408.04114](https://arxiv.org/abs/2408.04114)
**時間**: August 2024

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **任務統一**：論文統一了 NLI、摘要評估、事實驗證、事實一致性評估等任務來訓練跨領域 FC 評估模型。

2. **評測規模**：在包含 22 個資料集的綜合 benchmark 上評測，涵蓋多種任務、領域和文件長度。

3. **SOTA 效能**：相較 8 個 baseline，達到跨領域 SOTA 效能。

4. **Zero-shot 能力**：模型可 zero-shot 遷移到新領域進行 FC 評估。

### [I] 可推論的主張

1. FC 評估可泛化到多個領域，不需要領域特定訓練。
2. 統一框架可簡化評測流程。

---

## Where to Use

- [[文件摘要_Summarization]] - 能力卡（評測方法）
- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡（檢測方法）
