# 🏆 接案平台「成長等級制度」導入規格書
This document provides a refactored specification for importing the **AI Lab 7-Stage Growth Levels** into your existing freelance platform. It focuses strictly on level definitions, capabilities, and matching project types to make it easy for your development team or Codex to implement.

---

## 🎯 核心概念：接案方能力與專案類型對照

我們將 AI Lab 的 7 個學習階段直接對應至接案平台的 **「接案方能力等級」**。這有助於雇主快速篩選適合的開發者，也讓開發者有明確的晉升方向。

| 等級 | 平台等級名稱 (對應 AI Lab 階段) | 能力描述 (一言以蔽之) | 適合媒合之接案項目 (參考) |
|---|---|---|---|
| **LV0** | **AI 新手村 (AI Novice)** | 消除恐懼，建立人機協作思維。 | 基礎資料登錄、AI 潤稿輔助、文案翻譯與校對。 |
| **LV1** | **AI 探索者 (AI Explorer)** | 掌握提示詞精髓，能將 LLM 運用於日常辦公與內容產出。 | 結構化 Prompt 範本撰寫、客服話術與文案自動化生成。 |
| **LV2** | **AI 實踐者 (AI Implementer)** | 能使用 Vibe Coding 工具快速做出具備互動功能的產品原型。 | MVP 快速原型設計、靜態/動態網頁 UI 生成 (如 v0.dev, bolt.new, Lovable 等) 、低代碼 Chatbot 搭建。 |
| **LV3** | **初階 AI 建造者 (Junior AI Builder)** | 交付能存檔、能運作的真實全端系統。 | 完整全端網站開發、資料庫整合、自定義 API 串接與雲端部署。 |
| **LV4** | **流程自動化專家 (Workflow Specialist)** | 串聯企業碎片化工具，打造免人工干預的自動化流程。 | n8n / Make.com 跨 SaaS 平台自動化串接、Webhook 即時觸發與錯誤處理流程。 |
| **LV5** | **高階 AI 架構師 (Senior AI Builder)** | 打造具備自主決策、工具調用與企業記憶（RAG）的 Agent 系統。 | LangGraph 複雜狀態機設計、企業級知識庫（RAG）優化、多智能體（Multi-Agent）協作系統。 |
| **LV6** | **自我進化架構師 (Evolution Architect)** | 設計具備自我反思、評估與改進能力的元 Agent。 | 自動化評測系統（LLM-as-a-judge）、DSPy 動態 Prompt 編譯、推理模型（如 GRPO/DPO）微調。 |

---

## 📐 各等級詳細描述與接案項目對照

以下為每個等級的具體定義、能力特徵以及推薦的接案專案類型，供系統及 Codex 進行邏輯比對。

### ⛩️ LV0：AI 新手村 (AI Novice)
*   **能力定義**：能夠流暢地與主流 AI (ChatGPT/Claude/Gemini/DeepSeek) 進行日常提問與日常協作。
*   **適合接案項目**：
    *   **AI 輔助內容產出**：社群貼文初稿撰寫、產品描述優化。
    *   **翻譯與校對**：利用 AI 進行多國語言翻譯並進行人工潤飾。
    *   **資料整理**：將雜亂文本交由 AI 整理成結構化表格。

### 🧭 LV1：AI 探索者 (AI Explorer)
*   **能力定義**：熟練提示詞工程 (Prompt Engineering)，能撰寫出防止幻覺、格式穩定的結構化 System Prompt。
*   **適合接案項目**：
    *   **結構化 Prompt 客製**：為企業行銷、人資或客服團隊設計專用的 AI 提示詞模板。
    *   **AI 工具導入顧問**：引導企業員工使用 AI 進行日常工作減負。
    *   **基礎知識庫配置**：在 GPTs 或類似平台上進行基礎文檔的上傳與提示詞設定。

### 🎨 LV2：AI 實踐者 (AI Implementer)
*   **能力定義**：進入 Vibe Coding 領域，熟練使用 UI 生成與原型開發工具 (v0.dev, bolt.new, Lovable 等) 快速產出高保真 MVP 原型。
*   **適合接案項目**：
    *   **產品 MVP 快速開發**：在數天內為創業團隊製作出可互動的網頁/應用程式原型以利募資。
    *   **活動 Landing Page 製作**：快速生成視覺美觀且具備基本聯絡表單的網頁。
    *   **Dify/Coze 基礎工作流**：在無代碼平台搭建簡單的客服或資訊收集 Bot。

### 🛠️ LV3：初階 AI 建造者 (Junior AI Builder)
*   **能力定義**：具備代碼開發與部署能力，能打通前端、後端、資料庫與外部 API，交付穩定運作的 Web 系統。
*   **適合接案項目**：
    *   **客製化 Web 應用開發**：帶有使用者登入、權限管理與資料庫儲存的客製化網站。
    *   **AI API 應用整合**：將 OpenAI/Anthropic API 整合進企業現有的系統中。
    *   **第三方服務串接**：串接綠界金流、Line Pay、簡訊發送等外部 API。

### 🔗 LV4：流程自動化專家 (Workflow Specialist)
*   **能力定義**：擅長使用自動化平台 (n8n, Make.com) 串接不同的 SaaS 工具，建立無人值守的工作流。
*   **適合接案項目**：
    *   **企業自動化工作流**：如「當 Line 收到客戶詢價時，自動寫入 Google Sheets 並且發送 Slack 通知給業務」。
    *   **自動化報表生成**：自動定期抓取廣告後台數據，經由 AI 分析後寄送 PDF 報表給主管。
    *   **SaaS 數據同步**：在 HubSpot CRM、Shopify 與內部 ERP 之間建立雙向數據同步。

### 🧠 LV5：高階 AI 架構師 (Senior AI Builder)
*   **能力定義**：能夠使用程式碼框架 (LangChain, LangGraph) 設計擁有記憶、RAG 知識庫與自主決策工具的生產級 AI 系統。
*   **適合接案項目**：
    *   **有狀態多輪對話客服**：設計能根據用戶意圖，調用不同 API 並記錄長期記憶的智能客服。
    *   **高級 RAG 知識庫優化**：針對海量企業內部文件，設計 PDF 解析、語意分塊與 Rerank 重排管道，大幅提升問答準確率。
    *   **MCP Server 開發**：為 Cursor 或企業內部的 AI Client 開發專屬的本地工具連接器。

### 🧬 LV6：自我進化 Agent 架構師 (Evolution Architect)
*   **能力定義**：設計能自我反思、評估並持續改進的元 Agent 系統，讓 AI 在運行中自我優化。
*   **適合接案項目**：
    *   **自動化 Prompt 優化引擎**：使用 DSPy 等框架，建立能根據歷史失敗案例自動調整 Prompt 的自適應系統。
    *   **AI 自動化評測護欄**：為企業 AI 系統搭建評估機制（LLM-as-a-judge），自動偵測並過濾不合規回覆。
    *   **推理模型微調 (LoRA/GRPO)**：在特定領域（如法律、醫療）下，微調開源模型以提升其邏輯推理與格式輸出能力。

---

## 📝 導入現有網站的 Codex 提示詞指引

當您要在現有的網站 codebase 中加入此等級制度時，可以將以下 Prompt 提供給您的 Codex：

```markdown
我們正在現有的網站中導入「接案方成長等級制度」。請閱讀以下等級定義：
- 0: AI Novice (適合資料登錄、AI 潤稿)
- 1: AI Explorer (適合 Prompt 範本撰寫、客服話術優化)
- 2: AI Implementer (適合 MVP 原型、v0/bolt.new 網頁、Dify 基礎 Bot)
- 3: Junior AI Builder (適合全端網站、API 串接、資料庫整合)
- 4: Workflow Specialist (適合 n8n/Make 流程自動化)
- 5: Senior AI Builder (適合 LangGraph 狀態機、RAG 優化、多智能體)
- 6: Evolution Architect (適合 DSPy、自我反思系統、模型微調)

請在我們現有的專案中協助完成以下調整：
1. 在代表接案方的資料表中（例如 User 或 Profile），新增 `growth_level` 欄位（預設為 0）。
2. 在接案方個人主頁組件中，根據其 `growth_level` 渲染出對應的等級稱號（如 LV3 初階 AI 建造者）。
3. 在專案（Job）發布與篩選邏輯中，允許案主設定「期望的最低 AI 等級」，並在列表篩選或推薦演算法中，將符合或高於該等級的接案者排在前面。
```
