---
id: API_OpenAI_StructuredOutputs
type: evidence
title: "OpenAI Structured Outputs / JSON Mode"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [OpenAI, API, JSON, structured-outputs]
source_type: official_doc
evidence_level: E3
---

# OpenAI Structured Outputs / JSON Mode

## Citation

**來源**: OpenAI 官方文檔
**文檔**: [Structured Outputs Guide](https://platform.openai.com/docs/guides/structured-outputs)
**公告**: [Introducing Structured Outputs](https://openai.com/index/introducing-structured-outputs-in-the-api/)
**Cookbook**: [Introduction to Structured Outputs](https://cookbook.openai.com/examples/structured_outputs_intro)

---

## Supports Claims（可引用的主張）

### [F] 可直接引用的事實

1. **功能定義**：Structured Outputs 確保模型輸出嚴格符合開發者提供的 JSON Schema。

2. **效能數據**：
   - gpt-4o-2024-08-06 + Structured Outputs: 100% schema 遵循率
   - gpt-4-0613: < 40% schema 遵循率

3. **支援模型**：gpt-4o-mini、gpt-4o-mini-2024-07-18、gpt-4o-2024-08-06 及更新版本。

4. **兩種使用方式**：
   - Function calling 中設定 `strict: true`
   - response_format 設定 `json_schema`

5. **SDK 支援**：Python（Pydantic）和 TypeScript（Zod）原生支援。

6. **限制**：可能因 max_tokens 或安全拒絕而不完整。

7. **官方建議**：優先使用 Structured Outputs 而非舊版 JSON Mode。

### [I] 可推論的主張

1. 結構化輸出可大幅提升資訊抽取任務的可靠性。
2. 可用於強制輸出格式，減少後處理錯誤。

---

## Limitations（限制與假設）

- 僅支援特定模型版本
- 複雜 schema 可能增加延遲
- 安全過濾可能導致拒絕回應

---

## Where to Use（應連結到）

- [[文件抽取_Information-Extraction]] - 能力卡
- [[文件抽取_OCR_Playbook]] - Playbook

---

## 短評

Structured Outputs 是資訊抽取和結構化任務的重要功能。100% schema 遵循率使其非常適合 production 使用。注意模型版本限制。
