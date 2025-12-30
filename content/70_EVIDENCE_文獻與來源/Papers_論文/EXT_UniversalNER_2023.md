---
id: EXT_UniversalNER2023
type: evidence
title: "UniversalNER: Targeted Distillation from Large Language Models"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [NER, universal, distillation, benchmark]
source_type: paper
evidence_level: E3
---

# UniversalNER: Targeted Distillation from Large Language Models for Open Named Entity Recognition

## Citation

**標題**: UniversalNER: Targeted Distillation from Large Language Models for Open Named Entity Recognition
**網站**: [universal-ner.github.io](https://universal-ner.github.io/)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **效能數據**：UniversalNER-7B 在 20 個資料集上達到平均 F1 84.78%。

2. **超越 baseline**：分別超越 BERT-base 和 InstructUIE-11B 4.69% 和 3.62%。

3. **資料集規模**：UniversalNER 資料集包含 45,889 個輸入-輸出對，涵蓋 240,725 個實體和 13,020 種不同實體類型。

4. **領域覆蓋**：涵蓋從通用領域到臨床領域的實體類型。

### [I] 可推論的主張

1. 透過蒸餾可以創建高效的 NER 模型。
2. 開放 NER 可以處理多種實體類型。

---

## Key Data

| 模型 | 20 資料集平均 F1 | 參數量 |
|------|-----------------|-------|
| UniversalNER-7B | 84.78% | 7B |
| BERT-base | 80.09% | 110M |
| InstructUIE-11B | 81.16% | 11B |

---

## Where to Use

- [[文件抽取_Information-Extraction]] - 能力卡（Benchmark 數據）
