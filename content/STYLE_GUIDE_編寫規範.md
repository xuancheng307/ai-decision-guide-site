---
type: meta
title: "知識庫編寫規範 (Style Guide)"
created: 2025-01-XX
updated: 2025-01-XX
---

# 知識庫編寫規範 (Style Guide)

> 本文件定義 AI 決策型知識庫的編寫規則，確保內容一致性與可驗證性。

---

## 1. 引用規則（Citation Rules）

### 1.1 核心原則

**所有 footnote 必須指向 Evidence Note**

```
❌ 錯誤：直接貼外部 URL
[^1]: https://arxiv.org/abs/2005.11401

✅ 正確：指向 Evidence Note
[^RAG_Lewis2020]: 參見 [[RAG_Lewis_2020]]
```

### 1.2 Footnote Key 命名規則

Footnote key 必須等於對應 Evidence Note 的 YAML `id` 欄位。

**格式**：`TOPIC_AuthorYear` 或 `TOPIC_KeyNameYear`

| 類型 | 格式 | 範例 |
|------|------|------|
| 論文 | `TOPIC_Author年份` | `RAG_Lewis2020`, `SUM_ROUGE2004` |
| 官方文件 | `TOPIC_公司_功能` | `API_OpenAI_StructuredOutputs` |
| Benchmark | `BENCH_名稱年份` | `BENCH_MTEB2024`, `BENCH_TruthfulQA2022` |
| 產業報告 | `RPT_來源_年份` | `RPT_McKinsey_AI2024` |

### 1.3 引用流程

```
1. 找到/建立 Evidence Note
2. 確認 Evidence Note 有 id 欄位
3. 內容中使用 [^id] 引用
4. 文末補上 footnote 定義
```

**範例**：

```markdown
<!-- 內容中 -->
RAG 結合 pre-trained parametric memory 與 non-parametric memory[^RAG_Lewis2020]。

<!-- 文末 -->
[^RAG_Lewis2020]: Lewis, P. et al. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. 參見 [[RAG_Lewis_2020]]
```

### 1.4 找不到文獻時

如果暫時找不到合適的 Evidence Note：

```markdown
這個方法可以提升 10-15% 效能[TODO: evidence]。
```

**禁止**：杜撰引用、編造數據、使用未驗證來源。

---

## 2. 主張標記（Claim Tagging）

所有主張必須標記來源類型：

| 標記 | 含義 | 引用要求 |
|------|------|---------|
| `[F]` | **Fact** - 可直接引用的事實 | 必須引用 E3/E2 來源 |
| `[I]` | **Inference** - 合理推論 | 需說明推論依據 |
| `[H]` | **Heuristic** - 經驗法則 | 標明來源（團隊經驗/社群共識） |

**範例**：

```markdown
[F] RAG 相比純 LLM 可生成更 factual 的回答[^RAG_Lewis2020]。

[I] 基於上述數據，RAG 適合知識密集型任務（推論依據：Lewis 2020 的實驗結果）。

[H] 實務上建議 chunk size 設為 512 tokens（經驗法則，需根據資料調整）。
```

---

## 3. Evidence Level 定義

| Level | 定義 | 範例 |
|-------|------|------|
| **E4** | 內部測試/自有數據 | 公司 A/B 測試結果 |
| **E3** | 學術論文（peer-reviewed）、官方文件 | NeurIPS 論文、OpenAI 官方文件 |
| **E2** | 產業報告、公開 Benchmark | McKinsey 報告、MTEB Leaderboard |
| **E1** | 技術部落格、專家文章 | 知名工程師的技術文章 |
| **E0** | 社群討論、未驗證來源 | Reddit、Twitter 討論 |

**引用要求**：

| 文件類型 | 最低 E3 引用數 | 總引用數 |
|----------|---------------|---------|
| 能力卡 | 6 | 8+ |
| Playbook | 5 | 8+ |
| 瓶頸卡 | 3 | 6+ |
| Domain Pack | 3 | 5+ |
| 工具卡 | 2（官方文件） | 4+ |

---

## 4. YAML Frontmatter 規範

### 4.1 必填欄位

所有內容文件必須包含：

```yaml
---
type: capability | playbook | bottleneck | domain_pack | tool | evidence
title: "文件標題"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [tag1, tag2]
status: draft | stable | deprecated
---
```

### 4.2 Evidence Note 額外必填

```yaml
---
id: "TOPIC_AuthorYear"  # 必填！用於 footnote 對應
source_type: paper | official_doc | benchmark | industry_report | blog
evidence_level: E3 | E2 | E1 | E0
---
```

---

## 5. 連結規範

### 5.1 內部連結

使用 Wiki-style 連結：

```markdown
參見 [[RAG問答_RAG-QA]]
詳見 [[幻覺與可追溯性_Hallucination-Grounding]]
```

### 5.2 連結目標

- 連結必須指向存在的檔案
- 使用檔名（不含副檔名）
- 區分大小寫

---

## 6. 命名規範

### 6.1 檔案命名

| 類型 | 格式 | 範例 |
|------|------|------|
| 能力卡 | `中文名_English-Name.md` | `RAG問答_RAG-QA.md` |
| Playbook | `主題_Playbook.md` | `RAG_企業知識問答_Playbook.md` |
| 瓶頸卡 | `中文名_English-Name.md` | `幻覺與可追溯性_Hallucination-Grounding.md` |
| Domain Pack | `SME_領域_場景.md` | `SME_中小企業通用_客服與工單.md` |
| Evidence Note | `TOPIC_Author_Year.md` | `RAG_Lewis_2020.md` |

### 6.2 術語一致性

所有術語以 `00_START_HERE/Glossary_名詞表.md` 為準。

常見術語標準寫法：

| 統一用語 | 避免使用 |
|----------|---------|
| RAG | Retrieval Augmented Generation, 檢索增強生成 |
| LLM | Large Language Model, 大型語言模型 |
| Embedding | 嵌入, 向量化 |
| Hallucination | 幻覺 |
| Chunk | 分塊, 切片 |
| Reranker | 重排序器 |

---

## 7. 能力卡特殊規範

### 7.1 表現數據結構（三段式）

```markdown
## 表現程度

### Metrics（評測指標）
| 指標 | 定義 | 適用場景 |
|------|------|---------|
| Faithfulness | 答案與 context 的一致性 | RAG 評測 |
| ...

### Public Benchmarks（公開基準）
| Benchmark | 典型範圍 | 來源 |
|-----------|---------|------|
| RAGAS Faithfulness | 70-90% | [^RAGAS_2023] |
| ...

### Domain Baseline Plan（本域基準計畫）
建議使用者：
1. 準備 100+ 測試問答對
2. 使用 [評測工具] 計算 baseline
3. 記錄到 E4 Evidence Note
```

---

## 8. QA 檢查清單

發布前必須確認：

- [ ] 所有 `[^footnote]` 有對應的 Evidence Note
- [ ] 所有 `[[wiki-link]]` 指向存在的檔案
- [ ] YAML frontmatter 必填欄位完整
- [ ] Evidence Level 標記正確
- [ ] 無 `[TODO: evidence]` 殘留（或已標記為已知缺口）
- [ ] 術語與 Glossary 一致

---

## 9. 版本控制

- 每次重大更新需更新 `updated` 日期
- 每次驗證連結/數據有效需更新 `last_verified` 日期
- 過時內容標記 `status: deprecated` 而非刪除

---

*最後更新：2025-01-XX*
