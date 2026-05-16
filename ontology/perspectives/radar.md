# Radar 视角枚举定义

> **视角定位**：生态雷达（Radar）是面向技术决策者的核心视角，用于评估每项技术的**成熟度**与**战略重要性**，帮助团队判断"现在该用什么、该关注什么、该观望什么"。

---

## 字段结构

```json
"radar": {
  "group": "<所属分组>",
  "maturity": "<成熟度等级>",
  "importance": <0-100 重要性分值>
}
```

---

## `maturity` — 成熟度等级

参考 ThoughtWorks Technology Radar 四象限模型，定义如下三个等级：

| 枚举值 | 中文 | 含义 | 行动建议 |
|--------|------|------|---------|
| `adopt` | 采纳 | 技术已成熟，业界广泛验证，可放心用于生产 | **立即采用**，无需犹豫 |
| `trial` | 试用 | 技术有明确价值，但仍在快速演进，需要评估适配成本 | **小范围试点**，积累经验 |
| `assess` | 评估 | 技术有潜力但尚不成熟，值得持续关注 | **跟踪观察**，暂不投入 |

### 各等级代表条目

#### `adopt` — 采纳
| 条目 | 文件 | importance |
|------|------|-----------|
| ChatGPT | application | 98 |
| CUDA | infra | 98 |
| PyTorch | infra | 97 |
| GPT-4o | runtime | 97 |
| Cursor | application | 95 |
| Claude 3.7 Sonnet | runtime | 95 |
| RAG | runtime | 93 |
| vLLM | infra | 92 |
| Gemini 2.5 Pro | runtime | 92 |
| Claude (app) | application | 92 |
| Agentic Loop | orchestration | 88 |
| Gemini (app) | application | 88 |
| Llama 3 | runtime | 88 |
| Perplexity | application | 88 |
| Function Calling | runtime | 88 |
| Antigravity | application | 88 |
| AWS Bedrock | infra | 85 |
| Ollama | infra | 85 |
| DeepSeek R1 | runtime | 85 |
| GitHub Copilot | application | 85 |
| Fine-tuning | runtime | 84 |
| LiteLLM | infra | 83 |
| Dify | orchestration | 83 |
| Milvus | infra | 82 |
| Human-in-the-Loop | orchestration | 82 |
| Temporal | orchestration | 82 |
| Prompt Engineering | runtime | 80 |
| LangSmith | orchestration | 80 |
| Playwright | orchestration | 80 |
| Midjourney | application | 85 |
| Stable Diffusion | application | 82 |
| ElevenLabs | application | 80 |
| Airflow | orchestration | 76 |
| Qdrant | infra | 78 |
| TGI | infra | 78 |
| n8n | orchestration | 78 |
| Context Window | runtime | 86 |
| Chain-of-Thought | runtime | 85 |

#### `trial` — 试用
| 条目 | 文件 | importance |
|------|------|-----------|
| LangGraph | orchestration | 91 |
| MCP | runtime | 92 |
| o3 | runtime | 90 |
| CrewAI | orchestration | 80 |
| Browser Use | orchestration | 79 |
| Prefect | orchestration | 74 |
| Mem0 | runtime | 74 |
| Langfuse | orchestration | 71 |
| Flowise | orchestration | 70 |
| Mistral Large | runtime | 76 |
| Unsloth | infra | 72 |
| Zapier | orchestration | 72 |
| ROCm | infra | 62 |
| Zep | runtime | 66 |

#### `assess` — 评估
| 条目 | 文件 | importance |
|------|------|-----------|
| Stagehand | orchestration | 65 |
| TensorFlow | infra | 70 |
| A2A | runtime | 75 |

---

## `importance` — 重要性分值

取值范围 **0–100**，反映该技术在当前 AI 生态中的战略权重。

| 分值区间 | 等级 | 含义 |
|---------|------|------|
| 90–100 | ⭐⭐⭐⭐⭐ 核心 | 生态基石，不可或缺 |
| 80–89 | ⭐⭐⭐⭐ 重要 | 主流选择，强烈推荐关注 |
| 70–79 | ⭐⭐⭐ 有价值 | 特定场景下有明确价值 |
| 60–69 | ⭐⭐ 边缘 | 小众或早期，谨慎评估 |
| 0–59 | ⭐ 低优先级 | 暂不需要重点投入 |

---

## `group` — 所属分组（按文件）

### Infra
- `GPU & Compute`
- `Model Serving`
- `Training & Fine-tuning`
- `Vector Database`
- `Gateway & Proxy`

### Runtime
- `Frontier Model`
- `Protocol`
- `Memory & Context`
- `Reasoning Paradigms`

### Orchestration
- `Workflow Engine`
- `Agent Orchestration`
- `RPA & Computer Use`
- `Evaluation & Observability`
- `Orchestration Concept`

### Application
- `General Assistant`
- `Coding Assistant`
- `Creative Media`
- `AI Search & Research`
