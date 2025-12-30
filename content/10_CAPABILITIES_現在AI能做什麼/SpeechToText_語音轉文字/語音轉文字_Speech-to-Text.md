---
type: capability
title: "語音轉文字（Speech-to-Text / ASR）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [speech-to-text, ASR, transcription, Whisper, audio, voice]
status: stable
evidence_level: E3
---

# 語音轉文字（Speech-to-Text / ASR）

> **一句話**：將語音自動轉換為文字，用於會議記錄、字幕生成、語音輸入等場景。

---

## 基本資訊

| 項目 | 內容 |
|------|------|
| **輸入** | 音訊檔案（WAV/MP3/M4A）或即時音訊串流 |
| **輸出** | 文字稿、時間戳記、說話人標記（可選） |
| **成熟度** | **Production-ready**（主流語言），**Pilot**（小眾語言/專業術語） |
| **最後更新** | 2025-01-XX |

---

## 1. 能力定義（Definition）

**ASR（Automatic Speech Recognition）核心組件**：

| 組件 | 功能 | 說明 |
|------|------|------|
| **Acoustic Model** | 語音特徵識別 | 將聲波轉換為音素 |
| **Language Model** | 語言理解 | 將音素序列轉換為合理的句子 |
| **Diarization** | 說話人識別 | 區分不同說話者 |
| **Punctuation** | 標點符號 | 自動加入標點 |
| **Timestamp** | 時間對齊 | 字幕/搜尋用途 |

[F] OpenAI Whisper 在多語言 ASR 上達到接近人類水準的準確率，支援 99 種語言[^Whisper_Radford2022]。

---

## 2. 能做到的範圍（What it can do now）

### 2.1 表現良好的場景

- [x] 會議/訪談錄音轉文字
- [x] Podcast/影片字幕生成
- [x] 客服通話記錄
- [x] 語音輸入/聽寫
- [x] 語音搜尋
- [x] 即時字幕（串流模式）
- [x] 多語言轉錄

### 2.2 主流模型/服務比較

| 服務/模型 | 提供商 | 優點 | 缺點 | 適用場景 |
|-----------|--------|------|------|---------|
| **Whisper large-v3** | OpenAI | 準確率高、多語言、開源可本地 | 速度較慢 | 品質優先、離線處理 |
| **Whisper API** | OpenAI | 易用、穩定 | 檔案大小限制 25MB | API 整合 |
| **Deepgram** | Deepgram | 快速、即時串流、說話人識別 | 成本 | 即時應用、大量處理 |
| **AssemblyAI** | AssemblyAI | 功能完整、摘要整合 | 成本 | 會議記錄整合 |
| **Google STT** | Google | 企業級、多語言 | 設定複雜 | Google Cloud 環境 |
| **Azure STT** | Microsoft | 企業級、客製化模型 | 設定複雜 | Azure 環境、專業術語 |

### 2.3 準確率參考

| 場景 | WER（Word Error Rate）| 條件 |
|------|----------------------|------|
| **清晰錄音（英文）** | 3-5% | 高品質麥克風、無噪音 |
| **會議錄音（英文）** | 8-15% | 多人、遠場麥克風 |
| **電話品質** | 15-25% | 壓縮音訊、噪音 |
| **中文（普通話）** | 5-10% | 標準口音 |
| **方言/口音重** | 15-30%+ | 依方言而異 |

[F] Whisper large-v3 在 Fleurs 多語言測試集上平均 WER 約 10%，部分語言可達 5% 以下[^Whisper_Radford2022]。

---

## 3. 適合的任務特徵（Good fit）

這個能力適合的任務通常有以下特徵：

- [x] **清晰音訊**：品質良好的錄音
- [x] **主流語言**：英文、中文、日文等主流語言
- [x] **允許後編輯**：可以人工校對
- [x] **通用詞彙**：非高度專業領域
- [x] **批次處理**：非嚴格即時需求

---

## 4. 不適合/高風險（Bad fit / Red flags）

### 4.1 不適合的場景

- [ ] **極高準確率需求**：法律/醫療等需要 100% 準確的場景（需人工校對）
- [ ] **嚴重背景噪音**：工地、餐廳等高噪音環境
- [ ] **高度專業術語**：未經訓練的專業詞彙（醫學、法律術語）
- [ ] **強烈口音/方言**：非標準口音的辨識率較低
- [ ] **多人同時說話**：重疊語音難以辨識

### 4.2 紅旗警訊

- [x] **隱私風險**：語音包含個資、機密資訊
- [x] **合規要求**：某些產業有錄音/轉錄法規要求
- [x] **準確率期待過高**：客戶期待零錯誤

---

## 5. 常用落地模式（Patterns）

| 模式 | 適用情境 | 說明 |
|------|---------|------|
| **批次轉錄** | 會議記錄、Podcast | 上傳檔案，非即時處理 |
| **即時字幕** | 直播、視訊會議 | 串流處理，低延遲 |
| **語音搜尋** | 內容平台 | 轉錄後建立搜尋索引 |
| **說話人分離** | 多人會議 | Diarization + 轉錄 |
| **轉錄 + 摘要** | 會議助理 | STT + LLM 摘要整合 |
| **轉錄 + 翻譯** | 多語言會議 | STT + 翻譯 pipeline |

---

## 6. 常用工具（Tools）

| 層級 | 工具 | 備註 |
|------|------|------|
| **開源模型** | Whisper, faster-whisper | 可本地部署 |
| **API 服務** | OpenAI Whisper API, Deepgram, AssemblyAI | 易整合 |
| **企業方案** | Google STT, Azure STT, AWS Transcribe | 企業級 SLA |
| **整合平台** | Otter.ai, Descript, Fireflies.ai | 會議記錄專用 |

---

## 7. 瓶頸與對策（Bottlenecks & Mitigations）

| 瓶頸 | 症狀 | 緩解策略 |
|------|------|---------|
| **音訊品質差** | WER 高 | 降噪預處理、使用好麥克風 |
| **專業術語錯誤** | 特定詞彙錯誤 | 客製化詞彙表、後處理修正 |
| **說話人混淆** | 無法區分說話者 | 使用 Diarization、分軌錄音 |
| **處理速度** | 大量檔案處理慢 | 並行處理、使用 faster-whisper |
| **成本** | API 費用高 | 本地部署、批次處理 |
| **即時延遲** | 字幕延遲明顯 | 使用串流優化模型 |

---

## 8. 成熟度分級（Maturity）

| 階段 | 定義 | 這個能力的狀態 |
|------|------|---------------|
| **PoC** | 實驗室環境可行 | 容易達成 |
| **Pilot** | 小規模真實環境可行 | 需要評估音訊品質、準確率 |
| **Production** | 大規模穩定運行 | 需要建立校對流程、監控機制 |

**Production 需要**：
- 音訊品質標準定義
- 人工校對流程（依準確率需求）
- 處理 pipeline 監控
- 成本追蹤

---

## 9. 成本估算

### API 定價參考（2025-01）

| 服務 | 定價 | 備註 |
|------|------|------|
| **OpenAI Whisper API** | $0.006/分鐘 | 檔案限制 25MB |
| **Deepgram** | $0.0043-0.0145/分鐘 | 依功能 |
| **AssemblyAI** | $0.00025/秒起 | 約 $0.015/分鐘起 |
| **Google STT** | $0.004-0.009/15 秒 | 依模型 |

### 本地部署（Whisper）

| 項目 | 需求 | 效能 |
|------|------|------|
| **Whisper tiny** | CPU 可跑 | 32x 即時 |
| **Whisper base** | CPU 可跑 | 16x 即時 |
| **Whisper large** | GPU 建議 | 1-2x 即時（GPU）|
| **faster-whisper** | GPU 建議 | 4x 加速 |

---

## 10. 發展預期（Outlook & Watch signals）

### 10.1 觀測訊號

- [ ] **即時準確率提升**：串流模式準確率接近離線
- [ ] **多說話人改善**：重疊語音處理能力
- [ ] **方言支援擴展**：小眾語言/方言模型
- [ ] **端側部署**：手機端高效模型

### 10.2 預期趨勢

| 時間範圍 | 預期變化 | 依據 |
|----------|---------|------|
| 6 個月內 | 更多即時串流優化模型 | [I] 模型輕量化趨勢 |
| 1 年內 | STT + LLM 整合更普及 | [I] 會議助理產品發展 |

---

## 相關連結

- **能力卡**：[[多模態_Multimodal]]、[[翻譯_Translation]]
- **瓶頸卡**：[[延遲與成本_Latency-Cost]]

---

## 參考來源

[^Whisper_Radford2022]: Radford, A. et al. (2022). Robust Speech Recognition via Large-Scale Weak Supervision. OpenAI. https://arxiv.org/abs/2212.04356

[^DOC_OpenAI_Whisper]: OpenAI. Whisper API Documentation. https://platform.openai.com/docs/guides/speech-to-text

[^DOC_Deepgram]: Deepgram Documentation. https://developers.deepgram.com/

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Status | Stable |
| 待補 Evidence | ASR Benchmark 評測論文 |
| 待補 Playbook | 會議記錄自動化 Playbook |
