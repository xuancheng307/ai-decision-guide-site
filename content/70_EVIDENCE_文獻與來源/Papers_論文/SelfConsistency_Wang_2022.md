---
id: SelfConsistency_Wang2022
type: evidence
title: "Self-Consistency Improves Chain of Thought Reasoning"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [reasoning, CoT, self-consistency, ICLR]
source_type: paper
evidence_level: E3
---

# Self-Consistency Improves Chain of Thought Reasoning in Language Models

## Citation

**標題**: Self-Consistency Improves Chain of Thought Reasoning in Language Models
**作者**: Xuezhi Wang, Jason Wei, Dale Schuurmans, Quoc Le, Ed Chi, Sharan Narang, Aakanksha Chowdhery, Denny Zhou
**發表**: ICLR 2023
**arXiv**: [2203.11171](https://arxiv.org/abs/2203.11171)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **方法定義**：Self-consistency 透過 sampling 多條 reasoning paths，選擇最一致的答案（majority voting）。

2. **效能提升**：相比 greedy decoding 的 CoT prompting，self-consistency 在多個 benchmark 上顯著提升：
   - GSM8K: +17.9%
   - SVAMP: +11.0%
   - AQuA: +12.2%
   - StrategyQA: +6.4%
   - ARC-challenge: +3.9%

3. **模型泛化**：在 UL2-20B、GPT-3-175B、LaMDA-137B、PaLM-540B 四個模型上都有效。

4. **核心直覺**：複雜推理問題通常有多種正確推理路徑，正確答案會更「一致」。

### [I] 可推論的主張

1. 增加推理多樣性可以提升可靠性。
2. 類似的 ensemble 策略可用於提升 LLM 輸出的穩定性。

---

## Limitations（限制與假設）

- 需要多次 API call，成本增加
- 主要在 reasoning 任務上驗證，其他任務效果需驗證

---

## Where to Use（應連結到）

- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡（緩解策略）
- [[分類與路由_Classification-Routing]] - 能力卡（提升可靠性）

---

## 短評

Self-consistency 是一個簡單但有效的策略，透過多次 sampling 和投票來提升 LLM 輸出可靠性。對於重要決策可考慮使用，但需平衡成本。
