# Strategy 视角枚举定义

> **视角定位**：战略（Strategy）视角面向**技术决策者与架构负责人**，描述每项技术在 AI 技术栈中的**战略定位**，回答"为什么选择它"而非"它是什么"。帮助决策者在技术选型时快速识别每个工具的核心差异化价值、替代关系与战略风险。

---

## 字段结构

```json
"decision": {
  "positioning": "<定位标识>"
}
```

> **说明**：`positioning` 是对该技术战略角色的单一最优描述，每个条目有且仅有一个值。它与 `radar.maturity` 共同构成技术选型的决策依据：`maturity` 描述**采用成熟度**，`positioning` 描述**战略角色**。

---

## `positioning` — 战略定位枚举

战略定位按 AI 技术栈的四个类别分组，共覆盖 **4 个类别 · 50 个定位值**：

---

### Category A · 基础设施（Infra）

> 面向**平台工程师与 MLOps 团队**，描述计算、存储与服务层的战略选择逻辑。

#### A1 · GPU 计算层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `gpu-compute-standard` | GPU 计算行业标准 | CUDA | 无可替代的基础设施，生态锁定风险高但切换成本极高 |
| `open-gpu-alternative` | 开源 GPU 替代方案 | ROCm | CUDA 的开源替代，适合 AMD 硬件或规避 NVIDIA 锁定 |

#### A2 · 推理服务层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `high-throughput-serving` | 高吞吐推理服务首选 | vLLM | 生产级开源推理引擎，PagedAttention 技术领先 |
| `huggingface-native-serving` | HuggingFace 生态原生服务 | TGI | 与 HuggingFace 模型库深度集成，适合 HF 生态用户 |
| `local-dev-standard` | 本地开发标准工具 | Ollama | 开发者本地原型验证的事实标准，极低门槛 |

#### A3 · 训练适配层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `training-framework-standard` | 训练框架行业标准 | PyTorch | 研究与生产的统一框架，生态最完整 |
| `legacy-training-framework` | 遗留训练框架 | TensorFlow | 维护期框架，不推荐新项目，存量系统可继续使用 |
| `efficient-finetuning` | 高效微调加速器 | Unsloth | 显著降低微调硬件门槛，LoRA 训练提速 2-5x |

#### A4 · 数据存储层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `billion-scale-vector-store` | 十亿级向量存储 | Milvus | 生产级大规模向量检索，适合企业级 RAG 场景 |
| `low-latency-vector-store` | 低延迟向量存储 | Qdrant | 高性能向量检索，Payload 过滤能力强 |

#### A5 · 网关接入层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `unified-llm-gateway` | 统一 LLM API 网关 | LiteLLM | 多模型路由标准，避免单一供应商锁定 |
| `managed-cloud-ai-platform` | 托管云 AI 平台 | AWS Bedrock | 企业级安全合规，适合已在 AWS 生态的组织 |

---

### Category B · 运行时（Runtime）

> 面向**AI 工程师与模型集成团队**，描述模型选型、协议标准与推理范式的战略选择逻辑。

#### B1 · 前沿模型层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `general-purpose-api-standard` | 通用 API 集成标准 | GPT-4o | 最广泛集成的模型，生态兼容性最佳 |
| `high-reasoning-model` | 高推理能力模型 | o3 | 复杂问题求解首选，成本高但准确率领先 |
| `agentic-coding-leader` | Agentic 编码领域领导者 | Claude 3.7 Sonnet | 长上下文与代码 Agent 场景最优选择 |
| `long-context-leader` | 超长上下文处理领导者 | Gemini 2.5 Pro | 百万 Token 上下文，长文档理解场景首选 |
| `open-weight-standard` | 开源权重模型标准 | Llama 3 | 自托管与微调场景的基础模型首选 |
| `efficient-inference-model` | 高效推理模型 | Mistral Large | 性能与成本均衡，适合高频 API 调用场景 |
| `open-reasoning-model` | 开源推理模型 | DeepSeek R1 | 成本效益最优的推理模型，适合预算敏感场景 |

#### B2 · 协议标准层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `tool-use-standard` | 工具调用协议标准 | MCP | Anthropic 主导的工具集成标准，生态快速扩张 |
| `agent-communication-protocol` | Agent 通信协议 | A2A | Google 主导的多 Agent 通信标准，观望期 |

#### B3 · 记忆上下文层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `agent-memory-layer` | Agent 持久化记忆层 | Mem0 | 跨会话用户记忆的核心基础设施 |
| `temporal-memory-store` | 时序对话记忆存储 | Zep | 具备时间推理能力的对话历史管理 |
| `context-constraint-awareness` | 上下文约束感知 | Context Window | 所有长上下文架构决策的核心约束 |

#### B4 · 推理范式层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `hallucination-reduction-pattern` | 减少幻觉的核心模式 | RAG | 知识密集型场景的标准架构模式 |
| `step-by-step-reasoning-pattern` | 逐步推理核心模式 | Chain-of-Thought | 复杂推理任务的基础提示技术 |
| `tool-invocation-pattern` | 工具调用基础模式 | Function Calling | 所有工具调用 Agent 的底层机制 |
| `human-ai-control-layer` | 人机交互控制层 | Prompt Engineering | 提升输出质量与可控性的核心技能 |
| `domain-customization` | 领域定制化路径 | Fine-tuning | 垂直领域模型适配的核心技术路径 |

---

### Category C · 编排（Orchestration）

> 面向**AI 产品工程师与自动化架构师**，描述工作流、Agent 框架与可观测性的战略选择逻辑。

#### C1 · 工作流引擎层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `durable-agent-backbone` | 持久化 Agent 任务骨干 | Temporal | 长时运行、容错优先的 Agent 任务流首选 |
| `pythonic-ai-orchestrator` | Python 原生 AI 编排器 | Prefect | Python 生态的动态 DAG 编排，AI 流水线友好 |
| `legacy-data-orchestrator` | 遗留数据编排器 | Airflow | 成熟但 AI 场景适配有限，存量系统可继续使用 |

#### C2 · Agent 编排层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `stateful-agent-standard` | 有状态多 Agent 新兴标准 | LangGraph | 复杂 Agent 工作流的图状态管理首选 |
| `role-based-multi-agent-framework` | 角色驱动多 Agent 框架 | CrewAI | 低样板代码的角色协作 Agent 快速构建 |
| `low-code-agent-platform` | 低代码 Agent 构建平台 | Dify | 内置 RAG 与工具集成的可视化 Agent 平台 |
| `open-source-workflow-builder` | 开源可视化工作流构建器 | Flowise | 开源拖拽式 LangChain 工作流构建 |
| `self-hosted-zapier-alternative` | 自托管 Zapier 替代方案 | n8n | 数据主权优先的业务流程自动化 |
| `managed-no-code-automation` | 托管无代码自动化平台 | Zapier | 6000+ 应用集成，AI Action 层叠加 |

#### C3 · RPA 与计算机控制层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `open-browser-agent-framework` | 开源浏览器 Agent 框架 | Browser Use | LLM 驱动浏览器控制的开源基础框架 |
| `llm-enhanced-browser-sdk` | LLM 增强浏览器自动化 SDK | Stagehand | Playwright + LLM 元素定位的商业 SDK |
| `browser-automation-foundation` | 浏览器自动化基础设施 | Playwright | 跨浏览器自动化的底层基础，AI Agent 的执行基座 |

#### C4 · 可观测性层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `langchain-native-observability` | LangChain 生态原生可观测性 | LangSmith | LangChain 用户的首选追踪与评估平台 |
| `open-source-observability-stack` | 开源 LLM 可观测性技术栈 | Langfuse | 数据主权优先的开源追踪与评估方案 |

#### C5 · Agent 设计模式层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `autonomous-agent-core-pattern` | 自主 Agent 核心执行模式 | Agentic Loop | 所有自主 Agent 的基础执行范式 |
| `human-governed-agent-pattern` | 人类监督 Agent 安全模式 | Human-in-the-Loop | 高风险场景的 Agent 安全治理模式 |

---

### Category D · 应用（Application）

> 面向**产品决策者与开发者体验团队**，描述终端 AI 产品的战略定位与竞争格局。

#### D1 · 通用助手层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `consumer-ai-product-leader` | 消费级 AI 产品领导者 | ChatGPT | 用户规模最大，品牌认知最强，生态最广 |
| `reasoning-assistant-leader` | 推理能力最强消费级助手 | Claude | 长文档分析与深度推理场景的首选 |
| `multimodal-search-assistant` | 多模态搜索增强助手 | Gemini | Google Workspace 深度集成，实时搜索最强 |

#### D2 · 编码助手层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `agentic-ide-leader` | Agentic IDE 领域领导者 | Cursor | 增长最快的 AI 原生 IDE，开发者首选 |
| `multi-agent-ide` | 多 Agent 协作 IDE | Antigravity | Google 生态的多 Agent 编码平台 |
| `enterprise-coding-platform` | 企业级编码平台 | GitHub Copilot | 企业安全合规首选，GitHub 生态深度集成 |

#### D3 · 创意媒体层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `ai-image-generation-leader` | AI 图像生成领域领导者 | Midjourney | 审美质量最高，创意专业人士首选 |
| `open-weight-image-model` | 开源权重图像生成模型 | Stable Diffusion | 自托管与定制化图像生成的基础模型 |
| `voice-synthesis-leader` | AI 语音合成领域领导者 | ElevenLabs | 超真实语音克隆与合成的行业标准 |

#### D4 · AI 搜索层

| `positioning` 值 | 中文定位 | 代表条目 | 战略含义 |
|-----------------|---------|---------|---------|
| `ai-native-search` | AI 原生搜索引擎 | Perplexity | 带引用的实时 AI 搜索，研究场景首选 |

---

## 战略决策矩阵

> 结合 `radar.maturity` 与 `decision.positioning` 进行技术选型决策：

```
                    maturity
                adopt    trial    assess    hold
               ┌────────┬────────┬─────────┬──────┐
  positioning  │ 立即    │ 试点   │ 持续    │ 计划  │
  = leader /   │ 采用    │ 验证   │ 观察    │ 迁移  │
  standard     │        │        │         │      │
               ├────────┼────────┼─────────┼──────┤
  positioning  │ 场景    │ 谨慎   │ 等待    │ 不   │
  = alternative│ 评估    │ 试点   │ 成熟    │ 推荐  │
  / legacy     │        │        │         │      │
               └────────┴────────┴─────────┴──────┘
```

### 选型优先级规则

1. **`adopt` + `*-standard` / `*-leader`** → 直接采用，无需评估替代品
2. **`adopt` + `legacy-*`** → 存量维护可用，新项目应规划迁移
3. **`trial` + `*-alternative`** → 在特定约束条件下（成本、数据主权）优先评估
4. **`assess` + `*-protocol`** → 关注标准化进展，暂不生产化

---

## 完整战略定位图

```
┌─────────────────────────────────────────────────────────────────┐
│  Category D · 应用产品层                                          │
│  consumer-ai-product-leader │ reasoning-assistant-leader         │
│  agentic-ide-leader │ enterprise-coding-platform                 │
│  ai-image-generation-leader │ voice-synthesis-leader             │
│  ai-native-search                                                │
├─────────────────────────────────────────────────────────────────┤
│  Category C · 编排自动化层                                        │
│  durable-agent-backbone │ stateful-agent-standard                │
│  low-code-agent-platform │ self-hosted-zapier-alternative        │
│  open-browser-agent-framework │ browser-automation-foundation    │
│  langchain-native-observability │ open-source-observability-stack│
│  autonomous-agent-core-pattern │ human-governed-agent-pattern    │
├─────────────────────────────────────────────────────────────────┤
│  Category B · 运行时层                                            │
│  general-purpose-api-standard │ high-reasoning-model             │
│  agentic-coding-leader │ long-context-leader                     │
│  open-weight-standard │ open-reasoning-model                     │
│  tool-use-standard │ hallucination-reduction-pattern             │
│  domain-customization │ human-ai-control-layer                   │
├─────────────────────────────────────────────────────────────────┤
│  Category A · 基础设施层                                          │
│  gpu-compute-standard │ open-gpu-alternative                     │
│  high-throughput-serving │ local-dev-standard                    │
│  training-framework-standard │ legacy-training-framework         │
│  efficient-finetuning │ unified-llm-gateway                      │
│  billion-scale-vector-store │ low-latency-vector-store           │
│  managed-cloud-ai-platform                                       │
└─────────────────────────────────────────────────────────────────┘
```
