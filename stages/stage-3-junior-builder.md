# 🛠️ Stage 3：初階 AI 建造者 (Junior AI Builder)

> **一句話定義**：具備完整軟體交付能力的初階造物者。能真正打通應用的任督二脈，讓產品不再只是 Demo，而是能存檔、能運作的真實系統。

---

## 🎯 等級定位

| 維度 | 內容 |
|---|---|
| **階段定位** | **最關鍵的分水嶺**——從「AI 輔助玩玩」到「獨立交付產品」 |
| **上一階段** | [Stage 2：AI 實踐者](./stage-2-ai-implementer.md) |
| **下一階段** | [Stage 5：高階 AI 架構師](./stage-5-senior-builder.md) 或 [Stage 4](./stage-4-workflow-specialist.md) |
| **對應 Roadmap** | [Phase 3：代碼級 Agent](../AI-Agent-學習路線圖.md#phase-3代碼級-agent--打開黑盒3-4-周) |
| **建議學習時間** | 3-4 週（衝刺型）/ 5-8 週（穩健型） |

### 你在這個階段的畫像

- 你已經能用 Vibe Coding 做出原型，但想做更複雜的東西
- 你發現 AI 生成的程式碼有時需要手動調整才能跑
- 你想讓應用「真的能用」：有登入、能存資料、別人也能訪問
- **這個階段的目標**：掌握全棧開發 + LangChain Agent，獨立交付完整系統

---

## 📐 前置條件

- ✅ 已完成 [Stage 2](./stage-2-ai-implementer.md)
- ✅ 用 v0/bolt.new 至少做過 1 個產品原型
- ✅ 能看懂基本的 HTML / CSS / JavaScript 程式碼（不需要手寫）
- ✅ 有 GitHub 帳號並知道基本的 git 指令
- ✅ Python 環境已安裝（建議 3.10+）

---

## 🧠 知識點清單

### 1. 全棧開發基礎（AI 輔助學習）

| 層級 | 技術選項 | 你需要學到什麼程度 |
|---|---|---|
| **前端框架** | React（推薦）/ Vue / Next.js | 能看懂元件結構，會用 AI 修改 |
| **後端** | Node.js + Express / Python + FastAPI | 能搭建 REST API，處理請求 |
| **資料庫** | Supabase（推薦）/ PostgreSQL / MongoDB | 能建表、CRUD 操作 |
| **部署** | Vercel（前端）/ Render（後端） | 能把應用放上線，綁定域名 |
| **身份驗證** | Clerk / Supabase Auth | 能加入登入/註冊功能 |

**AI 輔助全棧開發心法**：
```
1. 先問 AI：「幫我設計這個應用的架構，包含前端、後端、資料庫怎麼分工」
2. 再分段實現：「先幫我做登入功能的前端」
3. 遇到錯誤：直接把錯誤訊息丟給 AI，它會幫你修
4. 關鍵原則：了解每一層在做什麼，但不需要熟記語法
```

### 2. Python + LangChain Agent 開發

#### 2.1 LangChain 核心概念

| 概念 | 一句話解釋 |
|---|---|
| **Chain** | 把多個步驟串聯（A → B → C） |
| **Tool** | 封裝一個能被 Agent 呼叫的函數 |
| **AgentExecutor** | Agent 的執行時：不斷執行「思考→呼叫工具→觀察」循環 |
| **Memory** | 讓 Agent 記住之前的對話 |
| **Runnable / LCEL** | LangChain 的宣告式程式設計介面 |
| **Callback** | 在 Agent 執行的每個節點插入自定義邏輯 |

#### 2.2 第一個 Agent（10 行程式碼）

```python
from langchain.agents import create_agent

agent = create_agent(
    model="claude-sonnet-4-5-20250929",
    tools=[search_tool, calculator_tool, weather_tool],
    system_prompt="你是一個有用的助手，可以搜尋資訊、計算數學、查詢天氣。"
)

result = agent.invoke({
    "messages": [{"role": "user", "content": "台北今天天氣怎麼樣？"}]
})
```

#### 2.3 自定義 Tool

```python
from langchain.tools import tool

@tool
def get_stock_price(symbol: str) -> str:
    """獲取指定股票的最新價格。
    
    Args:
        symbol: 股票代碼，如 AAPL、TSLA、2330.TW
    """
    price = api.get_price(symbol)
    return f"{symbol} 最新價格：${price}"
```

**Tool Description 最佳實踐**：
- ✅ 明確描述功能和參數
- ✅ 給出參數範例
- ✅ 說明回傳格式
- ❌ 不要寫「這個工具可以做任何事情」

#### 2.4 Agent 的四種類型

| 類型 | 工作機制 | 適用場景 |
|---|---|---|
| **ReAct** | Think → Act → Observe 循環 | 通用推理 + 行動 |
| **Plan-and-Execute** | 先規劃再執行 | 複雜多步驟任務 |
| **OpenAI Functions** | 依賴 OpenAI 原生 Function Calling | 簡單直白的工具呼叫 |
| **Structured Chat** | 支援多參數複雜工具呼叫 | 結構化輸入輸出 |

#### 2.5 Function Calling 完整流程

```
使用者提問 → LLM 判斷需要用哪個工具 → 回傳 function_call →
你的程式碼執行這個函數 → 將結果傳回 LLM → LLM 基於結果生成最終回覆
```

---

## 🛠️ 技能要求

### 硬技能

| 技能 | 說明 | 熟練度目標 |
|---|---|---|
| Python 基礎 | 變數、函數、類別、async/await | 掌握 |
| LangChain | Chain、Tool、AgentExecutor、Memory | 熟練 |
| FastAPI / Node.js | 搭建 REST API | 掌握 |
| SQL 基礎 | SELECT、INSERT、UPDATE、DELETE | 掌握 |
| Git 操作 | branch、merge、pull request | 掌握 |
| 部署 | Docker 基礎、雲端部署 | 入門 |
| 環境變數管理 | API Key 安全存放 | 掌握 |

### 軟技能

- **問題分解**：能將大需求拆成小步驟
- **錯誤排查**：看到報錯不慌張，會系統性找原因
- **技術選型**：知道何時用哪種技術棧

### 推薦工具

| 工具 | 用途 | 費用 |
|---|---|---|
| [Cursor](https://cursor.sh/) | AI 輔助程式編輯器 | 免費/付費 |
| [LangChain](https://www.langchain.com/) | Python Agent 框架 | 免費開源 |
| [Supabase](https://supabase.com/) | 後端即服務（資料庫+認證） | 免費/付費 |
| [Vercel](https://vercel.com/) | 前端部署 | 免費/付費 |
| [Render](https://render.com/) | 後端部署 | 免費/付費 |
| [Docker](https://www.docker.com/) | 容器化 | 免費 |

---

## 💪 練習項目

### 練習 1：Hello Agent（1 小時）

**目標**：用 LangChain 建立第一個會用工具的 Agent。

```python
from langchain.agents import create_agent
from langchain.tools import tool
import math

@tool
def calculator(expression: str) -> str:
    """計算數學表達式。例如：'2+2'、'sqrt(16)'、'100*3.14'"""
    try:
        result = eval(expression, {"__builtins__": {}}, {"sqrt": math.sqrt})
        return f"計算結果：{result}"
    except Exception as e:
        return f"計算錯誤：{e}"

agent = create_agent(
    model="gpt-4o-mini",
    tools=[calculator],
    system_prompt="你是一個數學助手，可以用計算機工具。"
)

result = agent.invoke({
    "messages": [{"role": "user", "content": "圓面積，半徑 5 公分是多少？"}]
})
print(result["messages"][-1].content)
```

### 練習 2：寫 3 個自定義 Tool（2 小時）

**目標**：建立一套可被 Agent 呼叫的工具集。

```
Tool 1：天氣查詢（模擬 API 呼叫）
Tool 2：翻譯工具（呼叫翻譯 API）
Tool 3：檔案讀取（讀取本地文字檔）

要求：
- 每個 Tool 有清晰的 description
- 讓 Agent 在一個對話中依序使用這三個工具
- 記錄 Agent 每次「思考→呼叫工具→觀察結果」的過程
```

### 練習 3：ReAct 循環 Tracing（1.5 小時）

**目標**：理解 Agent 內部決策過程。

```
為練習 1 的 Agent 加上詳細的 Logging：
- 每一步 Agent 的「思考」輸出
- 每一次「呼叫工具」的決定和參數
- 每一次「觀察工具結果」
- 最終輸出的生成

把這些 Log 整理成 Markdown 表格，分析 Agent 的決策路徑。
```

### 練習 4（專案 A）：AI 程式碼助手 Agent（4 小時）

**目標**：做一個能分析程式碼的 Agent。

```
工具集：
- read_file：讀取檔案
- search_code：搜尋程式碼關鍵字
- run_shell：執行指令（需安全沙箱）
- explain_code：用 LLM 解釋一段程式碼

能力：使用者說「幫我找到這個專案裡所有 API 呼叫的地方，檢查有沒有錯誤處理」
Agent 自己：讀檔案 → 搜尋 → 分析 → 回報結果
```

### 練習 5（專案 B）：第一個全棧應用（8 小時）

**目標**：用 AI 輔助，從零打造一個完整的全棧應用。

```
要求（全部用 AI 輔助完成，但你要理解每一層在做什麼）：

功能：簡單的筆記應用
- 前端：React + Tailwind CSS
- 後端：FastAPI (Python)
- 資料庫：Supabase (PostgreSQL)
- 認證：Supabase Auth（Google 登入）
- 部署：前端 Vercel + 後端 Render

使用者可以：註冊 → 登入 → 新增/編輯/刪除筆記
```

---

## 🏅 通過標準

**硬性指標**：

- [ ] 成功建構 **2 個**完整的實戰專案
- [ ] 每個專案必須包含：**前端 + 後端 + Database + 成功部署**
- [ ] 產出的外部連結任何人都可以公開訪問與使用
- [ ] 至少 1 個專案使用了 LangChain Agent + 自定義 Tool
- [ ] 專案程式碼放在 GitHub 公開倉庫，有 README 說明

**軟性指標**：

- [ ] 能解釋 Agent 的 ReAct 循環是怎麼運作的
- [ ] 能從零開始設定一個 Python 專案並安裝 LangChain
- [ ] 看到報錯訊息時，知道怎麼用 AI 輔助排查

---

## 🔝 升階條件

**進入下一階段前，你應該能回答以下問題**：

1. LangChain 的 Chain 和 Agent 有什麼不同？各自適合什麼場景？
2. 你的 Agent 呼叫 Tool 失敗時，你會怎麼設計錯誤處理？
3. 如果要讓你的全棧應用同時服務 1000 個使用者，現有架構需要改什麼？

**下一步路線選擇**：

| 路線 | 下一階段 | 說明 |
|---|---|---|
| **Agent 深度路線** | [Stage 5：高階 AI 架構師](./stage-5-senior-builder.md) | 直接進入 RAG + Multi-Agent 系統 |
| **自動化路線** | [Stage 4：流程自動化專家](./stage-4-workflow-specialist.md) | 用低代碼解決企業流程問題 |
| **雙刀流** | Stage 4 + Stage 5 並行 | 完整能力覆蓋，但時間投入最大 |

---

## 📚 學習資源

### 免費資源

| 資源 | 簡介 | 連結 |
|---|---|---|
| LangChain 官方文件 | Agent 開發最完整的參考 | [langchain.com](https://python.langchain.com/) |
| didilili/ai-agents-from-zero | 企業級實戰教程，含完整專案程式碼 | [GitHub](https://github.com/didilili/ai-agents-from-zero) |
| Haozhe-Xing/agent_learning | 系統性 Agent 學習路線圖 | [GitHub](https://github.com/Haozhe-Xing/agent_learning) |
| FastAPI 官方文件 | 現代 Python API 框架 | [fastapi.tiangolo.com](https://fastapi.tiangolo.com/) |
| Supabase 文件 | 後端即服務平台 | [supabase.com](https://supabase.com/docs) |

### 推薦論文

| 論文 | 學到什麼 | 連結 |
|---|---|---|
| ReAct | 推理+行動交替的 Agent 框架 | [arXiv](https://arxiv.org/abs/2210.03629) |
| Toolformer | 讓 LLM 學會自主使用工具 | [arXiv](https://arxiv.org/abs/2302.04761) |

---

> **給 Stage 3 的你**：這是整條路線圖中**最重要的階段**。過了這關，你就不再是「用 AI 做東西的人」，而是「能用程式碼讓 AI 做任何事的人」。兩個全棧專案聽起來很多，但善用 AI 輔助，你會發現比想像中快——重點不是寫多少程式碼，而是理解多少架構。
>
> **下一步**：[進入 Stage 4：流程自動化專家](./stage-4-workflow-specialist.md) 或 [Stage 5：高階 AI 架構師](./stage-5-senior-builder.md)
