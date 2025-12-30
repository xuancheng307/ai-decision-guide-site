---
id: LostInMiddle_Liu2023
type: evidence
title: "Lost in the Middle: How Language Models Use Long Contexts"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [long-context, LLM, retrieval, attention, TACL]
source_type: paper
evidence_level: E3
---

# Lost in the Middle: How Language Models Use Long Contexts

## Citation

**標題**: Lost in the Middle: How Language Models Use Long Contexts
**作者**: Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, Percy Liang
**發表**: Transactions of the Association for Computational Linguistics (TACL), Volume 12, pages 157–173, 2024
**arXiv**: [2307.03172](https://arxiv.org/abs/2307.03172)
**ACL Anthology**: [aclanthology.org/2024.tacl-1.9](https://aclanthology.org/2024.tacl-1.9/)
**GitHub**: [github.com/nelson-liu/lost-in-the-middle](https://github.com/nelson-liu/lost-in-the-middle)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **U 型效能曲線**：LLM 在處理長 context 時，對「開頭」和「結尾」的資訊表現最好，「中間」的資訊效能顯著下降（U-shaped curve）。

2. **長 context 不等於好效能**：即使模型支援長 context window，效能仍會隨 context 長度增加而下降。

3. **位置敏感性**：改變相關資訊在 context 中的位置會顯著影響模型表現，表明模型無法穩定利用長 context 中的資訊。

4. **評測任務**：論文評測了 multi-document QA 和 key-value retrieval 兩個任務。

### [I] 可推論的主張

1. RAG 系統的 retrieval 結果排序很重要——相關文件應放在 context 開頭或結尾。
2. 長文件摘要任務可能遺漏中間段落的重要資訊。
3. Context window 大不代表可以無腦塞入大量資料。

---

## Limitations（限制與假設）

- 主要評測英文 QA 和 key-value retrieval，其他任務需要驗證
- 論文發表於 2023，新模型可能有改進
- 不同模型的 U 型曲線程度不同

---

## Where to Use（應連結到）

- [[文件摘要_Summarization]] - 能力卡（長文件摘要限制）
- [[RAG問答_RAG-QA]] - 能力卡（retrieval 排序影響）
- [[RAG_企業知識問答_Playbook]] - Playbook（架構設計考量）

---

## 短評

這篇論文揭示了 long-context LLM 的重要限制。對於設計 RAG 系統和長文件處理非常關鍵。需要持續關注新模型是否改善此問題。
