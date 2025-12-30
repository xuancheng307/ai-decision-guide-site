---
id: RAG_Lewis2020
type: evidence
title: "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [RAG, retrieval, generation, NLP, NeurIPS]
source_type: paper
evidence_level: E3
---

# RAG: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

## Citation

**標題**: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks
**作者**: Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, Naman Goyal, Heinrich Küttler, Mike Lewis, Wen-tau Yih, Tim Rocktäschel, Sebastian Riedel, Douwe Kiela
**發表**: NeurIPS 2020
**arXiv**: [2005.11401](https://arxiv.org/abs/2005.11401)
**PDF**: [arxiv.org/pdf/2005.11401](https://arxiv.org/pdf/2005.11401)
**ACM**: [dl.acm.org/doi/10.5555/3495724.3496517](https://dl.acm.org/doi/abs/10.5555/3495724.3496517)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **RAG 架構定義**：RAG 結合 pre-trained parametric memory（seq2seq 模型）與 non-parametric memory（dense vector index），用於 knowledge-intensive 任務。

2. **RAG 優於純參數模型**：RAG 在 Open Domain QA 任務上達到 SOTA，優於純參數化的 seq2seq 模型和 task-specific retrieve-and-extract 架構。

3. **RAG 生成更具體、多樣、事實性**：相比純參數 baseline，RAG 生成的語言更 specific、diverse、factual。

4. **效率優勢**：截至 2020 年底，數億參數的 RAG 系統已超越 110 億參數的 closed-book LM，展示 hybrid memory 的效率。

5. **術語起源**：「RAG」一詞首次在此論文提出。

### [I] 可推論的主張

1. RAG 架構可泛化到任何需要外部知識的生成任務（不僅限於 QA）。
2. 結合 retrieval 可減少模型對參數記憶的依賴，降低 hallucination 風險。

---

## Limitations（限制與假設）

- 論文使用 Wikipedia 作為知識來源，對其他知識庫的泛化需要驗證
- Dense retriever 需要先做 embedding indexing
- 評測主要在英文 QA 任務上

---

## Where to Use（應連結到）

- [[RAG問答_RAG-QA]] - 能力卡
- [[RAG_企業知識問答_Playbook]] - Playbook
- [[幻覺與可追溯性_Hallucination-Grounding]] - 瓶頸卡

---

## 短評

這是 RAG 的奠基論文，定義了「檢索增強生成」的基本架構。對於理解 RAG 為什麼有效、何時使用是必讀。但需注意論文發表於 2020，當時的模型規模與能力與現在不同。
