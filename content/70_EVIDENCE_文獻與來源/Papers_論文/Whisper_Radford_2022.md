---
id: Whisper_Radford2022
type: evidence
title: "Robust Speech Recognition via Large-Scale Weak Supervision"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [speech-recognition, ASR, Whisper, multilingual, OpenAI]
source_type: paper
evidence_level: E3
---

# Robust Speech Recognition via Large-Scale Weak Supervision

## Citation

Radford, A., Kim, J.W., Xu, T., Brockman, G., McLeavey, C., & Sutskever, I. (2022). Robust Speech Recognition via Large-Scale Weak Supervision. OpenAI Technical Report.

**arXiv**: https://arxiv.org/abs/2212.04356

---

## Key Findings

### 1. 大規模弱監督訓練

[F] Whisper 使用 680,000 小時的多語言和多任務監督資料進行訓練，涵蓋語音識別、語音翻譯、語言識別和語音活動偵測任務。

### 2. 多語言覆蓋

[F] Whisper 支援 99 種語言的語音識別，其中約 三分之一 的語言在測試集上達到低於 10% 的 Word Error Rate（WER）。

### 3. 零樣本泛化

[F] Whisper 在未見過的資料集上展現強大的零樣本泛化能力，無需特定領域微調即可達到接近專門訓練模型的效能。

### 4. 魯棒性

[F] 相比傳統 ASR 模型，Whisper 對噪音、口音和錄音品質變化更具魯棒性。

---

## 模型規格

| 模型版本 | 參數量 | VRAM 需求 | 相對速度 |
|----------|--------|-----------|----------|
| tiny | 39M | ~1 GB | ~32x |
| base | 74M | ~1 GB | ~16x |
| small | 244M | ~2 GB | ~6x |
| medium | 769M | ~5 GB | ~2x |
| large | 1550M | ~10 GB | 1x |
| large-v2 | 1550M | ~10 GB | 1x |
| large-v3 | 1550M | ~10 GB | 1x |

---

## 效能數據

### 英語 LibriSpeech 測試

| 模型 | test-clean WER | test-other WER |
|------|----------------|----------------|
| Whisper large-v3 | 2.0% | 3.9% |
| 人類水準 | 5.8% | 12.6% |

### 多語言 Fleurs 測試

| 語言類別 | 平均 WER |
|----------|----------|
| 高資源語言（英、中、西等） | 5-10% |
| 中資源語言 | 10-20% |
| 低資源語言 | 20-40%+ |

---

## Limitations（原論文聲明）

1. **即時處理**：原始模型設計為離線處理，非優化於即時串流
2. **低資源語言**：部分低資源語言效能仍有限
3. **長音訊**：超過 30 秒的音訊需要分段處理
4. **背景噪音**：極端噪音環境下效能下降

---

## 後續發展

- **Whisper large-v3**（2023）：進一步提升多語言效能
- **faster-whisper**：社群開發的加速版本，速度提升 4 倍
- **whisper.cpp**：C++ 移植版本，支援更多平台

---

## 應用於知識庫

此 Evidence 支援以下主張：

| Claim ID | 主張 |
|----------|------|
| STT-F01 | Whisper 在多語言 ASR 上達到接近人類水準 |
| STT-F02 | Whisper 支援 99 種語言 |
| STT-F03 | Whisper large-v3 在 Fleurs 多語言測試集上平均 WER 約 10% |

---

## 原文連結

- **arXiv**: https://arxiv.org/abs/2212.04356
- **OpenAI Blog**: https://openai.com/research/whisper
- **GitHub**: https://github.com/openai/whisper

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Evidence Level | E3（同儕審查） |
| 驗證日期 | 2025-01-XX |
