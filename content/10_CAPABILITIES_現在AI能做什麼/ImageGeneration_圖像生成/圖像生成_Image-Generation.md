---
type: capability
title: "圖像生成（Image Generation）"
created: 2025-01-XX
updated: 2025-01-XX
last_verified: 2025-01-XX
tags: [image-generation, diffusion, DALL-E, Stable-Diffusion, Midjourney, creative]
status: stable
evidence_level: E3
---

# 圖像生成（Image Generation）

> **一句話**：讓 AI 根據文字描述生成圖像，用於設計、行銷、創意內容等場景。

---

## 基本資訊

| 項目 | 內容 |
|------|------|
| **輸入** | 文字 prompt（描述）、可選：參考圖片、風格參數 |
| **輸出** | 生成的圖像（PNG/JPEG） |
| **成熟度** | **Production-ready**（特定場景），**Pilot**（通用創意） |
| **最後更新** | 2025-01-XX |

---

## 1. 能力定義（Definition）

**圖像生成技術演進**：

| 世代 | 技術 | 代表模型 | 特點 |
|------|------|---------|------|
| **Gen 1** | GAN | StyleGAN | 特定領域（人臉等）表現佳 |
| **Gen 2** | Diffusion | Stable Diffusion, DALL-E 2 | 通用生成、品質大幅提升 |
| **Gen 3** | 進階 Diffusion | DALL-E 3, Midjourney v6, SD XL | 更好的 prompt 理解、細節 |

[F] Diffusion 模型透過逐步去噪過程生成圖像，相比 GAN 更穩定且品質更高[^DOC_Diffusion_Overview]。

---

## 2. 能做到的範圍（What it can do now）

### 2.1 表現良好的場景

- [x] 行銷素材生成（社群圖片、廣告圖）
- [x] 產品概念視覺化（原型設計）
- [x] 風格轉換（照片轉插畫等）
- [x] 圖片編輯（Inpainting、Outpainting）
- [x] 變體生成（基於參考圖生成多個版本）
- [x] 藝術創作輔助

### 2.2 主流模型比較

| 模型 | 提供商 | 優點 | 缺點 | 適用場景 |
|------|--------|------|------|---------|
| **DALL-E 3** | OpenAI | Prompt 理解最佳、API 易用 | 成本較高、風格偏特定 | 商業用途、API 整合 |
| **Midjourney v6** | Midjourney | 藝術品質最高、細節豐富 | 只有 Discord 介面、無 API | 創意設計、高品質需求 |
| **Stable Diffusion XL** | Stability AI | 開源、可本地部署、可控性高 | 需要調參、Prompt 技巧門檻 | 自建系統、隱私需求 |
| **Imagen 3** | Google | 高品質、與 Google 生態整合 | 較新、API 限制 | Google Cloud 用戶 |

### 2.3 生成品質評估維度

| 維度 | 說明 | 評估方式 |
|------|------|---------|
| **Prompt Adherence** | 與描述的符合度 | 人工評分 |
| **Visual Quality** | 視覺品質、細節 | FID、人工評分 |
| **Coherence** | 場景一致性 | 人工評分 |
| **Aesthetic** | 美學品質 | 人工評分 |
| **Artifact-free** | 無明顯瑕疵（畸形、模糊） | 人工檢查 |

---

## 3. 適合的任務特徵（Good fit）

這個能力適合的任務通常有以下特徵：

- [x] **創意輔助非替代**：輔助設計師，不是完全自動化
- [x] **允許迭代**：可以多次生成、挑選、修改
- [x] **非精確需求**：「感覺」比「規格」重要
- [x] **有人工審核**：最終由人確認品質
- [x] **智財風險可控**：已評估版權和商標風險

---

## 4. 不適合/高風險（Bad fit / Red flags）

### 4.1 不適合的場景

- [ ] **精確技術圖**：需要精確尺寸、比例的工程圖
- [ ] **人物肖像（商業用途）**：可能生成不存在的人，有法律風險
- [ ] **品牌 Logo**：難以控制細節，且有版權議題
- [ ] **文字生成**：圖像中的文字常出錯
- [ ] **需要 100% 可控**：無法保證每次生成結果

### 4.2 紅旗警訊

- [x] **版權風險**：訓練資料可能包含受版權保護的作品
- [x] **人物生成**：可能生成真實人物的相似圖像（Deepfake 風險）
- [x] **品牌侵權**：可能生成包含商標的圖像
- [x] **不當內容**：需要內容過濾機制

---

## 5. 常用落地模式（Patterns）

| 模式 | 適用情境 | 說明 |
|------|---------|------|
| **批量變體生成** | 行銷素材 | 一個概念生成多個版本，人工挑選 |
| **風格遷移** | 品牌一致性 | 統一風格參數，批量處理 |
| **Inpainting 編輯** | 圖片修改 | 保留部分、重新生成指定區域 |
| **參考圖生成** | 概念延伸 | 基於參考圖生成相似風格 |
| **ControlNet 控制** | 精確構圖 | 使用骨架、深度圖控制生成 |

---

## 6. 常用工具（Tools）

| 層級 | 工具 | 備註 |
|------|------|------|
| **API 服務** | OpenAI DALL-E 3, Stability AI | 最易整合 |
| **平台** | Midjourney, Leonardo.ai, Runway | 創意工作流 |
| **本地部署** | Stable Diffusion + ComfyUI/A1111 | 高可控、隱私 |
| **企業方案** | Adobe Firefly, Canva AI | 整合設計工具 |

---

## 7. 瓶頸與對策（Bottlenecks & Mitigations）

| 瓶頸 | 症狀 | 緩解策略 |
|------|------|---------|
| **Prompt 技巧** | 生成結果不符預期 | 使用 prompt 模板、負向 prompt |
| **一致性問題** | 多張圖風格不一致 | 使用 seed、固定風格參數 |
| **細節控制** | 難以精確控制構圖 | ControlNet、Inpainting |
| **生成時間** | 高解析度生成慢 | 先低解析度、再 upscale |
| **版權風險** | 智財權議題 | 使用商業授權模型、記錄 prompt |

---

## 8. 成熟度分級（Maturity）

| 階段 | 定義 | 這個能力的狀態 |
|------|------|---------------|
| **PoC** | 實驗室環境可行 | 容易達成 |
| **Pilot** | 小規模真實環境可行 | 需要建立審核流程 |
| **Production** | 大規模穩定運行 | 需要完整的品質管控、版權管理 |

**Production 需要**：
- 人工審核流程
- 版權和智財權政策
- 內容過濾機制
- 品牌一致性指南

---

## 9. 成本估算

### API 定價參考（2025-01）

| 服務 | 定價 | 備註 |
|------|------|------|
| **DALL-E 3** | ~$0.04-0.08/張 | 依解析度 |
| **Stability AI** | ~$0.01-0.03/張 | 依模型 |
| **Midjourney** | $10-60/月訂閱 | 依用量 |

### 本地部署成本

| 項目 | 需求 | 成本 |
|------|------|------|
| **GPU** | RTX 3090/4090 或 A100 | $1,500-15,000 |
| **VRAM** | 12GB+ | - |
| **儲存** | 模型 5-10GB | - |

---

## 10. 發展預期（Outlook & Watch signals）

### 10.1 觀測訊號

- [ ] **影片生成成熟**：Sora、Runway Gen-3 等影片生成普及
- [ ] **一致性改善**：多張圖的角色/風格一致性
- [ ] **3D 生成**：2D 到 3D 的突破
- [ ] **即時生成**：延遲降到可即時互動

### 10.2 預期趨勢

| 時間範圍 | 預期變化 | 依據 |
|----------|---------|------|
| 6 個月內 | 影片生成 API 更普及 | [I] Sora 等模型發展 |
| 1 年內 | 細節控制能力大幅提升 | [I] ControlNet 等技術發展 |

---

## 相關連結

- **Playbooks**：[TODO: 行銷素材生成 Playbook]
- **瓶頸卡**：[[延遲與成本_Latency-Cost]]
- **工具卡**：[[Evaluation_評測與可觀測性]]

---

## 參考來源

[^DOC_Diffusion_Overview]: Diffusion Models Overview. 各模型官方文件彙整。

[^DOC_DALLE3]: OpenAI. DALL-E 3 Documentation. https://platform.openai.com/docs/guides/images

[^DOC_StableDiffusion]: Stability AI. Stable Diffusion Documentation. https://stability.ai/

---

## 文件狀態

| 欄位 | 值 |
|------|------|
| Status | Stable |
| 待補 Evidence | 圖像生成評測 benchmark 論文 |
| 待補 Playbook | 行銷素材生成 Playbook |
