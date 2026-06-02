# 🤖 AI Agent 從入門到進階 — 學習路線圖

> **目標人羣**：對 AI Agent 有基本瞭解，知道 ChatGPT/Claude/Coze 是什麼，但面對「如何自己做一個 Agent」「如何深入 Agent 開發」時不知從何下手的人。
>
> **設計哲學**：每一階段都包含 **「學什麼 → 練什麼 → 用什麼工具 → 產出什麼」** 四個環節，確保每一步都有可驗證的成果。
>
> 📐 **配套等級制度**：本路線圖對應 [AI Lab 7 階段成長等級制度](./AI-Lab-成長等級制度.md)，每個 Phase 完成後可獲得相應等級認證。

---

## AI Lab 等級快速對照

| Roadmap Phase | 對應 AI Lab 等級 | 一句話定位 |
|---|---|---|
| Phase 0 | Stage 0 — AI 新手村 | 消除恐懼，建立人機協作思維 |
| Phase 1 | Stage 1 — AI 探索者 | 把 LLM 用成頂級特助 |
| Phase 2 | Stage 2 — AI 實踐者 | 用 AI 快速做出能看的原型 |
| Phase 3 | Stage 3 — 初階 AI 建造者 | 交付能存檔、能運作的真實系統 |
| Phase 4 | Stage 5 組件 — RAG & Memory | 給 Agent 裝上知識和大腦 |
| Phase 5 | Stage 4 — 自動化專家 / Stage 5 組件 | 從 Demo 到產品的關鍵跨越 |
| Phase 6 | Stage 5 — 高階架構師 | Multi-Agent 系統設計 |
| Phase 6 延伸 | Stage 6 — 自我進化架構師 🆕 | 設計能自我改進的元 Agent |

> 💡 **詳細等級定義、通過標準、升階條件** → 見 [AI-Lab-成長等級制度.md](./AI-Lab-成長等級制度.md)

---

## 目錄

- [快速自測：你現在在哪個階段？](#快速自測你現在在哪個階段)
- [Phase 0：前置知識補漏（1-2 天）](#phase-0前置知識補漏1-2-天)
- [Phase 1：Agent 核心心智（1 周）](#phase-1agent-核心心智1-周)
- [Phase 2：低代碼實戰 — 先做出來再理解（2 周）](#phase-2低代碼實戰--先做出來再理解2-周)
- [Phase 3：代碼級 Agent — 打開黑盒（3-4 周）](#phase-3代碼級-agent--打開黑盒3-4-周)
- [Phase 4：RAG & Memory — 給 Agent 裝上大腦（2-3 周）](#phase-4rag--memory--給-agent-裝上大腦2-3-周)
- [Phase 5：生產級 Agent — 從 Demo 到產品（3-4 周）](#phase-5生產級-agent--從-demo-到產品3-4-周)
- [Phase 6：Multi-Agent & 前沿 — 追平業界（持續）](#phase-6multi-agent--前沿--追平業界持續)
- [學習資源彙總](#-學習資源彙總)
- [常見誤區 & 避坑指南](#-常見誤區--避坑指南)

---

## 快速自測：你現在在哪個階段？

| 你能否做到？ | 如果不能 → 從 Phase 開始 |
|---|---|
| 理解 LLM 的基本原理（Token、上下文窗口、Temperature） | Phase 0 |
| 能手寫一個有效的 System Prompt 讓 AI 按你的意圖輸出 | Phase 0 |
| 在 Coze/Dify 上搭建過一個完整的 Agent Workflow | Phase 2 |
| 用 Python + LangChain 寫過 Agent（含 Tool Calling） | Phase 3 |
| 理解 RAG 的完整 Pipeline 並且自己實現過 | Phase 4 |
| 用 LangGraph 構建過多步驟的有狀態 Agent | Phase 5 |
| 理解 MCP/A2A 協議並能獨立開發 MCP Server | Phase 5 |
| 部署過一個生產可用的 Agent 服務（含監控） | Phase 5 |
| 構建過 Multi-Agent 協作系統 | Phase 6 |

---

## Phase 0：前置知識補漏（1-2 天）

> **目標**：確保你對 LLM 有正確的底層認知，而不是停留在「ChatGPT 很厲害」的表面。

### 學什麼

| 知識點 | 核心問題 | 推薦資源 |
|---|---|---|
| LLM 本質 | 大模型到底是什麼？爲什麼它能"理解"語言？ | [3Blue1Brown 神經網絡](https://www.3blue1brown.com/topics/neural-networks) |
| Token & Tokenizer | 爲什麼中文比英文貴？Token 是怎麼計算的？ | [OpenAI Tokenizer](https://platform.openai.com/tokenizer) |
| Context Window | 上下文窗口是什麼？爲什麼說它是最稀缺的資源？ | [Anthropic Context Windows 指南](https://docs.anthropic.com/en/docs/build-with-claude/context-windows) |
| Temperature & Top-P | 如何控制模型輸出的「創造力」？ | OpenAI/Anthropic 官方文檔 |
| 主流模型對比 | GPT / Claude / Gemini / DeepSeek / Qwen 各自擅長什麼？ | [LMSYS Chatbot Arena](https://chat.lmsys.org/) |

### 練什麼

- [ ] 在 [OpenAI Playground](https://platform.openai.com/playground) 中調整 Temperature 從 0 到 2，觀察同一 Prompt 的輸出差異
- [ ] 用同一個問題測試 GPT-4o / Claude / DeepSeek，寫出對比筆記
- [ ] 計算一段 1000 字中文文本大概消耗多少 Token

### 產出

✅ 一份 **「我的 AI 基礎認知筆記」**（至少包含：LLM 本質理解、模型對比表、Token 計算例子）

---

## Phase 1：Agent 核心心智（1 周）

> **目標**：深刻理解「Agent ≠ Chatbot」的核心差異，掌握 Agent 的思維框架。
>
> **爲什麼這個階段重要**：很多人卡住是因爲把 Agent 當成"更聰明的聊天機器人"——大錯特錯。Agent 的核心是 **自主決策 + 工具使用 + 任務規劃**。

### 學什麼

#### 1.1 Agent 的定義與核心循環

```
┌─────────────────────────────────────┐
│         Agent 核心循環               │
│                                     │
│  感知(Perceive) → 思考(Think) → 行動(Act) → 觀察(Observe) → 循環...  │
│                                     │
└─────────────────────────────────────┘
```

- **Perceive**：獲取環境信息（用戶輸入、工具返回、上下文）
- **Think**：LLM 推理，決定下一步做什麼
- **Act**：調用工具、生成回覆、執行代碼
- **Observe**：獲取行動結果，判斷是否達成目標

#### 1.2 Prompt Engineering for Agents

> 這不是普通的 Prompt Engineering——這是 Agent 的系統指令設計。

| 關鍵元素 | 說明 | 示例 |
|---|---|---|
| Role & Persona | 定義 Agent 的身份和能力邊界 | "你是一個數據分析專家..." |
| Task Definition | 明確的任務目標 | "你需要分析用戶上傳的 CSV 文件..." |
| Tool Descriptions | 告訴模型有哪些工具可用 | "你有以下工具：search_web, run_python, read_file" |
| Constraints & Rules | 行爲約束 | "不要編造數據。如果沒有找到答案，誠實告知。" |
| Output Format | 期望的輸出格式 | "最終回覆使用 Markdown 表格呈現" |

#### 1.3 Function Calling / Tool Use

這是 Agent 和 Chatbot 最大的分水嶺——**Agent 會調用工具**。

**完整流程**：
```
用戶提問 → LLM 判斷需要用哪個工具 → 返回 function_call → 
你的代碼執行這個函數 → 將結果傳回 LLM → LLM 基於結果生成最終回覆
```

### 練什麼

- [ ] 設計一個 Agent 的 System Prompt（角色：旅行規劃助手），包含至少 3 個工具描述
- [ ] 用 curl 或 Python 調用 OpenAI/Anthropic API 的 Function Calling，觀察返回的 `tool_calls`
- [ ] 寫一個小腳本：讓 LLM 決定"現在幾點"時自動調用 `get_current_time()` 函數

### 產出

✅ 一份 **Agent System Prompt 模板** + 一個 **Function Calling 的 Python Demo**

---

## Phase 2：低代碼實戰 — 先做出來再理解（2 周）

> **目標**：在 Coze/Dify 上構建 2-3 個可用的 Agent，建立「我能做出來」的信心。
>
> **爲什麼選低代碼**：直接上手 LangChain 容易迷失在 API 細節裏。先用低代碼平臺理解 Agent 的「感覺」，再回頭寫代碼才能知道自己在做什麼。

### 學什麼

| 平臺 | 定位 | 何時使用 |
|---|---|---|
| [**Coze (釦子)**](https://www.coze.com/) | 字節跳動出品，插件生態豐富 | 快速搭建 + 發佈到飛書/微信 |
| [**Dify**](https://dify.ai/) | 開源，可私有部署，企業級 | 需要私有化部署 + 複雜 Workflow |

**核心概念映射**（低代碼 → 代碼）：
| 低代碼概念 | 對應代碼層概念 |
|---|---|
| Plugin / 插件 | Tool / Function |
| Knowledge / 知識庫 | RAG 的 Indexing + Retrieval |
| Workflow / 工作流 | LangGraph StateGraph |
| Variable / 變量 | State |
| Node / 節點 | LangChain Runnable |

### 練什麼（按順序）

- [ ] **項目 1**：Coze 上搭建一個 **「AI 日報生成器」**
  - 輸入：用戶感興趣的主題
  - 工具：搜索插件 + 大模型
  - 輸出：格式化的日報 Markdown
  - 發佈到飛書 Bot

- [ ] **項目 2**：Dify 上搭建一個 **「智能客服 Agent」**
  - 知識庫：上傳 3-5 份產品文檔
  - 工作流：意圖識別 → 知識檢索 → 答案生成 → 無法回答時轉人工
  - 變量：記錄對話歷史，支持追問

- [ ] **項目 3（選做）**：搭建一個多步驟 Workflow
  - 場景：用戶輸入「幫我分析 XX 公司財報」
  - 步驟：搜索最新財報 → 提取關鍵指標 → 對比行業均值 → 生成分析報告

### 產出

✅ 至少 2 個**可演示的 Agent Bot** + 一份 **「低代碼 vs 代碼開發」對比筆記**

---

## Phase 3：代碼級 Agent — 打開黑盒（3-4 周）

> **目標**：用 Python + LangChain/LangGraph 從零構建 Agent，徹底理解 Agent 內部工作原理。
>
> **這是最關鍵的分水嶺**——過了這個階段，你就是能寫 Agent 的人了。

### 學什麼

#### 3.1 LangChain 核心概念

| 概念 | 一句話解釋 | 
|---|---|
| **Chain** | 把多個步驟串聯起來（A → B → C） |
| **Tool** | 封裝一個能被 Agent 調用的函數 |
| **AgentExecutor** | Agent 的運行時：不斷執行「思考→調用工具→觀察」循環 |
| **Memory** | 讓 Agent 記住之前的對話 |
| **Runnable / LCEL** | LangChain 的聲明式編程接口（`prompt \| llm \| parser`） |
| **Callback** | 在 Agent 運行的每個節點插入自定義邏輯（日誌、監控） |

#### 3.2 用 create_agent 快速起步

```python
# 最簡 Agent — 10 行代碼
from langchain.agents import create_agent

agent = create_agent(
    model="claude-sonnet-4-5-20250929",
    tools=[search_tool, calculator_tool, weather_tool],
    system_prompt="你是一個有用的助手，可以搜索信息、計算數學、查詢天氣。"
)

result = agent.invoke({"messages": [{"role": "user", "content": "北京今天天氣怎麼樣？"}]})
```

#### 3.3 自定義 Tool

```python
from langchain.tools import tool

@tool
def get_stock_price(symbol: str) -> str:
    """獲取指定股票的最新價格。symbol 參數爲股票代碼，如 AAPL、TSLA。"""
    # 實際實現中調用 API
    price = api.get_price(symbol)
    return f"{symbol} 最新價格：${price}"

# Tool description 至關重要！LLM 靠 description 決定是否調用這個工具
```

**Tool Description 最佳實踐**：
- ✅ 明確描述功能和參數
- ✅ 給出參數示例
- ✅ 說明返回格式
- ❌ 不要寫"這個工具可以做任何事情"

#### 3.4 Agent 的四種類型

| 類型 | 工作機制 | 適用場景 |
|---|---|---|
| **ReAct** | Think → Act → Observe 循環 | 通用推理 + 行動 |
| **Plan-and-Execute** | 先規劃再執行 | 複雜多步驟任務 |
| **OpenAI Functions** | 依賴 OpenAI 原生 Function Calling | 簡單直白的工具調用 |
| **Structured Chat** | 支持多參數複雜工具調用 | 需要結構化的輸入輸出 |

### 練什麼（按難度遞增）

- [ ] **練習 1**：Hello Agent — 創建第一個 Agent，帶搜索 + 計算器工具
- [ ] **練習 2**：寫 3 個自定義 Tool（查天氣、查快遞、發郵件），讓 Agent 按需調用
- [ ] **練習 3**：實現 ReAct 循環的完整 Tracing — 每次 Think/Act/Observe 都打日誌
- [ ] **項目 4**：**「AI 代碼助手 Agent」**
  - 工具：讀文件、寫文件、執行 Shell 命令、搜索代碼
  - 能力：用戶說"幫我在項目中找一個 bug"，Agent 自己讀代碼 → 分析 → 修復

### 產出

✅ **Hello Agent Demo** + **自定義 Tool 集合** + **AI 代碼助手 Agent** + **Agent 運行日誌 Tracing Demo**

---

## Phase 4：RAG & Memory — 給 Agent 裝上大腦（2-3 周）

> **目標**：讓 Agent 擁有「知識」和「記憶」，不再是金魚腦。
>
> **核心認知**：RAG 解決「外部知識」，Memory 解決「內部狀態」。

### 學什麼

#### 4.1 RAG 完整 Pipeline

```
離線階段（Indexing）：
文檔 → 分塊(Chunking) → 向量化(Embedding) → 存入向量數據庫

在線階段（Retrieval + Generation）：
用戶提問 → 向量化 → 相似度檢索 → 重排序(Rerank) → 拼接上下文 → LLM 生成答案
```

| 環節 | 關鍵技術 | 常見方案 |
|---|---|---|
| 文檔解析 | PDF/Word/HTML → 純文本 | Unstructured, MinerU, Markitdown |
| 分塊策略 | 怎麼切才能讓檢索更準？ | RecursiveCharacterTextSplitter, Semantic Chunking |
| Embedding | 把文本變成向量 | text-embedding-3-small, bge-m3, jina-embeddings |
| 向量數據庫 | 存向量 + 快速搜索 | Chroma（入門）, Milvus/Qdrant（生產） |
| 檢索策略 | 怎麼搜到對的？ | 混合檢索（向量 + 關鍵詞）, HyDE, Multi-Query |
| Rerank | 搜到後怎麼排序？ | Cohere Rerank, BGE-Reranker |
| 評估 | 檢索到的東西對不對？ | RAGAS（faithfulness, relevancy, precision） |

#### 4.2 Memory 三層架構

```
┌─────────────────┐
│  Working Memory │ ← 當前對話上下文
├─────────────────┤
│ Short-term Mem  │ ← 本次會話歷史
├─────────────────┤
│  Long-term Mem  │ ← 跨會話持久化記憶
└─────────────────┘
```

**關鍵操作**：
- **下沉(sink)**：重要信息從 Working → Long-term
- **上浮(pull)**：檢索 Long-term 中的相關信息到 Working

### 練什麼

- [ ] **練習 1**：用 Chroma + OpenAI Embedding 搭建最小 RAG 系統
  - 上傳 5 篇技術文章 → 能回答相關問題
- [ ] **練習 2**：對比不同分塊策略的檢索效果（固定大小 vs 語義分塊）
- [ ] **練習 3**：給 Agent 加上長期記憶（用 SQLite 存儲對話摘要）
- [ ] **項目 5**：**「個人知識庫 Agent」**
  - 導入你的筆記/文檔 → 自然語言問答
  - 支持追問和上下文關聯
  - 附帶檢索效果評估（RAGAS 評分）

### 產出

✅ **RAG 系統 Demo** + **分塊策略對比報告** + **帶記憶的 Agent**

---

## Phase 5：生產級 Agent — 從 Demo 到產品（3-4 周）

> **目標**：把 Agent 做成一個可以部署、可監控、能應對真實用戶的正經服務。
>
> **這是從「能做」到「能用」的關鍵跨越。**

### 學什麼

#### 5.1 LangGraph — 有狀態的 Agent 工作流

**爲什麼需要 LangGraph**：Chain 是線性的，但真實 Agent 需要分支、循環、條件判斷、人工介入。

```python
from langgraph.graph import StateGraph, START, END

# 核心概念
# State: Agent 的狀態（對話歷史、中間結果、用戶偏好等）
# Node: 一個處理步驟（調用 LLM、執行工具、檢查結果）
# Edge: 連接節點的線（普通邊、條件邊）
# Checkpoint: 狀態的快照（支持暫停/恢復/回溯）
```

#### 5.2 MCP (Model Context Protocol)

> MCP 是 Anthropic 提出的標準協議——讓 Agent 和工具之間用統一的方式通信。

```
┌──────────┐     MCP Protocol     ┌──────────────┐
│  Agent   │ ←──────────────────→ │  MCP Server   │
│ (Client) │   tools/list         │ (工具提供方)  │
│          │   tools/call         │               │
└──────────┘                      └──────────────┘
```

**關鍵認知**：
- MCP Server 可以是你寫的任何服務（數據庫查詢、API 調用、文件操作）
- 一旦寫好 MCP Server，任何支持 MCP 的 Agent 都能直接調用
- Claude Desktop / Cursor / Continue 都支持 MCP

#### 5.3 A2A (Agent-to-Agent Protocol)

> Google 提出的標準——讓不同 Agent 之間互相發現和協作。

MCP vs A2A 的區別：
| | MCP | A2A |
|---|---|---|
| 誰和誰通信 | Agent ↔ Tool | Agent ↔ Agent |
| 解決的問題 | 怎麼調用工具？ | 怎麼讓兩個 Agent 協作？ |

#### 5.4 生產部署 Checklist

| 維度 | 要做什麼 | 工具/方案 |
|---|---|---|
| **部署** | 容器化 + API 服務 | Docker + FastAPI / Flask |
| **安全** | 沙箱隔離、權限控制 | Docker sandbox, API Key 管理 |
| **監控** | Token 用量、響應時間、錯誤率 | LangSmith, LangFuse, Weave |
| **成本** | 緩存策略、模型降級 | 語義緩存(GPTCache)、小模型兜底 |
| **評測** | 回答質量、工具調用準確率 | 人工標註 + 自動評測 + A/B 測試 |
| **流式輸出** | SSE / WebSocket | FastAPI StreamingResponse |

### 練什麼

- [ ] **練習 1**：用 LangGraph 把 Phase 3 的 Agent 改寫成有狀態的 Graph
- [ ] **練習 2**：寫一個 MCP Server（功能：查詢本地文件 + 執行 SQL）
  - 在 Claude Desktop 中加載這個 Server，驗證能用
- [ ] **練習 3**：給你的 Agent 加上完整的監控（LangFuse / LangSmith）
- [ ] **項目 6**：**「生產級客服 Agent」**
  - LangGraph 實現：意圖識別 → 檢索 → 生成 → 不滿意則轉人工
  - FastAPI 部署 + Docker 容器化
  - LangFuse 全鏈路監控
  - 至少處理 50 條真實測試用例，記錄準確率

### 產出

✅ **LangGraph Agent** + **MCP Server** + **部署文檔** + **監控 Dashboard**

---

## Phase 6：Multi-Agent & 前沿 — 追平業界（持續）

> **目標**：構建多 Agent 協作系統，跟蹤前沿，建立持續學習的習慣。

### 學什麼

#### 6.1 Multi-Agent 協作模式

| 模式 | 描述 | 類比 |
|---|---|---|
| **Supervisor** | 一個主 Agent 分配任務給子 Agent | 項目經理 + 執行團隊 |
| **Decentralized** | Agent 之間平等協商 | 團隊 Brainstorming |
| **Hierarchical** | 多層級的 Agent 結構 | 公司組織架構 |
| **Blackboard** | Agent 共享一個數據空間 | 共享白板協作 |

#### 6.2 主流 Multi-Agent 框架

| 框架 | 特點 | 適合場景 |
|---|---|---|
| **CrewAI** | 角色扮演 + 任務分配，最易上手 | 內容創作、市場分析 |
| **AutoGen (Microsoft)** | 對話驅動，支持人機協作 | 研究分析、代碼審查 |
| **LangGraph** | 圖結構，最靈活 | 複雜業務邏輯 |
| **OpenAI Swarm** | 輕量級，適合實驗 | 快速原型 |

#### 6.3 Agent 微調 (Fine-tuning)

> 什麼時候需要微調 Agent？
> - 模型不按你的 System Prompt 行事 → 微調能顯著改善
> - 需要特定領域的專業術語理解
> - 需要固定風格的輸出

**微調方案對比**：

| 方案 | 適用場景 | 成本 |
|---|---|---|
| Prompt Engineering | 簡單行爲約束 | ⭐ 零成本 |
| Few-shot Examples | 格式化輸出 | ⭐ 零成本 |
| SFT + LoRA | 領域適配、行爲對齊 | ⭐⭐⭐ 需 GPU |
| DPO / GRPO | 偏好對齊、質量提升 | ⭐⭐⭐⭐ 需更多計算 |

#### 6.4 前沿追蹤

**2025-2026 年必關注方向**：

| 方向 | 代表工作 | 爲什麼重要 |
|---|---|---|
| **Agentic RL** | GRPO (DeepSeek-R1) | 讓 Agent 通過強化學習自我改進 |
| **Computer Use** | Claude Computer Use, OpenAI Operator | Agent 直接操控電腦 |
| **Code Agent** | Devin, Cursor Agent, Claude Code | AI 程序員正在重塑軟件開發 |
| **Agent Protocol** | MCP, A2A, ANP | Agent 互聯網的 TCP/IP |
| **SWE-bench** | 軟件工程評測基準 | 衡量 Agent 編程能力的標準 |

### 練什麼

- [ ] **項目 7**：**「Multi-Agent 內容創作團隊」**
  - Agent 1（研究員）：搜索 + 整理資料
  - Agent 2（寫手）：根據資料生成文章
  - Agent 3（編輯）：審查 + 潤色
  - Agent 4（審覈員）：最終質量把關
  - 框架：CrewAI 或 LangGraph

- [ ] **項目 8**：**「個人 AI 助手」**
  - 功能：管理日程 + 記錄筆記 + 搜索信息 + 執行自動化任務
  - MCP Server 集成各種個人工具
  - 長期記憶（記住你的偏好和習慣）

- [ ] **持續習慣**：
  - 每週讀 2-3 篇 arXiv Agent 論文
  - 關注 [LMSYS Chatbot Arena](https://chat.lmsys.org/) 排行榜
  - 參與 GitHub 開源 Agent 項目

### 產出

✅ **Multi-Agent 協作系統** + **個人 AI 助手** + **論文閱讀筆記（持續更新）**

---

## Stage 6 延伸：自我進化 Agent 架構師

> **目標**：設計能自我評估、自我改進、自我進化的元 Agent 系統。
>
> **這不再是「Agent 開發」，而是「Agent 進化生態系統的設計」。**

### 核心概念：從「人驅動 Agent」到「Agent 驅動 Agent」

```
傳統 Agent 開發 (Stage 5)：
  人類工程師 → 設計 Prompt → 選擇工具 → 配置評估 → 上線 → 人類監控調優

自我進化 Agent (Stage 6)：
  Meta-Agent → 自動設計子 Agent → 自動評估 → 自動優化 Prompt/Tool → 
  持續監控 → 自我修正 → 越來越強
```

### 六大能力模塊

#### S6.1 自我評估與錯誤修正

基於 **Reflexion** 框架：Agent 分析自己的失敗案例，生成「經驗教訓」存入長期記憶，下次遇到類似場景自動應用。

```python
# Reflexion 僞代碼
def agent_with_reflexion(task):
    result = agent.execute(task)
    if result.failed:
        lesson = agent.analyze_failure(result)  # "我應該先查數據庫再調API"
        memory.store(lesson)                     # 存爲長期經驗
        result = agent.execute(task)             # 重試（這次會參考lesson）
    return result
```

**關鍵技術**：
- 自動迴歸測試：每次修改後跑測試集，發現退化自動回滾
- 信心度校準：Agent 知道何時該請求人工介入
- 失敗模式分類：將錯誤歸類爲「知識不足」「工具缺失」「推理錯誤」等

#### S6.2 自主工具生成

Agent 發現現有工具不足時，**自己寫新工具**並驗證可用性。

```
Agent 執行任務 → 發現缺工具 → 生成工具代碼 → 
驗證 LLM 能否正確調用 → 加入工具庫 → 完成原任務
```

**關鍵指標**：工具生成成功率、LLM 調用準確率、工具使用頻率

#### S6.3 動態 Prompt 優化（DSPy 方向）

不手寫 Prompt，而是讓 Agent **通過測試數據自動搜索最優 Prompt**。

```python
# DSPy 核心思路
import dspy

class MyAgent(dspy.Module):
    def __init__(self):
        self.prompt = dspy.ChainOfThought("question -> answer")
    
    def forward(self, question):
        return self.prompt(question=question)

# 自動優化：跑測試集，找到最佳 Prompt 組合
optimizer = dspy.BootstrapFewShot(metric=accuracy_metric)
optimized_agent = optimizer.compile(MyAgent(), trainset=test_cases)
```

#### S6.4 強化學習驅動的 Agent 訓練

| 技術 | 一句話 | 學習資源 |
|---|---|---|
| **GRPO** | 組內相對比較，無需 Critic 模型（DeepSeek-R1 用的方法） | [DeepSeek-R1 Paper](https://arxiv.org/abs/2501.12948) |
| **DPO** | 偏好對比學習，比 RLHF 更穩定 | [DPO Paper](https://arxiv.org/abs/2305.18290) |
| **RLHF** | 人類反饋強化學習 | [InstructGPT Paper](https://arxiv.org/abs/2203.02155) |

#### S6.5 元 Agent 架構（Meta-Agent）

```
Meta-Agent（設計者 + 評估者 + 優化者）
    │
    ├── Agent 設計器：根據任務自動生成 Agent 配置
    ├── Agent 評估器：自動化 Benchmark，產出效能報告  
    └── Agent 優化器：基於報告自動調整配置
```

#### S6.6 持續學習管道

- **經驗回放**：過往的成功和失敗案例 → 經驗庫
- **課程學習**：簡單任務 → 逐步增加難度
- **災難性遺忘防護**：學新任務不丟舊能力
- **人機迴環**：關鍵決策保留人工審覈，比例隨 Agent 能力提升逐步降低

### 練習項目

- [ ] **項目 9**：**「自我改進的 Code Agent」**
  - 初始 Agent：能做簡單的代碼審查
  - 改進機制：每次審查後自動對比人類反饋，修正自己的審查規則
  - 驗證：對比初始版本和訓練後的版本的審查準確率

- [ ] **項目 10**：**「元 Agent — 自動生成客服 Agent」**
  - 輸入：業務描述（如"處理電商退貨諮詢"）
  - Meta-Agent 自動：設計 Prompt → 配置 RAG → 設置工具 → 測試
  - 輸出：一個可用的客服 Agent + 評估報告

### 產出

✅ **自我改進 Agent Demo** + **Meta-Agent 系統** + **Agent 評估報告**

> 📖 **Stage 6 完整定義、六大核心能力詳解、通過標準、企業價值** → 見 [AI-Lab-成長等級制度.md - Stage 6](./AI-Lab-成長等級制度.md#-stage-6自我進化-agent-架構師-evolution-architect-)

---

## 📚 學習資源彙總

### 必讀開源項目

| 項目 | 簡介 | 階段 |
|---|---|---|
| [liyupi/ai-guide](https://github.com/liyupi/ai-guide) | 魚皮 AI 知識庫，Vibe Coding + AI 工具大全 | Phase 0-1 |
| [Haozhe-Xing/agent_learning](https://github.com/Haozhe-Xing/agent_learning) | 系統性 Agent 學習路線圖，論文精讀 + 交互動畫 | Phase 1-6 |
| [didilili/ai-agents-from-zero](https://github.com/didilili/ai-agents-from-zero) | 企業級實戰教程，含完整項目代碼 | Phase 2-5 |
| [adongwanai/AgentGuide](https://github.com/adongwanai/AgentGuide) | 求職導向 Agent 通關指南，1000+ 面試題 | Phase 5-6 |
| [krishnaik06/Roadmap-To-Learn-Agentic-AI](https://github.com/krishnaik06/Roadmap-To-Learn-Agentic-AI) | Agentic AI 全棧路線（英文） | Phase 1-6 |

### 框架 & 工具

| 工具 | 用途 | 學習難度 |
|---|---|---|
| [Coze](https://www.coze.com/) | 低代碼 Agent 搭建 | ⭐ |
| [Dify](https://dify.ai/) | 開源 Agent 平臺 | ⭐⭐ |
| [LangChain](https://www.langchain.com/) | Python Agent 框架 | ⭐⭐⭐ |
| [LangGraph](https://langchain-ai.github.io/langgraph/) | 有狀態 Agent 工作流 | ⭐⭐⭐⭐ |
| [CrewAI](https://www.crewai.com/) | Multi-Agent 框架 | ⭐⭐⭐ |
| [LangSmith](https://www.langchain.com/langsmith) | Agent 監控 & 調試 | ⭐⭐ |
| [LangFuse](https://langfuse.com/) | 開源 LLM 可觀測性 | ⭐⭐ |

### 必讀論文（按學習階段排列）

| 階段 | 論文 | 核心貢獻 |
|---|---|---|
| Phase 1 | [ReAct](https://arxiv.org/abs/2210.03629) | 推理 + 行動交替的 Agent 框架 |
| Phase 3 | [Toolformer](https://arxiv.org/abs/2302.04761) | 讓 LLM 學會自主使用工具 |
| Phase 4 | [MemGPT](https://arxiv.org/abs/2310.08560) | 給 LLM 操作系統級內存管理 |
| Phase 6 | [AutoGen](https://arxiv.org/abs/2308.08155) | 多 Agent 對話框架 |
| Phase 6 | [DeepSeek-R1 (GRPO)](https://arxiv.org/abs/2501.12948) | 強化學習訓練推理能力 |
| Phase 6 | [SWE-bench](https://arxiv.org/abs/2310.06770) | 軟件工程 Agent 評測基準 |

---

## ⚠️ 常見誤區 & 避坑指南

### 誤區 1：「我先把 LangChain 文檔看完再動手」

**真相**：LangChain 文檔 2000+ 頁，看完你也寫不出 Agent。
**正確做法**：跟着教程先跑通一個 Hello Agent，然後邊做邊查。**20% 的 API 覆蓋 80% 的場景。**

### 誤區 2：「Agent 不就是把 ChatGPT 套個殼嗎」

**真相**：Agent 的核心是 **決策循環 + 工具調用 + 狀態管理**。ChatGPT 套殼是 1 次調用，Agent 是 N 次調用的編排。
**正確做法**：理解 ReAct 循環，理解 Function Calling 的完整流程。

### 誤區 3：「我要用最牛的模型才能做 Agent」

**真相**：Function Calling 能力 GPT-4o-mini 就很好用，DeepSeek-V3 也夠用。貴的模型不一定讓你的 Agent 更好。
**正確做法**：用便宜的模型做開發調試，只在需要複雜推理時切換大模型。

### 誤區 4：「RAG 就是把文檔丟進向量數據庫就行」

**真相**：RAG 的效果 80% 取決於分塊策略和檢索策略。隨便丟進去的 RAG 準確率可能不到 50%。
**正確做法**：花時間調 Chunking Strategy + Rerank + 評測。

### 誤區 5：「學完 LangChain 就夠了，不需要學 LangGraph」

**真相**：LangChain 適合寫 Demo，LangGraph 適合做產品。真實業務需要分支、循環、人工介入——只有 LangGraph 支持。
**正確做法**：學完 LangChain 基礎後立即切到 LangGraph。

### 誤區 6：「先學理論，再做項目」

**真相**：Agent 開發是工程活，不是純理論。最好的學習方式是 **做中學**。
**正確做法**：每個 Phase 都以「做一個能跑的 Project」爲終點。

---

## 📊 每週學習時間建議

| 節奏 | 每週時間 | 適合人羣 | 完成全部路線 |
|---|---|---|---|
| **衝刺型** | 20+ 小時 | 求職/轉行，有時間投入 | 6-8 周 |
| **穩健型** | 10-15 小時 | 在職學習，穩步前進 | 10-14 周 |
| **緩慢型** | 5-8 小時 | 學生/副業探索 | 16-20 周 |

---

## 🎯 最終檢查：你是否真正掌握了？

完成以上所有 Phase 後，你應該能：

- [ ] 獨立從零搭建一個 Agent（選框架、寫工具、部署）
- [ ] 理解 RAG 的每個環節，並根據場景優化
- [ ] 用 LangGraph 設計複雜的有狀態 Agent 工作流
- [ ] 寫一個 MCP Server 並被 Claude Desktop 調用
- [ ] 構建一個 Multi-Agent 協作系統
- [ ] 部署生產級 Agent 服務（含監控和成本控制）
- [ ] 看懂 arXiv 上的 Agent 論文，並能復現核心思想
- [ ] 在面試中講清楚 Agent 的架構設計和技術選型

---

> **最後一句**：Agent 的世界正在以周爲單位進化。這份路線圖是你前進的地圖，但真正的成長來自於 **「把每一個小項目跑通」**。別等看完所有資料——今天就動手。
>
> **Start small. Build fast. Iterate relentlessly.**
