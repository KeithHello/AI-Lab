# 🧠 Stage 5：高階 AI 架構師 (Senior AI Builder)

> **一句話定義**：AI Lab 的 Agent 系統殿堂。打造具備「自主思考、決策、調用工具、擁有企業記憶（RAG）」的 AI Agent 系統。

---

## 🎯 等級定位

| 維度 | 內容 |
|---|---|
| **階段定位** | Agent 開發的集大成——從「寫一個 Agent」到「設計一套 Agent 系統」 |
| **上一階段** | [Stage 3](./stage-3-junior-builder.md) 或 [Stage 4](./stage-4-workflow-specialist.md) |
| **下一階段** | [Stage 6：自我進化 Agent 架構師](./stage-6-evolution-architect.md) |
| **對應 Roadmap** | [Phase 4：RAG & Memory](../AI-Agent-學習路線圖.md#phase-4rag--memory--給-agent-裝上大腦2-3-周) + [Phase 6：Multi-Agent](../AI-Agent-學習路線圖.md#phase-6multi-agent--前沿--追平業界持續) |
| **建議學習時間** | 5-7 週（衝刺型）/ 8-12 週（穩健型） |

### 你在這個階段的畫像

- 你已經能獨立寫 Agent，但你的 Agent 還很「笨」——沒有長期記憶、不會協作
- 你想讓 Agent 真正幫企業解決複雜問題，而不是只能回答 FAQ
- **這個階段的目標**：交付一套能替代高階人力的企業級 Multi-Agent 系統

---

## 📐 前置條件

本階段提供 **A軌：技術代碼軌** 與 **B軌：企業低代碼軌** 雙路徑選擇：

### A軌：技術代碼軌
- ✅ 已完成 [Stage 3](./stage-3-junior-builder.md)（技術路線）
- ✅ 熟練使用 Python/LangChain 開發與自定義 Tool
- ✅ 有 Python API 部署與 Docker 基礎
- ✅ 建議：有 1 個上線的全棧專案經驗

### B軌：企業低代碼軌
- ✅ 已完成 [Stage 4](./stage-4-workflow-specialist.md)（自動化路線）
- ✅ 熟練使用 Coze / Dify 搭建基本 Agent 工作流
- ✅ 熟練 n8n 或 Make.com 多系統自動化整合

---

## 🧠 知識點清單

### 1. RAG（檢索增強生成）全流程

```
離線階段（Indexing）：
文件 → 分塊(Chunking) → 向量化(Embedding) → 存入向量資料庫

線上階段（Retrieval + Generation）：
使用者提問 → 向量化 → 相似度檢索 → 重排序(Rerank) → 拼接上下文 → LLM 生成答案
```

| 環節 | 關鍵技術 | 常見方案 |
|---|---|---|
| **文件解析** | PDF/Word/HTML → 純文字 | Unstructured, MinerU, Markitdown |
| **分塊策略** | 怎麼切才能讓檢索更準？ | RecursiveCharacterTextSplitter, Semantic Chunking |
| **Embedding** | 把文字變成向量 | text-embedding-3-small, bge-m3, jina-embeddings |
| **向量資料庫** | 存向量 + 快速搜尋 | Chroma（入門）, Milvus/Qdrant（生產） |
| **檢索策略** | 怎麼搜到對的？ | 混合檢索（向量+關鍵詞）, HyDE, Multi-Query |
| **Rerank** | 搜到後怎麼排序？ | Cohere Rerank, BGE-Reranker |
| **評估** | 檢索到的東西對不對？ | RAGAS（faithfulness, relevancy, precision） |

#### RAG 優化核心心法

> RAG 的效果 **80% 取決於分塊和檢索策略**，而非模型本身。

```
常見 RAG 失敗原因排行榜：
1. 文件切太碎 → 上下文不完整
2. 只用向量檢索 → 關鍵詞匹配不到（如產品代碼 "SKU-123"）
3. 沒有 Rerank → 相關文件排在很後面被截斷
4. Embedding 模型不適合中文 → 語義理解偏差
```

### 2. Memory 三層架構

```
┌─────────────────┐
│  Working Memory │ ← 當前對話上下文（最活躍、最昂貴）
├─────────────────┤
│ Short-term Mem  │ ← 本次會話歷史（暫時但完整）
├─────────────────┤
│  Long-term Mem  │ ← 跨會話持久化記憶（壓縮、可檢索）
└─────────────────┘
```

**關鍵操作**：
- **下沉(sink)**：重要資訊從 Working → Long-term（摘要儲存）
- **上浮(pull)**：檢索 Long-term 中的相關資訊到 Working（語義檢索）

### 3. LangGraph — 有狀態的 Agent 工作流

**為什麼需要 LangGraph**：Chain 是線性的（A→B→C），但真實 Agent 需要分支、循環、條件判斷、人工介入。

```python
from langgraph.graph import StateGraph, START, END

# 核心概念
# State: Agent 的狀態（對話歷史、中間結果、使用者偏好等）
# Node: 一個處理步驟（呼叫 LLM、執行工具、檢查結果）
# Edge: 連接節點的線（普通邊、條件邊）
# Checkpoint: 狀態的快照（支援暫停/恢復/回溯）
```

**LangGraph 經典模式**：

```
                ┌─────────┐
     START ───→ │ 意圖識別 │
                └────┬────┘
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
    ┌─────────┐ ┌─────────┐ ┌─────────┐
    │ 檢索知識 │ │ 呼叫工具 │ │ 轉人工  │
    └────┬────┘ └────┬────┘ └────┬────┘
         │           │           │
         └───────────┼───────────┘
                     ▼
              ┌───────────┐
              │  生成回覆  │
              └─────┬─────┘
                    │
              ┌─────▼─────┐
              │ 滿意度檢查 │
              └─────┬─────┘
                    │
         ┌─────────┼─────────┐
         ▼                   ▼
    [滿意 → END]    [不滿意 → 轉人工]
```

### 4. Multi-Agent 協作

#### 4.1 協作模式

| 模式 | 描述 | 類比 |
|---|---|---|
| **Supervisor** | 一個主 Agent 分配任務給子 Agent | 專案經理 + 執行團隊 |
| **Decentralized** | Agent 之間平等協商 | 團隊 Brainstorming |
| **Hierarchical** | 多層級的 Agent 結構 | 公司組織架構 |
| **Blackboard** | Agent 共享一個資料空間 | 共享白板協作 |

#### 4.2 主流 Multi-Agent 框架

| 框架 | 特點 | 適合場景 |
|---|---|---|
| **CrewAI** | 角色扮演 + 任務分配，最易上手 | 內容創作、市場分析 |
| **AutoGen (Microsoft)** | 對話驅動，支援人機協作 | 研究分析、程式碼審查 |
| **LangGraph** | 圖結構，最靈活 | 複雜業務邏輯 |
| **OpenAI Swarm** | 輕量級，適合實驗 | 快速原型 |

### 5. MCP (Model Context Protocol) & A2A

#### MCP：統一工具標準

```
┌──────────┐     MCP Protocol     ┌──────────────┐
│  Agent   │ ←──────────────────→ │  MCP Server   │
│ (Client) │   tools/list         │ (工具提供方)  │
│          │   tools/call         │               │
└──────────┘                      └──────────────┘
```

- MCP Server 可以是你寫的任何服務
- Claude Desktop / Cursor 都支援 MCP
- 一旦寫好 MCP Server，任何支援 MCP 的 Agent 都能直接呼叫

#### A2A：Agent 之間的語言

| | MCP | A2A |
|---|---|---|
| **誰和誰通訊** | Agent ↔ Tool | Agent ↔ Agent |
| **解決的問題** | Agent 怎麼呼叫工具？ | Agent 之間怎麼協作？ |

### 6. 生產部署 Checklist

| 維度 | 要做什麼 | 工具/方案 |
|---|---|---|
| **部署** | 容器化 + API 服務 | Docker + FastAPI |
| **安全** | 沙箱隔離、權限控制 | Docker sandbox, API Key 管理 |
| **監控** | Token 用量、回應時間、錯誤率 | LangSmith, LangFuse |
| **成本** | 快取策略、模型降級 | 語義快取、小模型兜底 |
| **評測** | 回答品質、工具呼叫準確率 | RAGAS + 人工標註 + A/B 測試 |
| **流式輸出** | SSE / WebSocket | FastAPI StreamingResponse |

> [!WARNING]
> **安全隔離原則 (Sandbox execution)**：
> 當 Agent 擁有執行代碼（如 Python Repl, Shell）的工具時，**絕對禁止**直接在主伺服器主機環境執行。必須通過獨立 Docker 容器、WASM（WebAssembly）沙箱或伺服器無伺服器沙箱（如 E2B Sandbox）進行物理隔離，並設置嚴格的執行逾時和記憶體限制。
> 
> **防注入防禦 (Prompt Injection Defense)**：
> 應實施「輸入過濾」和「護欄模型（如 Llama Guard / Guardrails AI）」，檢測輸入中是否包含 "ignore previous instructions" 等惡意嘗試。

---

## 🛠️ 技能要求

### 硬技能

| 技能 | 說明 | 熟練度目標 |
|---|---|---|
| RAG 全流程 | 從文件解析到評估 | 熟練 |
| LangGraph | StateGraph、條件邊、Checkpoint | 熟練 |
| Multi-Agent 架構 | CrewAI / AutoGen / LangGraph | 掌握 |
| MCP Server 開發 | 標準化工具介面 | 掌握 |
| 向量資料庫 | Chroma / Milvus / Qdrant | 掌握 |
| 監控與評測 | LangSmith / LangFuse / RAGAS | 掌握 |
| Docker 部署 | Dockerfile、docker-compose | 掌握 |

### 軟技能

- **系統設計**：能設計 Multi-Agent 的協作架構
- **效能調優**：能診斷 RAG 的檢索瓶頸
- **技術溝通**：能向客戶解釋 Agent 能做什麼、不能做什麼

### 推薦工具

| 工具 | 用途 | 費用 |
|---|---|---|
| [LangGraph](https://langchain-ai.github.io/langgraph/) | 有狀態 Agent 工作流 | 免費開源 |
| [CrewAI](https://www.crewai.com/) | Multi-Agent 框架 | 免費開源 |
| [LangSmith](https://www.langchain.com/langsmith) | Agent 監控與調試 | 免費/付費 |
| [LangFuse](https://langfuse.com/) | 開源 LLM 可觀測性 | 免費開源 |
| [Chroma](https://www.trychroma.com/) | 向量資料庫（入門） | 免費開源 |
| [Milvus](https://milvus.io/) | 向量資料庫（生產） | 免費開源 |

---

## 💪 練習項目

### 練習 1：最小 RAG 系統（3 小時）

**目標**：從零搭建一個 RAG 系統，理解每個環節。

```
步驟：
1. 收集 5 篇技術文章（文字檔）
2. 用 LangChain TextSplitter 進行分塊
3. 用 OpenAI Embedding 向量化
4. 存入 Chroma 向量資料庫
5. 實現查詢 → 檢索 → 生成
6. 用 RAGAS 評估檢索品質（faithfulness, relevancy）

對比實驗：
- 固定大小分塊 vs 語義分塊（哪個效果好？）
- 只用向量檢索 vs 添加 Rerank（效果差多少？）
```

### 練習 2：帶記憶的 Agent（3 小時）

**目標**：讓 Agent 記住跨會話的資訊。

```
功能設計：
- Working Memory：當前對話
- Short-term Memory：本次會話歷史（直接用 context window）
- Long-term Memory：用 SQLite 存對話摘要
  - 每次對話結束時，Agent 自動摘要重點存入
  - 下次對話開始時，自動檢索相關記憶

測試：先問 Agent「我叫小明，我喜歡喝咖啡」，
結束後開新對話問「你記得我喜歡喝什麼嗎？」
```

### 練習 3：LangGraph 客服 Agent（4 小時）

**目標**：把 Stage 3 的 Agent 改寫成 LangGraph 有狀態版本。

```python
# 狀態定義
class AgentState(TypedDict):
    messages: list          # 對話歷史
    intent: str             # 辨識出的使用者意圖
    retrieved_docs: list    # 從知識庫檢索到的文件
    needs_human: bool       # 是否需要轉人工

# 圖結構
graph = StateGraph(AgentState)

graph.add_node("classify_intent", classify_intent_node)
graph.add_node("retrieve", retrieve_node)
graph.add_node("generate", generate_node)
graph.add_node("human_handoff", human_node)
graph.add_node("check_satisfaction", check_satisfaction_node)

graph.add_edge(START, "classify_intent")
graph.add_conditional_edges("classify_intent", route_by_intent, {
    "question": "retrieve",
    "complaint": "human_handoff",
    "other": "generate"
})
graph.add_edge("retrieve", "generate")
graph.add_edge("generate", "check_satisfaction")
graph.add_conditional_edges("check_satisfaction", route_by_satisfaction, {
    "satisfied": END,
    "unsatisfied": "human_handoff"
})
```

#### B軌（低代碼）：Dify 進階工作流對應
對於不使用 Python 的 B軌學員，**Dify/Flowise** 的視覺化編輯器是實現有狀態有向無環圖 (DAG) 工作流的核心工具。其邏輯與 A軌代碼完全對應：
- **Dify 意圖分類節點 (Intent Classifier)** = 條件分支邊 (Conditional Edges)
- **知識庫檢索節點 (Knowledge Retrieval)** = RAG Node
- **Tool 節點 / HTTP 節點** = Function Calling Node
- **人工審核節點 (Human Review Node)** = Human-in-the-loop / Input Interceptor (人工介入與狀態快照恢復)

### 練習 4（專案 A）：Multi-Agent 內容創作團隊（5 小時）

**目標**：用 CrewAI 搭建一個多 Agent 協作的內容創作系統。

```
Agent 團隊：
- Agent 1（研究員）：搜尋 + 整理資料
- Agent 2（寫手）：根據資料生成文章
- Agent 3（編輯）：審查 + 潤色
- Agent 4（審核員）：最終品質把關

協作流程：
研究員接收主題 → 搜集資料 → 交給寫手 →
寫手生成初稿 → 交給編輯 → 編輯潤色 → 
交給審核員 → 通過或退回修改
```

### 練習 5（專案 B）：MCP Server 開發（3 小時）

**目標**：寫一個 MCP Server，讓 Claude Desktop 能透過它查詢本地資料。

```
MCP Server 功能：
- tools/list：提供「查詢資料庫」、「執行程式」、「讀取檔案」三個工具
- tools/call：實際執行工具並回傳結果

測試：
- 在 Claude Desktop 中載入這個 MCP Server
- 對 Claude 說「幫我查一下今天有多少筆訂單」
- 觀察 Claude 如何透過 MCP 協議呼叫你的工具
```

### 練習 6（專案 C）：企業級 Multi-Agent 系統（8 小時）

**目標**：為一個虛擬企業設計並實現一套完整的 Multi-Agent 解決方案。

**場景選擇（擇一）**：

| 場景 | 核心 Agent | 給定測試數據 |
|---|---|---|
| 智能電商客服總監 | 意圖分類 Agent + 知識庫 Agent + 退貨處理 Agent + 客訴升級 Agent | 20 條真實客服對話（附在下方） |
| AI 合約審查官 | 文件解析 Agent + 風險標記 Agent + 報告生成 Agent | 2 份範例合約（NDA + 採購合約，提供 PDF 連結） |
| AI 供應鏈調度總監 | 庫存監控 Agent + 需求預測 Agent + 採購生成 Agent | 模擬庫存 CSV（30 天歷史 + 安全庫存閾值） |

**通用技術要求**：
| 需求 | A軌 | B軌 |
|---|---|---|
| 知識庫 | Chroma + OpenAI Embedding | Dify 知識庫節點 |
| 工作流 | LangGraph StateGraph | Dify Workflow（含條件分支） |
| 監控 | LangFuse 全鏈路追蹤 | Dify 內建日誌 + Google Sheets 儀表板 |
| 部署 | Docker + FastAPI | Dify Cloud / 自架 |

**驗收清單**（A軌）：
- [ ] RAG 知識庫正確檢索，Top-3 檢索結果在 10 條測試中 ≥ 7 條命中正確答案
- [ ] 至少 3 個 Agent 協作，工作流無死循環
- [ ] LangFuse 儀表板顯示完整的 Token 用量和延遲
- [ ] Docker 部署可一鍵啟動（`docker-compose up`）
- [ ] 處理 30 條測試案例，記錄：準確率、平均回應時間、平均 Token 成本
- [ ] 產出 1 份系統設計文件（含架構圖 + 技術選型 + 部署步驟 + 測試報告）

**驗收清單**（B軌）：
- [ ] 知識庫上傳文件後，檢索結果在 10 條測試中 ≥ 7 條正確
- [ ] 意圖分類節點在 10 條混合輸入中 ≥ 8 條分類正確
- [ ] 至少 1 條路徑包含人工審核節點，正確觸發
- [ ] 對話記錄自動歸檔到 Google Sheets
- [ ] 產出 1 頁系統架構說明文件（含 Dify 工作流截圖）

---

## 💪 B軌練習項目（企業低代碼軌）

> 以下練習專為不寫程式碼的 B 軌學員設計，使用 Dify / n8n / Make.com 實現與 A 軌等效的學習目標。

### B軌練習 1：Dify + RAG 企業知識庫 Agent（3 小時）

**場景**：某電商公司有 5 份產品說明文件，客服人員每次都要手動翻找。你需要在 Dify 中搭建一個能回答產品問題的 AI Agent。

**給定資源**：上傳以下 5 種類型的文件到 Dify 知識庫（自己找真實文件或模擬）：
- 產品規格表（1 份，含尺寸、材質、價格）
- 退換貨政策（1 份）
- 常見問題 FAQ（1 份，至少 10 條 Q&A）
- 保固說明（1 份）
- 運送政策（1 份）

**驗收清單**：
- [ ] 在 Dify 中建立知識庫，上傳全部 5 份文件
- [ ] 設定意圖分類節點：產品詢問 / 訂單問題 / 退換貨 / 其他
- [ ] 產品詢問 → 知識庫檢索 → LLM 生成回答（附文件來源引用）
- [ ] 退換貨 → 顯示退貨流程 + 人工審核節點（模擬轉真人）
- [ ] 用 10 條測試問題驗證，記錄意圖分類準確率（目標 > 80%）

### B軌練習 2：Dify 多 Agent 協作工作流（4 小時）

**場景**：仿照 A 軌的「Multi-Agent 內容創作團隊」，在 Dify 中實現等效的多 Agent 串聯。

**Dify 實現方式**：
| 角色 | Dify 節點 | 輸入 | 輸出 |
|---|---|---|---|
| 研究員 | HTTP 請求節點 | 主題關鍵字 | 搜尋結果（JSON 格式） |
| 寫手 | LLM 節點 | 研究資料 + 寫作 Prompt | 500 字文章草稿 |
| 編輯 | LLM 節點 | 草稿 + 潤色指令 | 終稿 |

**驗收清單**：
- [ ] 三個 Agent 節點串聯成一個完整 Workflow
- [ ] 輸入一個主題 → 自動產出一篇 500 字以上文章
- [ ] 含條件分支：如果研究員節點回傳空結果 → 提示「無法找到相關資料，請換個主題」
- [ ] 含變數傳遞：研究員的輸出作為寫手的輸入，寫手的輸出作為編輯的輸入

### B軌練習 3：Dify + 外部 API 連接器（3 小時）

**場景**：讓 Dify Agent 能查詢即時數據——不只是回答文件裡的靜態內容，還能告訴使用者「現在外面的天氣」、「即時股價」、「某個訂單的狀態」。

**核心任務**：建立至少 1 個自定義 HTTP 連接器。

**建議 API**（選一個）：
- 公開天氣 API（如 OpenWeatherMap 免費層）
- 公開股票 API（如 Alpha Vantage 免費層）
- 自建 Mock API（用 n8n Webhook 模擬 CRM 查詢回傳假資料）

**驗收清單**：
- [ ] 成功配置至少 1 個外部 API 連接器（含認證設定）
- [ ] Dify Agent 能根據對話內容自動決定是否呼叫該 API
- [ ] API 回傳的 JSON 資料被正確解析為自然語言回覆（不是直接吐出 JSON）
- [ ] 含錯誤處理：API 呼叫失敗時 Agent 回覆「暫時無法查詢，請稍後再試」

### B軌練習 4（專案）：Dify 企業級智能客服總監（6 小時）

**場景**：完整的企業客服 Multi-Agent 系統——B 軌版的「專案 C」。

**功能地圖**：
```
客戶輸入
  ↓
意圖分類節點
  ├── 產品詢問 → 知識庫檢索 → LLM 生成回答（附來源引用）
  ├── 退換貨 → HTTP 節點（查詢訂單 API）→ 條件判斷（退貨資格）
  │              ├── 符合資格 → LLM 生成退貨標籤文字
  │              └── 不符合 → LLM 生成拒絕原因說明
  ├── 客訴 → 記錄到 Google Sheets（n8n Webhook）→ Slack 通知 → 人工審核
  └── 其他 → LLM 自由回答
```

**驗收清單**：
- [ ] 至少 3 條不同意圖的路徑正常工作
- [ ] 知識庫檢索的回答附有來源引用（Dify 內建功能）
- [ ] 人工審核節點正確觸發（含說明何時需要人工介入）
- [ ] 對話記錄自動歸檔到 Google Sheets（透過 n8n Webhook 或 Make.com 串接）
- [ ] 產出 1 頁系統架構說明文件（含 Dify 工作流截圖 + 節點說明）

---

## 🏅 通過標準

**A軌（代碼軌）硬性指標**：

- [ ] 為企業成功設計、測試並實際上線 **1 套**客製化的多智能體協作系統
- [ ] 系統必須包含：RAG 知識庫 + 至少 3 個協作 Agent + LangGraph 有狀態工作流
- [ ] 部署為可公開訪問的服務（Docker + FastAPI）
- [ ] 通過 30 條測試案例，記錄各項指標（準確率、回應時間、Token 成本）
- [ ] 產出 1 份完整的系統設計文件（架構圖 + 技術選型說明 + 部署指南）

**B軌（低代碼軌）硬性指標**：

- [ ] 在 Dify 中搭建 **1 套**多 Agent 協作工作流
- [ ] 系統必須包含：RAG 知識庫 + 意圖分類 + 至少 1 條人工審核路徑 + 外部 API 連接器
- [ ] 工作流可演示（接受 Dify 分享連結或截圖錄影）
- [ ] 通過 10 條測試案例，記錄意圖分類準確率和回答正確率
- [ ] 產出 1 頁系統架構說明文件（含 Dify 工作流截圖）

**軟性指標**（A/B 通用）：

- [ ] 能根據業務需求選擇合適的 Multi-Agent 架構模式
- [ ] 能診斷 RAG 系統的檢索瓶頸並優化
- [ ] 能在面試中清晰地解釋 Agent 系統的架構設計

---

## 🔝 升階條件

**進入 Stage 6 前，你應該能回答以下問題**：

1. 你的 Multi-Agent 系統上線後，如何發現它在變差？用什麼指標監控？
2. 如果讓你的 Agent 系統自己在失敗中學習，需要增加哪些機制？
3. GRPO 和 DPO 有什麼不同？什麼情況下該用哪個？

**下一步**：

| 路線 | 說明 |
|---|---|
| [Stage 6：自我進化 Agent 架構師](./stage-6-evolution-architect.md) | 讓你的 Agent 不再需要人工調優——它會自己變好 |

---

## 📚 學習資源

### 免費資源

| 資源 | 簡介 | 連結 |
|---|---|---|
| LangGraph 官方文件 | 有狀態 Agent 完整指南 | [langchain.com](https://langchain-ai.github.io/langgraph/) |
| CrewAI 文件 | Multi-Agent 框架入門 | [crewai.com](https://docs.crewai.com/) |
| MCP 官方規範 | Model Context Protocol 標準 | [modelcontextprotocol.io](https://modelcontextprotocol.io/) |
| Haozhe-Xing/agent_learning | 論文精讀 + Multi-Agent 架構 | [GitHub](https://github.com/Haozhe-Xing/agent_learning) |
| RAGAS 文件 | RAG 評估框架 | [ragas.io](https://docs.ragas.io/) |

### 推薦論文

| 論文 | 核心貢獻 | 連結 |
|---|---|---|
| MemGPT | 給 LLM 作業系統級記憶管理 | [arXiv](https://arxiv.org/abs/2310.08560) |
| AutoGen | 多 Agent 對話框架 | [arXiv](https://arxiv.org/abs/2308.08155) |
| DeepSeek-R1 (GRPO) | 強化學習訓練推理能力 | [arXiv](https://arxiv.org/abs/2501.12948) |
| SWE-bench | 軟體工程 Agent 評測基準 | [arXiv](https://arxiv.org/abs/2310.06770) |

---

> **給 Stage 5 的你**：到了這個階段，你已經是業界搶手的人才。你能獨立設計和交付一套 AI Agent 系統——這是目前市場上最稀缺的能力之一。但別停在這裡：你做的系統每次出錯時，都要靠你手動修。下一步是讓系統學會自己修。
>
> **下一步**：[進入 Stage 6：自我進化 Agent 架構師](./stage-6-evolution-architect.md)
