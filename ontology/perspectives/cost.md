# Cost 视角枚举定义

> **视角定位**：成本（Cost）视角面向**技术决策者与工程负责人**，描述每项技术的定价模型、成本层级与相对成本水平，帮助团队在技术选型时快速评估预算影响、识别隐性成本，并在功能与成本之间做出合理权衡。

---

## 字段结构

```json
"cost": {
  "model": "<定价模型>",
  "tier": "<成本层级>",
  "relative": "<相对成本>",
  "note": "..."   // 可选，补充说明
}
```

> **说明**：`model` 描述收费方式；`tier` 描述入门使用的成本层级；`relative` 是跨类别的相对成本感知；`note` 补充具体定价信息或隐性成本说明。

---

## `model` — 定价模型枚举

共 **11 个枚举值**，覆盖从完全免费到企业订阅的全部定价形态：

| `model` 值 | 中文 | 含义 | 代表条目 |
|-----------|------|------|---------|
| `free` | 完全免费 | 开源或永久免费，无付费计划 | Airflow、Playwright、Stable Diffusion |
| `freemium` | 免费增值 | 有免费层，高级功能付费 | Prefect、Dify、Langfuse、ChatGPT、Claude |
| `open-source` | 开源自托管 | 软件免费，成本为基础设施 | vLLM、Milvus、Qdrant |
| `pay-per-use` | 按量付费 | 按 API 调用量或 Token 计费 | GPT-4o、Claude 3.7、Gemini 2.5 Pro |
| `subscription` | 订阅制 | 按月/年固定费用 | Midjourney、Zapier |
| `capex` | 资本支出 | 一次性硬件采购，无持续费用 | H100、H200、A100、Apple Silicon |
| `self-hosted` | 自托管基础设施 | 软件免费，成本为服务器/云资源 | LangGraph、CrewAI、Flowise |
| `infrastructure` | 基础设施成本 | 按计算资源消耗计费 | AWS Bedrock、Google TPU v5 |
| `token-overhead` | Token 消耗开销 | 每次循环消耗 LLM Token，成本随迭代累积 | Agentic Loop |
| `human-effort` | 人力成本 | 主要成本为人工审核时间 | Human-in-the-Loop |
| `compute-intensive` | 计算密集型 | 训练/推理需要大量 GPU 算力 | Fine-tuning |

---

## `tier` — 成本层级枚举

描述**入门使用**时的成本门槛：

| `tier` 值 | 中文 | 含义 | 典型场景 |
|----------|------|------|---------|
| `free` | 免费 | 零成本可开始使用 | 开源工具、免费层产品 |
| `standard` | 标准 | 个人/小团队付费层，通常 $10-50/月 | SaaS 工具标准订阅 |
| `premium` | 高级 | 专业用户付费层，通常 $50-200/月 | 高级功能或更高配额 |
| `enterprise` | 企业 | 企业定制定价，通常需要商务洽谈 | 大规模部署、合规需求 |
| `variable` | 可变 | 成本随使用量或场景动态变化 | 按量计费、人力成本 |

---

## `relative` — 相对成本枚举

跨类别的**主观成本感知**，用于快速比较：

| `relative` 值 | 中文 | 含义 | 典型条目 |
|--------------|------|------|---------|
| `low` | 低 | 几乎无成本或极低成本 | 开源工具、免费层 |
| `medium` | 中 | 有一定成本，在合理预算范围内 | 标准 SaaS 订阅、中端 API |
| `high` | 高 | 成本显著，需要预算规划 | 高端 API、专业订阅 |
| `very-high` | 极高 | 成本极高，需要专项预算 | 高端 GPU 硬件、大规模训练 |

---

## 各层成本分布

### Hardware 层（物理加速器）

| 条目 | model | tier | relative | 说明 |
|------|-------|------|----------|------|
| H100 | `capex` | `enterprise` | `very-high` | 单卡 $25,000-35,000；云端 $2-4/小时 |
| H200 | `capex` | `enterprise` | `very-high` | 单卡 $35,000+；云端 $3-5/小时 |
| A100 | `capex` | `enterprise` | `high` | 单卡 $10,000-15,000；云端 $1-3/小时 |
| Apple Silicon | `capex` | `standard` | `medium` | M4 Max MacBook Pro ~$3,999 起 |
| Google TPU v5 | `infrastructure` | `enterprise` | `very-high` | 仅通过 Google Cloud 按需计费 |
| Groq LPU | `pay-per-use` | `standard` | `medium` | 按 Token 计费，推理速度极快 |

### Infra 层（基础设施）

| 条目 | model | tier | relative | 说明 |
|------|-------|------|----------|------|
| vLLM | `open-source` | `free` | `low` | 开源免费；成本为 GPU 基础设施 |
| TGI | `open-source` | `free` | `low` | 开源免费；HuggingFace 托管版按量计费 |
| Ollama | `free` | `free` | `low` | 完全免费；本地运行 |
| PyTorch | `free` | `free` | `low` | 开源免费；训练成本为 GPU 算力 |
| Unsloth | `freemium` | `free` | `low` | 开源版免费；Pro 版付费 |
| Milvus | `open-source` | `free` | `low` | 开源免费；Zilliz Cloud 托管版按量计费 |
| Qdrant | `open-source` | `free` | `low` | 开源免费；Qdrant Cloud 有免费层 |
| LiteLLM | `open-source` | `free` | `low` | 开源免费；Enterprise 版付费 |
| AWS Bedrock | `pay-per-use` | `variable` | `medium` | 按 Token 计费；无最低消费 |
| CUDA | `free` | `free` | `low` | 免费工具包；成本为 NVIDIA GPU 硬件 |
| ROCm | `free` | `free` | `low` | 完全开源免费 |
| TensorFlow | `free` | `free` | `low` | 开源免费 |

### Runtime 层（模型运行时）

| 条目 | model | tier | relative | 说明 |
|------|-------|------|----------|------|
| GPT-4o | `pay-per-use` | `standard` | `medium` | $2.50/1M input tokens；$10/1M output tokens |
| o3 | `pay-per-use` | `premium` | `high` | $10/1M input tokens；$40/1M output tokens |
| Claude 3.7 Sonnet | `pay-per-use` | `standard` | `medium` | $3/1M input tokens；$15/1M output tokens |
| Gemini 2.5 Pro | `pay-per-use` | `standard` | `medium` | $1.25/1M input tokens（≤200K） |
| Llama 3 | `free` | `free` | `low` | 开源权重免费；推理成本为自托管算力 |
| Mistral Large | `pay-per-use` | `standard` | `medium` | $2/1M input tokens；$6/1M output tokens |
| DeepSeek R1 | `pay-per-use` | `standard` | `low` | $0.55/1M input tokens；极具成本优势 |
| MCP | `free` | `free` | `low` | 开放协议，免费使用 |
| A2A | `free` | `free` | `low` | 开放协议，免费使用 |
| Mem0 | `freemium` | `free` | `low` | 开源版免费；Cloud 版按使用量计费 |
| Zep | `freemium` | `free` | `low` | 开源版免费；Cloud 版按月计费 |
| Context Window | `token-based` | `variable` | `medium` | 成本随上下文长度线性增长 |

### Patterns 层（推理范式）

| 条目 | model | tier | relative | 说明 |
|------|-------|------|----------|------|
| RAG | `infrastructure` | `variable` | `medium` | 向量存储 + 检索 + LLM 调用的综合成本 |
| Chain-of-Thought | `token-overhead` | `variable` | `medium` | 增加推理步骤导致 Token 消耗增加 2-5x |
| Prompt Engineering | `human-effort` | `free` | `low` | 主要成本为工程师时间，无直接费用 |
| Function Calling | `token-overhead` | `variable` | `medium` | 工具描述占用 Token；多轮调用累积成本 |
| Fine-tuning | `compute-intensive` | `enterprise` | `very-high` | 训练成本 $100-10,000+；取决于数据量和模型规模 |

### Orchestration 层（编排）

| 条目 | model | tier | relative | 说明 |
|------|-------|------|----------|------|
| Temporal | `freemium` | `free` | `low` | 开源自托管免费；Cloud 版 ~$0.00025/action |
| Prefect | `freemium` | `free` | `low` | 开源免费；Cloud 免费层 + Pro 付费 |
| Airflow | `free` | `free` | `low` | Apache 开源；成本为基础设施 |
| LangGraph | `free` | `free` | `low` | 开源库免费；LangGraph Cloud 托管版付费 |
| CrewAI | `freemium` | `free` | `low` | 开源免费；Enterprise 版付费 |
| Dify | `freemium` | `free` | `low` | 开源自托管免费；Cloud 版有免费层 |
| Flowise | `free` | `free` | `low` | 完全开源免费 |
| n8n | `freemium` | `free` | `low` | 自托管免费；Cloud 版从 $20/月起 |
| Zapier | `subscription` | `standard` | `medium` | 免费层 100 tasks/月；付费从 $19.99/月 |
| Browser Use | `free` | `free` | `low` | 开源免费；成本为 LLM API 调用 |
| Stagehand | `freemium` | `standard` | `medium` | SDK 开源免费；Browserbase Cloud 托管付费 |
| Playwright | `free` | `free` | `low` | 完全开源免费 |
| LangSmith | `freemium` | `standard` | `medium` | 免费层 5k traces/月；Developer $39/月 |
| Langfuse | `freemium` | `free` | `low` | 开源自托管免费；Cloud 版有免费层 |
| Agentic Loop | `token-overhead` | `variable` | `high` | 每次迭代消耗 LLM Token；失控循环成本极高 |
| Human-in-the-Loop | `human-effort` | `variable` | `medium` | 人工审核时间成本；降低自动化 ROI |

### Application 层（终端产品）

| 条目 | model | tier | relative | 说明 |
|------|-------|------|----------|------|
| ChatGPT | `freemium` | `free` | `low` | 免费层可用；Plus $20/月；Enterprise 定制 |
| Claude | `freemium` | `free` | `low` | 免费层可用；Pro $20/月 |
| Gemini | `freemium` | `free` | `low` | 免费层可用；Advanced $19.99/月 |
| Cursor | `freemium` | `standard` | `medium` | 免费层有限；Pro $20/月；Business $40/用户/月 |
| Antigravity | `freemium` | `standard` | `medium` | 免费层可用；高级 Agent 功能付费 |
| GitHub Copilot | `freemium` | `standard` | `medium` | 学生/OSS 免费；Individual $10/月；Business $19/用户/月 |
| Midjourney | `subscription` | `standard` | `medium` | Basic $10/月；Standard $30/月；Pro $60/月 |
| Stable Diffusion | `free` | `free` | `low` | 开源权重免费；成本为 GPU 算力 |
| ElevenLabs | `freemium` | `free` | `medium` | 免费层 10k chars/月；Creator $22/月 |
| Perplexity | `freemium` | `free` | `low` | 免费层可用；Pro $20/月 |

---

## 成本决策框架

### 选型成本优先级规则

1. **原型验证阶段** → 优先选择 `tier: free` 的工具，控制前期投入
2. **生产部署阶段** → 评估 `model: pay-per-use` vs `subscription` 的盈亏平衡点
3. **数据主权要求** → 选择 `model: open-source` / `self-hosted`，以基础设施成本换取数据控制权
4. **高频调用场景** → 关注 `relative: low` 的模型（如 DeepSeek R1），避免 Token 成本失控
5. **Agent 循环场景** → 特别注意 `model: token-overhead` 条目，设置 Token 预算上限

### 隐性成本识别

| 隐性成本类型 | 涉及条目 | 风险说明 |
|------------|---------|---------|
| **Token 累积** | Agentic Loop、Chain-of-Thought、Function Calling | 多轮迭代导致成本指数级增长 |
| **基础设施运维** | 所有 `self-hosted` 条目 | 需要 DevOps 人力维护 |
| **GPU 闲置** | H100、H200、A100 | 低利用率时资本支出浪费 |
| **数据传输** | AWS Bedrock、LangSmith | 跨区域数据传输额外计费 |
| **人工审核** | Human-in-the-Loop | 规模化时人力成本显著 |

---

## 成本 vs 能力权衡矩阵

```
                    relative cost
                low        medium       high      very-high
               ┌──────────┬──────────┬──────────┬──────────┐
  capability   │ Llama 3  │ GPT-4o   │ o3       │ H100     │
  = high       │ DeepSeek │ Claude   │ Fine-tune│ H200     │
               │ Airflow  │ Cursor   │          │          │
               ├──────────┼──────────┼──────────┼──────────┤
  capability   │ Flowise  │ Zapier   │          │          │
  = medium     │ n8n      │ Stagehand│          │          │
               │ Langfuse │ LangSmith│          │          │
               └──────────┴──────────┴──────────┴──────────┘
```

> **最优选择区间**：`capability: high` + `relative: low` — 以 DeepSeek R1、Llama 3 为代表的高性价比选项。
