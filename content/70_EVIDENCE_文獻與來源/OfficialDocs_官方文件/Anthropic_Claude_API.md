---
id: API_Anthropic_Claude
type: evidence
title: "Anthropic Claude API Documentation"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [Anthropic, Claude, API]
source_type: official_doc
evidence_level: E3
---

# Anthropic Claude API Documentation

## Citation

**來源**: Anthropic 官方
**主文檔**: [docs.claude.com](https://docs.claude.com/)
**API Overview**: [console.anthropic.com/docs/en/api/overview](https://console.anthropic.com/docs/en/api/overview)
**開發者平台**: [anthropic.com/api](https://www.anthropic.com/api)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **API 端點**：RESTful API 在 `https://api.anthropic.com`，主要使用 Messages API（POST /v1/messages）。

2. **功能支援**：
   - Prompt caching（降低延遲 80%、成本 90%）
   - Extended thinking
   - Streaming
   - Batch processing
   - Citations（引用）
   - Vision（視覺）
   - PDF 支援
   - Tool use

3. **SDK 支援**：Python 3.7+ 和 TypeScript 4.5+。

4. **最新模型**：Claude Sonnet 4.5（complex agents 和 coding 最佳）。

5. **新工具**：bash_20250124、text_editor_20250124（不需要 beta header）。

### [I] 可推論的主張

1. Claude API 功能與 OpenAI 相近，可作為替代方案。
2. Prompt caching 對高頻 RAG 應用有顯著成本優勢。

---

## Limitations（限制與假設）

- 某些功能在 beta 階段
- 地區可用性可能有限制

---

## Where to Use（應連結到）

- [[RAG問答_RAG-QA]] - 能力卡（模型選項）
- [[RAG_企業知識問答_Playbook]] - Playbook（工具選型）

---

## 短評

Anthropic Claude API 是主要的 LLM API 選項之一。Prompt caching 功能對降低成本很有價值。Tool use 和 Vision 支援使其適合複雜應用。
