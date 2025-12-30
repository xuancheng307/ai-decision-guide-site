---
type: reference_index
title: "權威文獻總表 (Master Reference List)"
created: 2025-01-XX
updated: 2025-01-XX
description: "本專案可引用的權威文獻彙整，按主題分類"
---

# 權威文獻總表 (Master Reference List)

> 本文件彙整了 AI 決策型知識庫可引用的權威文獻，優先選擇近期（2024-2025）的學術論文、官方文件及產業報告。

---

## 1. RAG 與檢索增強生成

### 基礎論文

| 標題 | 作者 | 發表 | arXiv/DOI | 備註 |
|------|------|------|-----------|------|
| Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks | Lewis et al. | NeurIPS 2020 | [2005.11401](https://arxiv.org/abs/2005.11401) | RAG 原始論文 |
| Lost in the Middle: How Language Models Use Long Contexts | Liu et al. | TACL 2024 | [2307.03172](https://arxiv.org/abs/2307.03172) | Long context 問題 |
| RAGAS: Automated Evaluation of Retrieval Augmented Generation | Es et al. | EACL 2024 | [2309.15217](https://arxiv.org/abs/2309.15217) | RAG 評測框架 |

### RAG 最新進展（2024-2025）

| 標題 | 作者/來源 | 時間 | arXiv | 重點 |
|------|----------|------|-------|------|
| Retrieval-Augmented Generation for AI-Generated Content: A Survey | Gao et al. | 2024 | [2402.19473](https://arxiv.org/abs/2402.19473) | RAG 綜述 |
| A Survey on RAG Meeting LLMs | Fan et al. | 2024 | [2405.06211](https://arxiv.org/abs/2405.06211) | RAG + LLM 整合 |
| Blended RAG: Improving RAG Accuracy with Semantic Search and Hybrid Query-Based Retrievers | - | 2024 | [2404.07220](https://arxiv.org/abs/2404.07220) | Hybrid Search |
| DAT: Dynamic Alpha Tuning for Hybrid Retrieval in RAG | - | 2025 | [2503.23013](https://arxiv.org/abs/2503.23013) | 動態混合檢索 |

### Chunking 策略

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| Rethinking Chunk Size for Long-Document Retrieval: A Multi-Dataset Analysis | 2025 | [2505.21700](https://arxiv.org/abs/2505.21700) | 最佳 chunk size 研究 |
| Financial Report Chunking for Effective RAG | 2024 | [2402.05131](https://arxiv.org/abs/2402.05131) | 結構化 chunking |
| Mix-of-Granularity: Optimize the Chunking Granularity for RAG | 2024 | [2406.00456](https://arxiv.org/abs/2406.00456) | 動態粒度 |
| ChunkRAG: Novel LLM-Chunk Filtering Method for RAG Systems | 2024 | [2410.19572](https://arxiv.org/abs/2410.19572) | Chunk 過濾 |
| Reconstructing Context: Evaluating Advanced Chunking Strategies for RAG | 2025 | [2504.19754](https://arxiv.org/abs/2504.19754) | Chunking 策略評估 |

### Reranking

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| A Thorough Comparison of Cross-Encoders and LLMs for Reranking SPLADE | 2024 | [2403.10407](https://arxiv.org/abs/2403.10407) | Cross-encoder vs LLM |
| RankRAG: Unifying Context Ranking with Retrieval-Augmented Generation in LLMs | 2024 | [2407.02485](https://arxiv.org/abs/2407.02485) | 統一排序與生成 |
| Drowning in Documents: Consequences of Scaling Reranker Inference | 2024 | [2411.11767](https://arxiv.org/abs/2411.11767) | Reranker 規模效應 |
| SciRerankBench: Benchmarking Rerankers Towards Scientific RAG-LLMs | 2025 | [2508.08742](https://arxiv.org/abs/2508.08742) | 科學領域 reranker |

---

## 2. 幻覺與可信度

### 幻覺調查

| 標題 | 作者 | 發表 | arXiv | 重點 |
|------|------|------|-------|------|
| A Survey on Hallucination in Large Language Models | Huang et al. | ACM TOIS 2024 | [2311.05232](https://arxiv.org/abs/2311.05232) | 幻覺綜述 |
| A Comprehensive Survey of Hallucination in Large Language Models: Causes, Detection, and Mitigation | - | 2024 | [2510.06265](https://arxiv.org/abs/2510.06265) | 幻覺成因與緩解 |
| TruthfulQA: Measuring How Models Mimic Human Falsehoods | Lin et al. | ACL 2022 | [2109.07958](https://arxiv.org/abs/2109.07958) | Truthfulness 評測 |

### 幻覺檢測（2024-2025）

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| FaithLens: Detecting and Explaining Faithfulness Hallucination | 2024 | [2512.20182](https://arxiv.org/abs/2512.20182) | Faithfulness 檢測 |
| Hallucination Detection in LLMs: Fast and Memory-Efficient Finetuned Models | 2024 | [2409.02976](https://arxiv.org/abs/2409.02976) | 高效檢測 |
| On A Scale From 1 to 5: Quantifying Hallucination in Faithfulness Evaluation | 2024 | [2410.12222](https://arxiv.org/abs/2410.12222) | 量化評估 |
| Lynx: An Open Source Hallucination Evaluation Model | 2024 | [2407.08488](https://arxiv.org/abs/2407.08488) | 開源評估模型 |
| Benchmarking LLM Faithfulness in RAG with Evolving Leaderboards | 2025 | [2505.04847](https://arxiv.org/abs/2505.04847) | RAG Faithfulness |

### 緩解策略

| 標題 | 作者 | 發表 | arXiv | 重點 |
|------|------|------|-------|------|
| Self-Consistency Improves Chain of Thought Reasoning | Wang et al. | ICLR 2023 | [2203.11171](https://arxiv.org/abs/2203.11171) | Self-consistency |

---

## 3. 文字分類

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| Fine-Tuned 'Small' LLMs (Still) Significantly Outperform Zero-Shot Generative AI Models in Text Classification | 2024 | [2406.08660](https://arxiv.org/abs/2406.08660) | Fine-tune vs Zero-shot |
| Large Language Models Are Zero-Shot Text Classifiers | 2023 | [2312.01044](https://arxiv.org/abs/2312.01044) | Zero-shot 分類 |
| Small Language Models are Good Too: An Empirical Study of Zero-Shot Classification | 2024 | [2404.11122](https://arxiv.org/abs/2404.11122) | 小模型效能 |
| Logistic Regression Makes Small LLMs Strong "Tens-of-Shot" Classifiers | 2024 | [2408.03414](https://arxiv.org/abs/2408.03414) | 高效分類方法 |

---

## 4. 資訊抽取與 NER

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| GPT-NER: Named Entity Recognition via Large Language Models | 2023 | [2304.10428](https://arxiv.org/abs/2304.10428) | LLM NER |
| Recent Advances in Named Entity Recognition: A Comprehensive Survey | 2024 | [2401.10825](https://arxiv.org/abs/2401.10825) | NER 綜述 |
| Financial Named Entity Recognition: How Far Can LLM Go? | 2025 | [2501.02237](https://arxiv.org/abs/2501.02237) | 金融 NER |
| LinkNER: Linking Local NER Models to LLMs using Uncertainty | 2024 | [2402.10573](https://arxiv.org/abs/2402.10573) | 混合 NER |

### 文件理解

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| LayoutLMv3: Pre-training for Document AI with Unified Text and Image Masking | 2022 | [2204.08387](https://arxiv.org/abs/2204.08387) | Document AI 基礎 |
| LayoutLLM: Large Language Model Instruction Tuning for Visually Rich Document Understanding | 2024 | [2403.14252](https://arxiv.org/abs/2403.14252) | LayoutLLM |

---

## 5. 摘要生成

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| An Empirical Comparison of Text Summarization: Multi-Dimensional Evaluation of LLMs | 2025 | [2504.04534](https://arxiv.org/abs/2504.04534) | 多維度評估 |
| Towards Multi-dimensional Evaluation of LLM Summarization across Domains and Languages | 2025 | [2506.00549](https://arxiv.org/abs/2506.00549) | 跨領域評估 |
| Zero-shot Factual Consistency Evaluation Across Domains | 2024 | [2408.04114](https://arxiv.org/abs/2408.04114) | 事實一致性 |
| SummExecEdit: A Factual Consistency Benchmark in Summarization | 2024 | [2412.13378](https://arxiv.org/abs/2412.13378) | 摘要 benchmark |
| Factual Consistency Evaluation of Summarization in the Era of LLMs | 2024 | [2402.13758](https://arxiv.org/abs/2402.13758) | LLM 摘要評估 |

---

## 6. AI Agent 與工具使用

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| AFlow: Automating Agentic Workflow Generation | 2024 | [2410.10762](https://arxiv.org/abs/2410.10762) | 工作流自動化 |
| A Survey on LLM-Based Agentic Workflows and LLM-Profiled Components | 2024 | [2406.05804](https://arxiv.org/abs/2406.05804) | Agent 工作流綜述 |
| ARTIST: Agentic Reasoning and Tool Integration for LLMs via RL | 2025 | [2505.01441](https://arxiv.org/abs/2505.01441) | 工具整合 RL |
| Dynamic Tool Dependency Retrieval for Efficient Function Calling | 2024 | [2512.17052](https://arxiv.org/abs/2512.17052) | 高效 function calling |
| Agentic AI: A Comprehensive Survey of Architectures, Applications | 2025 | [2510.25445](https://arxiv.org/abs/2510.25445) | Agent AI 綜述 |
| AgentArch: A Comprehensive Benchmark to Evaluate Agent Architectures | 2025 | [2509.10769](https://arxiv.org/abs/2509.10769) | Agent 評測 |

---

## 7. 安全性與 Prompt Injection

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| Prompt Injection attack against LLM-integrated Applications (HouYi) | 2023 | [2306.05499](https://arxiv.org/abs/2306.05499) | Prompt injection 攻擊 |
| Benchmarking and Defending Against Indirect Prompt Injection Attacks | 2023 | [2312.14197](https://arxiv.org/abs/2312.14197) | 間接注入防禦 |
| Defense Against Prompt Injection Attack by Leveraging Attack Techniques | 2024 | [2411.00459](https://arxiv.org/abs/2411.00459) | 防禦策略 |
| Defending Against Prompt Injection With Defensive Tokens | 2025 | [2507.07974](https://arxiv.org/abs/2507.07974) | Defensive Tokens |
| A Multi-Agent LLM Defense Pipeline Against Prompt Injection | 2025 | [2509.14285](https://arxiv.org/abs/2509.14285) | 多 Agent 防禦 |
| Automatic and Universal Prompt Injection Attacks against LLMs | 2024 | [2403.04957](https://arxiv.org/abs/2403.04957) | 自動化攻擊 |

---

## 8. Long Context 評測

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| ∞Bench: Extending Long Context Evaluation Beyond 100K Tokens | 2024 | [2402.13718](https://arxiv.org/abs/2402.13718) | 100K+ 評測 |
| LongBench v2 | 2024 | [2412.15204](https://arxiv.org/abs/2412.15204) | 長文本理解 |
| ChatQA 2: Bridging the Gap to Proprietary LLMs in Long Context and RAG | 2024 | [2407.14482](https://arxiv.org/abs/2407.14482) | Long context + RAG |
| LV-Eval | 2024 | [2402.05136](https://arxiv.org/abs/2402.05136) | 256k 評測 |

---

## 9. Embedding 模型

### 資源連結

| 名稱 | 類型 | 連結 | 說明 |
|------|------|------|------|
| MTEB Leaderboard | Benchmark | [huggingface.co/spaces/mteb/leaderboard](https://huggingface.co/spaces/mteb/leaderboard) | Embedding 模型排行榜 |
| Sentence Transformers | Library | [github.com/huggingface/sentence-transformers](https://github.com/huggingface/sentence-transformers) | Embedding 模型庫 |
| MTEB GitHub | Benchmark | [github.com/embeddings-benchmark/mteb](https://github.com/embeddings-benchmark/mteb) | 評測框架 |

### 相關論文

| 標題 | 時間 | arXiv | 重點 |
|------|------|-------|------|
| Recent Advances in Text Embedding: A Comprehensive Review of Top-Performing Methods on MTEB | 2024 | [2406.01607](https://arxiv.org/abs/2406.01607) | Embedding 綜述 |

---

## 10. 向量資料庫

### 比較資源

| 資料庫 | 類型 | 特點 | 適用場景 |
|--------|------|------|---------|
| **Pinecone** | Managed | 低延遲、無運維 | 快速部署、中小規模 |
| **Milvus** | Open-source | 11 種索引、高 throughput | 大規模、需彈性配置 |
| **Weaviate** | Open-source | 原生 hybrid search | 需混合檢索 |
| **Qdrant** | Open-source | 高效能、Rust 實作 | 效能優先 |
| **Chroma** | Open-source | 輕量、易上手 | PoC、小規模 |

### 效能參考

- Milvus/Zilliz: <10ms p50 latency (768-dim)
- Pinecone: 20-50ms latency
- Milvus supports 11 index types (最多)
- Weaviate: 原生 hybrid search 最佳

---

## 11. 官方文件

### API 文件

| 廠商 | 文件 | 重點功能 |
|------|------|---------|
| **OpenAI** | [platform.openai.com/docs](https://platform.openai.com/docs) | Structured Outputs, Function Calling |
| **Anthropic** | [docs.anthropic.com](https://docs.anthropic.com) | Prompt Caching, Tool Use, Citations |
| **Google** | [ai.google.dev](https://ai.google.dev) | Gemini API |

### 工具框架

| 工具 | 文件 | 用途 |
|------|------|------|
| **LangChain** | [docs.langchain.com](https://docs.langchain.com) | LLM 編排 |
| **LlamaIndex** | [docs.llamaindex.ai](https://docs.llamaindex.ai) | RAG 框架 |
| **RAGAS** | [docs.ragas.io](https://docs.ragas.io) | RAG 評測 |
| **DeepEval** | [docs.confident-ai.com](https://docs.confident-ai.com) | LLM 評測 |

---

## 12. 產業報告與統計

### McKinsey

| 報告 | 時間 | 關鍵數據 |
|------|------|---------|
| The State of AI in 2024 | 2024 | 65% 組織使用 GenAI（較 10 個月前翻倍） |
| The State of AI in 2025 | 2025 | 78% 組織至少在一個功能使用 AI |
| AI Adoption | 2024 | 72% 採用率（過去六年約 50%） |

### Gartner

| 統計 | 數據 |
|------|------|
| GenAI 部署 | No.1 AI 解決方案類型 |
| AI 成熟組織 | 9% |
| 2028 Agentic AI | 33% 企業軟體將包含 Agentic AI |
| CEO 認為 AI 重要 | 74%（2023 年 59%） |
| AI 採用障礙 | 49% 難以估算 AI 價值 |

### 投資數據

| 指標 | 數據 |
|------|------|
| 2024 企業 AI 投資 | $252.3B |
| 私人投資年增 | 44.5% |
| 2025 全球 AI 支出預測 | $1.5T |

---

## 13. 客服 AI 案例

| 公司 | 成效 | 來源 |
|------|------|------|
| **Klarna** | 相當於 700 FTE、$40M 利潤提升、2 分鐘解決（原 11 分鐘）、25% 重複詢問減少 | Industry Report |
| **Verizon** | 銷售提升 40%、95% 查詢可回答 | Industry Report |
| **Solo Brands** | 75% 客戶互動解決率（原 40%） | Gartner Case Study |
| **H&M** | 70% 查詢無需人工 | Research Paper |
| **ING** | 85,000 週查詢量、GenAI 試點 | McKinsey Case |

---

## 14. 法規與合規

### EU AI Act

| 項目 | 內容 |
|------|------|
| 正式名稱 | Regulation (EU) 2024/1689 |
| 生效日期 | 2024 年 8 月 1 日 |
| 禁止 AI 截止 | 2025 年 2 月 2 日 |
| GPAI 規則生效 | 2025 年 8 月 2 日 |
| 高風險 AI 全面適用 | 2026 年 8 月 2 日 |

### 與 GDPR 關係

- AI Act 不取代 GDPR，而是補充
- 資料處理仍需遵守 GDPR
- 兩者有顯著重疊（資料保護原則）

---

## 使用說明

1. **引用格式**：使用 footnote 格式，如 `[^rag-lewis]`
2. **Evidence Level**：
   - E3：學術論文、官方文件
   - E2：產業報告、Benchmark
   - E1：技術部落格
3. **連結到內容**：從此清單複製 citation 到能力卡、Playbook 等

---

*最後更新：2025-01-XX*
