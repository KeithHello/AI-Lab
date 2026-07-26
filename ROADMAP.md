# ROADMAP.md — AI Lab 專案進度追蹤

本檔案為專案真實進度源，記錄當前階段、已完成事項、進行中工作與最近驗證結果。

---

## 📌 當前階段
**階段**：GitHub Pages 設定與線上驗證  
**目標**：完成已確認成果的 PR 審核，設定 GitHub Pages 並驗證公開網址。

---

## ✅ 已完成

### 1. 學習體系與成長等級制度
- [x] 建立 7 階段等級制度（Stage 0–6）AI-Lab-成長等級制度.md。
- [x] 建立 AI Agent 學習路線圖（Phase 0–6）AI-Agent-學習路線圖.md。
- [x] 建立 7 個 Stage 詳細手冊（stages/stage-0-ai-novice.md 至 stages/stage-6-evolution-architect.md）。
- [x] 增加代碼軌／低代碼軌（A/B 雙軌）實戰設計與 Stage 2→3 橋接練習。
- [x] 加入 9 張 Mermaid 視覺化圖表。
- [x] 接案平台成長等級導入規格 AI-Lab-接案平台成長等級設計.md。

### 2. 靜態成果網站與獨立課程頁面（2026-07-26 完成）
- [x] 建立根重導向頁面 docs/index.html。
- [x] 建立成果總覽頁面 docs/ai-lab-showcase/index.html。
- [x] 將成果總覽的 7 個 Stage 卡片連結至對應的獨立 HTML 課程頁面，並加入查看課程提示。
- [x] 建立 7 個 Stage 的手機版 HTML 課程頁面（docs/ai-lab-showcase/stages/stage-0.html 至 stage-6.html）。
- [x] 擴充 docs/ai-lab-showcase/style.css，加入程式碼區塊、卡片與 Stage 上下頁導航樣式。
- [x] 移除決議事項、個人署名與原始 .md 檔案連結，全數轉換為 HTML 頁面呈現。
- [x] 將成果首頁調整為能力成果導向：呈現培養的人才、企業問題對應、七階段學習／通過標準／通過後能力，以及後續延展方向。
- [x] 首頁語氣改為中肯客觀，移除個人與組織主詞及促銷式對比語句。

### 3. 開發規範與檔案排除
- [x] 更新 .gitignore 排除本地內部分析檔 nalysis-*.md 與展示目錄內 .md 備份檔。
- [x] 建立 CLAUDE.md 專案規範文件。

### 4. 本機驗收
- [x] 主人已確認根入口、成果總覽與 7 個 Stage 課程頁面。

---

## 🔄 進行中
- [ ] 設定 GitHub Pages 為 main 分支的 /docs 資料夾並驗證公開網址。

---

## 📋 待辦事項
- [ ] PR #2 審核後合併至 main。
- [ ] 統一 README、路線圖與 Stage 手冊中的統計數字。
- [ ] 補齊代表性項目的測試資料包與執行範例。

---

## 🧪 最近驗證
- **2026-07-26**：完成成果首頁方向 A 改版；確認 9 個主要內容區塊、7 個 Stage 課程連結、HTML section 開關數量一致，且未出現「弘基」「執事會」或「方案 Review」文字。
- **2026-07-26**：完成 7 個 Stage HTML 課程頁面與導航建置；成果總覽卡片可直接開啟對應課程；docs/index.html 可導向成果總覽；全部頁面通過 HTTP 200 測試；主人已確認本機成果；commit 39b33d6 已推送，PR #2 已建立，等待 GitHub Pages 設定。
