# 🧭 Stage 1：AI 探索者 (AI Explorer)

> **一句話定義**：掌握提示詞精髓的「超級個體」，能將大語言模型（LLM）的潛能逼到極致，成為職場上的高效特助。

---

## 🎯 等級定位

| 維度 | 內容 |
|---|---|
| **階段定位** | 從「AI 使用者」進化為「AI 駕馭者」的關鍵轉折 |
| **上一階段** | [Stage 0：AI 新手村](./stage-0-ai-novice.md) |
| **下一階段** | [Stage 2：AI 實踐者](./stage-2-ai-implementer.md) |
| **對應 Roadmap** | [Phase 1：Agent 核心心智](../AI-Agent-學習路線圖.md#phase-1agent-核心心智1-周) |
| **建議學習時間** | 1 週（衝刺型）/ 2 週（穩健型） |

### 你在這個階段的畫像

- 你已經能熟練使用 ChatGPT/Claude，不再是「試試看」的階段
- 但你可能發現：有時 AI 的回覆很棒，有時卻很糟——你不知道為什麼
- 你想讓 AI 輸出更一致、更高品質的結果
- **這個階段的目標**：從「被動提問」變成「精準指揮」

---

## 📐 前置條件

- ✅ 已完成 [Stage 0](./stage-0-ai-novice.md) 全部練習
- ✅ 能獨立註冊並使用至少 2 個 AI 平台
- ✅ 理解 Token、Context Window、Temperature、幻覺的基本概念
- ✅ 有 1 份 AI 基礎認知筆記

---

## 🧠 知識點清單

### 1. 進階 Prompt Engineering

#### 1.1 Prompt 結構化框架

```
┌─────────────────────────────────────────┐
│         高品質 Prompt 六要素              │
│                                         │
│  1. Role（角色）：你是誰？               │
│  2. Task（任務）：要做什麼？             │
│  3. Context（背景）：為什麼要做？        │
│  4. Format（格式）：輸出成什麼樣子？     │
│  5. Constraints（約束）：有什麼限制？    │
│  6. Examples（範例）：長什麼樣子？       │
└─────────────────────────────────────────┘
```

**實例對比**：

```
❌ 普通 Prompt：「幫我寫一封 Email」

✅ 結構化 Prompt：
「你是一位專業的專案經理（Role）。
你需要寫一封 Email 給客戶，通知他們專案進度延遲一週（Task）。
原因是供應商物料短缺（Context）。
請使用正式但友善的語氣，控制在 200 字以內（Constraints）。
格式如下：主旨 → 開頭問候 → 說明延遲原因 → 新時程 → 補償方案（Format）。
參考以下語氣範例：（Examples）...」
```

#### 1.2 核心 Prompt 技巧

| 技巧 | 說明 | 何時使用 |
|---|---|---|
| **Chain-of-Thought (CoT)** | 要求 AI「一步步思考」再回答 | 複雜推理、數學問題 |
| **Few-shot Prompting** | 給 AI 2-3 個範例讓它模仿 | 格式化輸出、固定風格 |
| **Role Prompting** | 指定 AI 扮演特定角色 | 專業領域、語境控制 |
| **Structured Output** | 要求 AI 輸出 JSON/Markdown/表格 | 需要程式處理的場景 |
| **Self-Consistency** | 讓 AI 多次回答後投票選最佳 | 需要高準確度的分析 |
| **Tree-of-Thought (ToT)** | 讓 AI 探索多條思路再選擇 | 策略規劃、多方案比較 |

### 2. AI 工作流設計

#### 2.1 單次對話 vs. 工作流思維

| | 單次對話 | 工作流思維 |
|---|---|---|
| **方式** | 一個問題一個回答 | 多步驟串聯處理 |
| **品質** | 依賴單次 Prompt 品質 | 每步驟可控、可調整 |
| **場景** | 簡單問答 | 報告生成、分析、創作 |

#### 2.2 常見 AI 工作流模式

**模式 A：分步處理**
```
原始資料 → AI 整理 → AI 分析 → AI 生成報告 → 人工審核
```

**模式 B：多模型分工**
```
內容草稿(GPT) → 潤色優化(Claude) → 事實查核(Perplexity) → 終稿
```

**模式 C：AI + 人工協作**
```
AI 生成初稿 → 人工修改 → AI 再次優化 → 人工定稿
```

### 3. Agent 的雛形理解

> 在進入 Stage 2 之前，你需要先理解：Agent 不是更聰明的 Chatbot。

| 特徵 | 一般 Chatbot | AI Agent |
|---|---|---|
| 互動次數 | 1 次問答 | 多次往返 |
| 能力範圍 | 只有對話 | 對話 + 調用工具 + 執行程式 |
| 記憶 | 無或很弱 | 有短期/長期記憶 |
| 自主性 | 被動回應 | 主動規劃 + 執行 |

**Agent 核心循環**（先記住這個模式）：
```
感知 → 思考 → 行動 → 觀察結果 → 再思考 → 再行動 → ... → 達成目標
```

---

## 🛠️ 技能要求

### 硬技能

| 技能 | 說明 | 熟練度目標 |
|---|---|---|
| Prompt 設計 | 能獨立寫出結構化、可複用的 Prompt | 熟練 |
| CoT 引導 | 能引導 AI 進行逐步推理 | 掌握 |
| Few-shot 設計 | 能挑選有效範例提升輸出品質 | 掌握 |
| 多模型協作 | 知道何時用哪個模型 | 熟練 |
| Function Calling 認知 | 理解 AI 如何調用外部工具 | 入門 |

### 軟技能

- **精準表達**：能把模糊需求轉化為明確指令
- **迭代調優**：輸出不好時知道如何調整 Prompt
- **品質判斷**：能判斷 AI 輸出的品質好壞

### 推薦工具

| 工具 | 用途 | 費用 |
|---|---|---|
| [ChatGPT](https://chat.openai.com/) | 主力 Prompt 實驗 | 免費/付費 |
| [Claude](https://claude.ai/) | 長文 Prompt 測試 | 免費/付費 |
| [Anthropic Prompt Library](https://docs.anthropic.com/en/prompt-library/library) | Prompt 模板參考 | 免費 |
| [OpenAI Playground](https://platform.openai.com/playground) | 調整 Temperature 等參數 | API 費用 |

---

## 💪 練習項目

### 練習 1：Prompt 改造挑戰（1 小時）

**目標**：將一個「爛 Prompt」改造成「好 Prompt」，感受結構的力量。

```
原始 Prompt：「幫我寫一份市場分析報告」

改造要求：
- 加入 Role（例如：你是資深市場分析師）
- 指定分析對象和範圍
- 定義輸出格式（Markdown 表格 + 分點說明）
- 加入約束（字數、語氣）

比較改造前後的輸出品質，記錄你的發現。
```

### 練習 2：CoT 推理實驗（30 分鐘）

**目標**：體驗 Chain-of-Thought 的力量。

```
問題：「小明有 15 顆蘋果，他給了小華 1/3，又給了小美 2 顆，
最後剩下的蘋果中有一半是壞的。請問小明還有幾顆可以吃的蘋果？」

分別用以下兩種方式提問：
A. 直接問答案
B. 加上「請一步步思考，寫出每個步驟的計算過程」

觀察兩種方式的答案準確度和推理過程。
```

### 練習 3：製作你的第一個 Prompt 模板庫（2 小時）

**目標**：建立一個可複用的 Prompt 模板庫，解決你日常的 3 個真實問題。

```
模板 1：週報生成器
- 輸入：本週工作要點（關鍵字）
- 輸出：結構化週報（完成事項 / 進行中 / 下週計劃 / 遇到的問題）

模板 2：Email 回覆助手
- 輸入：收到的 Email 原文 + 你的回覆意圖
- 輸出：符合語境的正式回信

模板 3：自選場景（如：讀書摘要、會議記錄整理、程式碼解釋）
```

### 練習 4：Function Calling 初體驗（1 小時）

**目標**：親手讓 AI 自動決定「何時需要調用外部函數」。

```python
# 用 Python 呼叫 OpenAI API 的 Function Calling
import openai

tools = [{
    "type": "function",
    "function": {
        "name": "get_current_time",
        "description": "取得目前的日期和時間",
        "parameters": {
            "type": "object",
            "properties": {
                "timezone": {
                    "type": "string",
                    "description": "時區，例如 Asia/Taipei"
                }
            }
        }
    }
}]

response = openai.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "現在幾點？"}],
    tools=tools
)

# 觀察 response 中是否包含 tool_calls
print(response.choices[0].message.tool_calls)
```

---

## 🏅 通過標準

**硬性指標**：

- [ ] 產出 **1 篇**能被社群公用的「結構化高級 Prompt 範本」，用來解決一個真實的辦公/生活痛點
- [ ] Prompt 範本必須包含：Role + Task + Format + Constraints 至少四個元素
- [ ] 能解釋 CoT 的原理，並用一個例子展示效果差異
- [ ] 完成 Prompt 模板庫（至少 3 個模板）
- [ ] 成功運行 Function Calling Demo，並能解釋 AI 決定調用工具的邏輯

**軟性指標**：

- [ ] 能根據 AI 的回覆品質，反過來調整 Prompt（迭代能力）
- [ ] 知道何時用 GPT vs. Claude vs. 其他模型
- [ ] 能判斷 AI 的輸出是否可信（批判性使用）

---

## 🔝 升階條件

**進入 Stage 2 前，你應該能回答以下問題**：

1. 一個好的 Prompt 應該包含哪些元素？為每個元素舉例。
2. CoT 和 Few-shot 分別適用於什麼場景？
3. Function Calling 和一般對話有什麼本質區別？

**下一步有兩個選擇**：

| 路線 | 下一階段 | 說明 |
|---|---|---|
| **技術路線** | [Stage 2：AI 實踐者](./stage-2-ai-implementer.md) | 進入 Vibe Coding，開始做原型 |
| **非技術路線** | 可跳過 Stage 2，直接學習 [Stage 4：流程自動化專家](./stage-4-workflow-specialist.md) | 用自動化工具串接 AI 能力 |

---

## 📚 學習資源

### 免費資源

| 資源 | 簡介 | 連結 |
|---|---|---|
| Anthropic Prompt Library | Claude 官方 Prompt 模板集 | [anthropic.com](https://docs.anthropic.com/en/prompt-library/library) |
| OpenAI Prompt Engineering Guide | 官方提示詞工程指南 | [OpenAI Docs](https://platform.openai.com/docs/guides/prompt-engineering) |
| Learn Prompting | 免費 Prompt Engineering 課程 | [learnprompting.org](https://learnprompting.org/) |
| 魚皮 DeepSeek 提問技巧 | 中文場景 Prompt 實戰 | [ai-guide](https://github.com/liyupi/ai-guide) |

### 推薦論文

| 論文 | 學到什麼 | 連結 |
|---|---|---|
| Chain-of-Thought | CoT 的原理和效果 | [arXiv](https://arxiv.org/abs/2201.11903) |
| ReAct | Agent 推理+行動框架 | [arXiv](https://arxiv.org/abs/2210.03629) |

---

> **給 Stage 1 的你**：Prompt Engineering 是 AI 時代最重要的「程式語言」——不用學語法，但需要學思維。你寫下的每一個 Prompt 都在訓練自己「如何精準地表達需求」，這項能力在任何時代都是稀缺的。
>
> **下一步**：[進入 Stage 2：AI 實踐者](./stage-2-ai-implementer.md)
