---
id: RAGAS_Es2023
type: evidence
title: "RAGAS: Automated Evaluation of Retrieval Augmented Generation"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [RAG, evaluation, metrics, EACL]
source_type: paper
evidence_level: E3
---

# RAGAS: Automated Evaluation of Retrieval Augmented Generation

## Citation

**標題**: RAGAS: Automated Evaluation of Retrieval Augmented Generation
**作者**: Shahul Es, Jithin James, Luis Espinosa Anke, Steven Schockaert
**發表**: EACL 2024 System Demonstrations, pages 150–158
**arXiv**: [2309.15217](https://arxiv.org/abs/2309.15217)
**GitHub**: [github.com/explodinggradients/ragas](https://github.com/explodinggradients/ragas)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **Reference-free 評測**：RAGAS 提供不需要人工標註 ground truth 的 RAG 評測方法。

2. **四個核心指標**：
   - **Context Relevancy**：檢索的 context 是否相關
   - **Context Recall**：是否檢索到所有需要的資訊
   - **Faithfulness**：生成答案是否忠於 context（事實準確性）
   - **Answer Relevancy**：答案是否相關

3. **Faithfulness 計算方式**：正確陳述數 / 總陳述數。

4. **整合支援**：RAGAS 提供與 LlamaIndex、LangChain 的整合。

5. **快速評測週期**：此框架可加速 RAG 架構的評測迭代。

### [I] 可推論的主張

1. RAG 評測需要多維度指標，單一指標不足。
2. Faithfulness 是衡量 hallucination 的代理指標。
3. 自動化評測可減少對人工標註的依賴。

---

## Limitations（限制與假設）

- 指標本身依賴 LLM 作為 judge，可能有偏差
- 特定領域/語言可能需要調整
- Context recall 需要 ground truth 來計算

---

## Where to Use（應連結到）

- [[RAG問答_RAG-QA]] - 能力卡（評測方法）
- [[RAG_企業知識問答_Playbook]] - Playbook（offline 評測）
- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡（faithfulness 指標）

---

## 短評

RAGAS 是目前最主流的 RAG 評測框架之一。四個指標的設計很實用，但需要注意 LLM-as-judge 的局限性。建議搭配人工抽查使用。
