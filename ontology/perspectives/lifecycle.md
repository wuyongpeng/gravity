# Lifecycle 视角枚举定义

> **视角定位**：生命周期（Lifecycle）视角面向**AI 工程师与系统设计师**，描述每项技术在 AI 任务处理流水线中所处的阶段，帮助理解数据与请求从输入到输出的完整流转路径，以及各组件在流水线中的职责边界。

---

## 字段结构

```json
"lifecycle": {
  "stage": "<主阶段>",
  "focus": ["<关注点1>", "<关注点2>"]  // 可选，补充说明该阶段的具体能力
}
```

> **说明**：`stage` 描述技术所处的主要流水线阶段；`focus` 是对该阶段内具体能力的补充说明，两者可单独使用或组合使用。

---

## `stage` — 主阶段枚举

AI 任务处理流水线按顺序分为 **9 个主阶段**：

```
input-construction
      ↓
training
      ↓
retrieval
      ↓
context-retrieval
      ↓
reasoning
      ↓
tool-execution
      ↓
agent-coordination / agent-collaboration / agent-loop
      ↓
output-generation / computer-execution
      ↓
monitoring / human-approval
```

---

### Stage 1 · `input-construction` — 输入构建

> 在请求发送给模型之前，对输入内容进行设计、格式化与优化。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `input-construction` | 构建模型输入（Prompt 设计） | Prompt Engineering |

---

### Stage 2 · `training` — 模型训练与适配

> 对模型权重进行更新，包括预训练、微调与强化学习。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `training` | 模型训练与微调 | Fine-tuning |

---

### Stage 3 · `retrieval` — 知识检索

> 从外部知识库或向量数据库中检索相关内容，为模型提供上下文依据。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `retrieval` | 向量检索与知识增强 | RAG |

---

### Stage 4 · `context-retrieval` — 上下文恢复

> 从持久化记忆中恢复跨会话的用户偏好与历史上下文。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `context-retrieval` | 跨会话上下文恢复 | Mem0 |

---

### Stage 5 · `reasoning` — 模型推理

> 模型对输入进行理解、分析与推断，生成中间思考过程或最终答案。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `reasoning` | 模型推理与思考 | o3、Chain-of-Thought |

---

### Stage 6 · `tool-execution` — 工具调用

> 模型通过结构化协议调用外部工具、API 或数据源，扩展自身能力边界。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `tool-execution` | 工具调用与外部集成 | MCP、Function Calling |

---

### Stage 7 · `agent-coordination` / `agent-collaboration` / `agent-loop` — Agent 协作

> 多个 Agent 之间的任务分配、协作执行与循环迭代。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `agent-coordination` | Agent 间任务协调与通信 | LangGraph、A2A |
| `agent-collaboration` | 基于角色的 Agent 协作执行 | CrewAI |
| `agent-loop` | 自主 Agent 的计划-行动-观察循环 | Agentic Loop |
| `pipeline-orchestration` | AI 流水线的整体编排调度 | Prefect |
| `task-execution` | 持久化任务的可靠执行 | Temporal |
| `batch-scheduling` | 批量任务的定时调度 | Airflow |

---

### Stage 8 · `output-generation` / `computer-execution` — 输出执行

> 生成最终输出内容，或通过计算机控制执行具体操作。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `computer-execution` | 通过浏览器/终端执行计算机操作 | Browser Use、Stagehand |

---

### Stage 9 · `monitoring` / `human-approval` — 监控与治理

> 对 AI 系统的运行状态进行追踪、评估，并在关键节点引入人工审核。

| 枚举值 | 含义 | 代表条目 |
|--------|------|---------|
| `monitoring` | 链路追踪、评估与可观测性 | LangSmith、Langfuse |
| `human-approval` | 人工审核与干预检查点 | Human-in-the-Loop |

---

## `focus` — 阶段内关注点枚举

`focus` 是对 `stage` 的细化补充，描述该技术在所处阶段内的具体能力侧重。

### 推理服务类（infra 层）

| `focus` 值 | 含义 | 代表条目 |
|-----------|------|---------|
| `continuous-batching` | 连续批处理推理 | vLLM、TGI |
| `decoding` | Token 解码策略 | vLLM |
| `routing` | 请求路由与负载均衡 | LiteLLM |
| `fallback` | 故障回退与容错 | LiteLLM |

### 模型能力类（runtime 层）

| `focus` 值 | 含义 | 代表条目 |
|-----------|------|---------|
| `extended-thinking` | 扩展思考模式 | Claude (app) |
| `analysis` | 深度文档分析 | Claude (app) |
| `generation` | 内容生成 | Claude (app) |
| `search-augmented` | 搜索增强推理 | Gemini (app) |
| `multimodal-reasoning` | 多模态理解与推理 | Gemini (app) |
| `retrieval` | 知识检索 | Perplexity |
| `citation` | 引用溯源 | Perplexity |

### 编码工具类（application 层）

| `focus` 值 | 含义 | 代表条目 |
|-----------|------|---------|
| `conversation` | 多轮对话管理 | ChatGPT |
| `tool-calling` | 工具调用能力 | ChatGPT |
| `output-generation` | 多模态内容生成 | ChatGPT |
| `multi-file-editing` | 跨文件代码编辑 | Cursor |
| `agentic-loop` | 代码 Agent 循环执行 | Cursor |
| `multi-agent` | 多 Agent 协作编码 | Antigravity |
| `computer-use` | 计算机控制能力 | Antigravity |

---

## 完整流水线阶段图

```
┌─────────────────────────────────────────────────────────────┐
│  Stage 1 · input-construction                               │
│  Prompt Engineering                                         │
├─────────────────────────────────────────────────────────────┤
│  Stage 2 · training                                         │
│  Fine-tuning → [PyTorch / Unsloth]                         │
├─────────────────────────────────────────────────────────────┤
│  Stage 3 · retrieval                                        │
│  RAG → [Milvus / Qdrant]                                   │
├─────────────────────────────────────────────────────────────┤
│  Stage 4 · context-retrieval                                │
│  Mem0 / Zep                                                 │
├─────────────────────────────────────────────────────────────┤
│  Stage 5 · reasoning                                        │
│  o3 / Chain-of-Thought / Claude 3.7 Sonnet                 │
├─────────────────────────────────────────────────────────────┤
│  Stage 6 · tool-execution                                   │
│  MCP / Function Calling                                     │
├─────────────────────────────────────────────────────────────┤
│  Stage 7 · agent-coordination / agent-loop                  │
│  LangGraph / CrewAI / Agentic Loop                         │
│  Temporal / Prefect / Airflow                               │
├─────────────────────────────────────────────────────────────┤
│  Stage 8 · computer-execution                               │
│  Browser Use / Stagehand / Playwright                       │
├─────────────────────────────────────────────────────────────┤
│  Stage 9 · monitoring / human-approval                      │
│  LangSmith / Langfuse / Human-in-the-Loop                  │
└─────────────────────────────────────────────────────────────┘
```
