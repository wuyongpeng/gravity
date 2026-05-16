# Stack 视角枚举定义

> **视角定位**：技术架构（Stack）视角面向**系统架构师**，描述每项技术在 AI 技术栈中所处的层次位置，帮助理解各组件之间的垂直依赖关系与水平替代关系，构建完整的 AI 系统分层架构图。

---

## 字段结构

```json
"stack": {
  "layer": "<层次标识>"
}
```

---

## `layer` — 层次枚举

整个 AI 技术栈从底层硬件到上层应用，共分为 **10 个层次**，每层包含若干 `layer` 枚举值：

---

### Layer 1 · 硬件计算层 `hardware`

> 直接操控物理计算资源的底层运行时，是整个 AI 栈的算力基础。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `gpu-compute-runtime` | GPU 计算运行时 | CUDA、ROCm | infra |

---

### Layer 2 · 推理服务层 `inference`

> 将模型权重加载并对外提供推理服务的引擎，直接决定吞吐量与延迟。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `inference-server` | 推理服务器 | vLLM、TGI | infra |
| `local-inference-runtime` | 本地推理运行时 | Ollama | infra |

---

### Layer 3 · 训练适配层 `training`

> 负责模型训练、微调与参数优化的框架与工具。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `training-framework` | 训练框架 | PyTorch、TensorFlow | infra |
| `fine-tuning-accelerator` | 微调加速器 | Unsloth | infra |

---

### Layer 4 · 数据存储层 `data`

> 为 AI 系统提供向量检索、知识存储能力的专用数据库。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `vector-store` | 向量存储 | Milvus、Qdrant | infra |

---

### Layer 5 · 网关接入层 `gateway`

> 统一管理模型 API 访问、路由、限流与多云接入的中间层。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `api-gateway` | API 网关 | LiteLLM | infra |
| `managed-cloud-platform` | 托管云平台 | AWS Bedrock | infra |

---

### Layer 6 · 基础模型层 `model`

> 提供核心语言理解与生成能力的大模型，是整个 AI 应用的智能核心。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `foundation-model` | 基础模型 | GPT-4o、Claude 3.7 Sonnet、Gemini 2.5 Pro、Llama 3、Mistral Large | runtime |
| `reasoning-model` | 推理增强模型 | o3、DeepSeek R1 | runtime |

---

### Layer 7 · 协议记忆层 `protocol-memory`

> 标准化模型与外部世界的交互协议，以及跨会话的上下文持久化能力。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `runtime-protocol` | 运行时协议 | MCP | runtime |
| `agent-protocol` | Agent 通信协议 | A2A | runtime |
| `memory-layer` | 记忆层 | Mem0、Zep | runtime |
| `runtime-constraint` | 运行时约束 | Context Window | runtime |

---

### Layer 8 · 推理范式层 `paradigm`

> 定义模型如何思考、检索与使用工具的核心设计模式，是 AI 能力的方法论基础。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `reasoning-pattern` | 推理范式 | RAG、Chain-of-Thought、Prompt Engineering | runtime |
| `tool-use-pattern` | 工具调用范式 | Function Calling | runtime |
| `adaptation-pattern` | 模型适配范式 | Fine-tuning | runtime |

---

### Layer 9 · 编排自动化层 `orchestration`

> 将模型、工具、记忆组合成可执行任务流的编排引擎与自动化平台。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `workflow-runtime` | 工作流运行时 | Temporal、Prefect | orchestration |
| `workflow-scheduler` | 工作流调度器 | Airflow | orchestration |
| `agent-runtime` | Agent 运行时 | LangGraph | orchestration |
| `agent-framework` | Agent 框架 | CrewAI | orchestration |
| `visual-agent-platform` | 可视化 Agent 平台 | Dify | orchestration |
| `visual-agent-builder` | 可视化 Agent 构建器 | Flowise | orchestration |
| `business-automation` | 业务自动化 | n8n、Zapier | orchestration |
| `browser-agent-runtime` | 浏览器 Agent 运行时 | Browser Use | orchestration |
| `browser-agent-sdk` | 浏览器 Agent SDK | Stagehand | orchestration |
| `browser-automation-runtime` | 浏览器自动化运行时 | Playwright | orchestration |
| `llm-observability` | LLM 可观测性 | LangSmith、Langfuse | orchestration |
| `agent-pattern` | Agent 设计模式 | Agentic Loop | orchestration |
| `governance-pattern` | 治理模式 | Human-in-the-Loop | orchestration |

---

### Layer 10 · 应用产品层 `application`

> 直接面向终端用户或开发者交付 AI 价值的产品与平台。

| `layer` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `consumer-ai-product` | 消费级 AI 产品 | ChatGPT、Claude、Gemini | application |
| `ai-developer-tool` | AI 开发者工具 | Cursor、Antigravity、GitHub Copilot | application |
| `creative-ai-platform` | 创意 AI 平台 | Midjourney、ElevenLabs | application |
| `open-weight-generative-model` | 开源生成模型 | Stable Diffusion | application |
| `ai-search-platform` | AI 搜索平台 | Perplexity | application |

---

## 完整层次架构图

```
┌─────────────────────────────────────────────────────────┐
│  Layer 10 · 应用产品层                                    │
│  consumer-ai-product │ ai-developer-tool                 │
│  creative-ai-platform │ ai-search-platform               │
├─────────────────────────────────────────────────────────┤
│  Layer 9 · 编排自动化层                                   │
│  workflow-runtime │ agent-runtime │ agent-framework       │
│  business-automation │ llm-observability                 │
│  browser-agent-runtime │ governance-pattern              │
├─────────────────────────────────────────────────────────┤
│  Layer 8 · 推理范式层                                     │
│  reasoning-pattern │ tool-use-pattern │ adaptation-pattern│
├─────────────────────────────────────────────────────────┤
│  Layer 7 · 协议记忆层                                     │
│  runtime-protocol │ agent-protocol │ memory-layer        │
├─────────────────────────────────────────────────────────┤
│  Layer 6 · 基础模型层                                     │
│  foundation-model │ reasoning-model                      │
├─────────────────────────────────────────────────────────┤
│  Layer 5 · 网关接入层                                     │
│  api-gateway │ managed-cloud-platform                    │
├─────────────────────────────────────────────────────────┤
│  Layer 4 · 数据存储层                                     │
│  vector-store                                            │
├─────────────────────────────────────────────────────────┤
│  Layer 3 · 训练适配层                                     │
│  training-framework │ fine-tuning-accelerator            │
├─────────────────────────────────────────────────────────┤
│  Layer 2 · 推理服务层                                     │
│  inference-server │ local-inference-runtime              │
├─────────────────────────────────────────────────────────┤
│  Layer 1 · 硬件计算层                                     │
│  gpu-compute-runtime                                     │
└─────────────────────────────────────────────────────────┘
```
