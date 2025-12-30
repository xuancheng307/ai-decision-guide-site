---
id: CLS_FineTuneVsZeroShot2024
type: evidence
title: "Fine-Tuned Small LLMs Still Significantly Outperform Zero-Shot Generative AI in Text Classification"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [classification, fine-tuning, zero-shot, LLM]
source_type: paper
evidence_level: E3
---

# Fine-Tuned 'Small' LLMs (Still) Significantly Outperform Zero-Shot Generative AI Models in Text Classification

## Citation

**標題**: Fine-Tuned 'Small' LLMs (Still) Significantly Outperform Zero-Shot Generative AI Models in Text Classification
**arXiv**: [2406.08660](https://arxiv.org/abs/2406.08660)
**時間**: June 2024

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **核心發現**：較小的微調 LLM 在文本分類任務上持續且顯著優於較大的 zero-shot prompted 模型。

2. **比較對象**：研究比較了三個主要生成式 AI 模型（ChatGPT GPT-3.5/GPT-4 和 Claude Opus）與多個微調 LLM。

3. **任務類型**：評測涵蓋多種分類任務，包括情感分析、贊成/反對、情緒分類、政黨立場等。

4. **資料來源**：測試資料包括新聞、推文和演講。

### [I] 可推論的主張

1. 對於特定分類任務，微調小模型可能比使用大型 API 更具成本效益。
2. Zero-shot 適合快速原型，生產環境可考慮微調。

---

## Key Data

| 方法 | 適用場景 | 效能 | 成本 |
|------|---------|------|------|
| Zero-shot LLM | 快速原型、少量資料 | 較低 | API 費用 |
| Fine-tuned 小模型 | 生產環境、大量資料 | 較高 | 訓練 + 推論 |

---

## Where to Use

- [[分類與路由_Classification-Routing]] - 能力卡（方法選擇）
