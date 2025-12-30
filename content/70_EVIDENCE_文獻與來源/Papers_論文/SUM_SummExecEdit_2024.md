---
id: SUM_SummExecEdit2024
type: evidence
title: "SummExecEdit: A Factual Consistency Benchmark in Summarization"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [summarization, benchmark, factual-consistency]
source_type: paper
evidence_level: E3
---

# SummExecEdit: A Factual Consistency Benchmark in Summarization with Executable Edits

## Citation

**標題**: SummExecEdit: A Factual Consistency Benchmark in Summarization with Executable Edits
**arXiv**: [2412.13378](https://arxiv.org/abs/2412.13378)
**時間**: December 2024

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **最佳模型表現**：在 SummExecEdit 上表現最佳的 Claude 3.5 Sonnet 準確率僅約 73%。

2. **挑戰性 Benchmark**：此 benchmark 具有挑戰性，多數 LLM 難以檢測事實錯誤。

3. **LLM 檢測困難**：整體檢測結果顯示許多 LLM 在檢測事實錯誤上仍有困難。

### [I] 可推論的主張

1. 即使是最先進的 LLM，事實錯誤檢測仍是挑戰。
2. 生產環境需要人工覆核機制。

---

## Key Data

| 模型 | SummExecEdit 準確率 |
|------|-------------------|
| Claude 3.5 Sonnet | ~73% |
| 其他 LLM | < 73% |

---

## Where to Use

- [[文件摘要_Summarization]] - 能力卡（表現數據）
- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡
