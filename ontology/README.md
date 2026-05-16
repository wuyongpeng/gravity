# AI Technology Ontology

> 一个结构化的 AI 技术知识库，将 AI 技术栈从物理硬件到终端应用系统性地组织为 **6 层架构 × 9 个视角**，为技术选型、架构决策与团队对齐提供统一的认知框架。

---

## 项目概述

本项目通过 JSON 数据文件定义 AI 技术生态中的核心工具、模型、框架与概念，并为每个条目附加多维度的结构化视角描述。目标是让技术决策者能够：

- **快速定位**：在 50+ 个 AI 工具中找到适合特定场景的选项
- **多维评估**：从成本、安全、开放性、性能等 9 个维度对比技术选项
- **统一语言**：为跨团队技术讨论提供标准化的术语与分类体系
- **规避风险**：识别供应商锁定、数据主权与合规风险

---

## 架构层次

知识库按 AI 技术栈的依赖关系组织为 6 层，体现了从物理算力到认知逻辑再到应用产品的完整链路：

### 能力提供者 (Capability Providers)

**Layer 1 · Hardware** — 物理加速器  
提供原始算力：GPU、TPU、移动/边缘AI芯片、GPU互联技术

**Layer 2 · Infra** — 基础设施与服务  
提供计算与存储能力：推理服务、训练框架、向量数据库、状态记忆、分布式计算

**Layer 3 · Runtime** — 模型与协议  
提供基础智力：前沿模型（GPT-4o、Llama 3）、多模态与具身模型（RT-2）、通信协议（MCP）

### 认知逻辑 (Cognitive Logic)

**Layer 4 · Reasoning** — 推理范式  
定义思维方式：如何将 L3 的原始智力转化为解决具体问题的逻辑（RAG、CoT、Function Calling、Context Window）

### 能力消费者 (Capability Consumers)

**Layer 5 · Orchestration** — 工作流与自动化编排  
封装执行流程：工作流引擎、Agent 框架、RPA、可观测性

**Layer 6 · Application** — 终端产品与平台  
交付用户价值：通用助手、编码工具、创意媒体、AI 搜索、边缘AI设备

```
┌─────────────────────────────────────────────────────┐
│  Layer 6 · Application    终端产品与平台              │
│  ChatGPT · Claude · Cursor · Midjourney · Rabbit R1 │
├─────────────────────────────────────────────────────┤
│  Layer 5 · Orchestration  工作流与自动化编排          │
│  LangGraph · n8n · Temporal · LangSmith · Playwright │
├─────────────────────────────────────────────────────┤
│  Layer 4 · Reasoning      推理范式                    │
│  RAG · Chain-of-Thought · Function Calling · Context Window │
├─────────────────────────────────────────────────────┤
│  Layer 3 · Runtime        模型与协议                  │
│  GPT-4o · Llama 3 · RT-2 · MCP · Gemini 2.5 Pro     │
├─────────────────────────────────────────────────────┤
│  Layer 2 · Infra          基础设施与服务              │
│  vLLM · Milvus · PyTorch · Mem0 · Zep · Ray         │
├─────────────────────────────────────────────────────┤
│  Layer 1 · Hardware       物理加速器                  │
│  H100 · Apple Silicon · Snapdragon · Jetson · NVLink │
└─────────────────────────────────────────────────────┘
```

---

## 文件结构

### 数据文件(JSON)

| 文件 | 层级 | 条目数 | 内容 |
|------|------|--------|------|
| [`layers/L1-hardware.json`](layers/L1-hardware.json) | Layer 1 | 14 | GPU/TPU/LPU 物理加速器、移动AI芯片、边缘AI芯片、GPU互联 |
| [`layers/L2-infra.json`](layers/L2-infra.json) | Layer 2 | 17 | 推理服务、向量数据库、训练框架、状态与记忆、分布式计算 |
| [`layers/L3-runtime.json`](layers/L3-runtime.json) | Layer 3 | 12 | 前沿模型、多模态与具身模型、协议 |
| [`layers/L4-reasoning.json`](layers/L4-reasoning.json) | Layer 4 | 6 | RAG、CoT、Prompt Engineering、Function Calling、Fine-tuning、Context Window |
| [`layers/L5-orchestration.json`](layers/L5-orchestration.json) | Layer 5 | 17 | 工作流引擎、Agent 框架、RPA、可观测性、设计模式 |
| [`layers/L6-application.json`](layers/L6-application.json) | Layer 6 | 13 | 通用助手、编码工具、创意媒体、AI 搜索、边缘AI设备 |

**合计：79 个条目**

### 视角文档（Markdown）

| 文件 | 视角 | 面向角色 |
|------|------|---------|
| [`perspectives/radar.md`](perspectives/radar.md) | Radar · 技术雷达 | 技术委员会、架构师 |
| [`perspectives/deployment.md`](perspectives/deployment.md) | Deployment · 部署模式 | 平台工程师、DevOps |
| [`perspectives/lifecycle.md`](perspectives/lifecycle.md) | Lifecycle · 生命周期 | AI 工程师、产品经理 |
| [`perspectives/performance.md`](perspectives/performance.md) | Performance · 性能效率 | 系统优化师、后端工程师 |
| [`perspectives/stack.md`](perspectives/stack.md) | Stack · 技术栈定位 | 架构师、技术负责人 |
| [`perspectives/strategy.md`](perspectives/strategy.md) | Strategy · 战略定位 | 技术决策者、CTO |
| [`perspectives/cost.md`](perspectives/cost.md) | Cost · 成本模型 | 工程负责人、财务决策者 |
| [`perspectives/security.md`](perspectives/security.md) | Security · 安全合规 | 安全工程师、合规负责人 |
| [`perspectives/openness.md`](perspectives/openness.md) | Openness · 开放性 | 架构师、开源策略负责人 |

---

## 数据结构

每个条目遵循统一的 JSON Schema：

```json
{
  "uuid": "e5",
  "name": "LangGraph",
  "type": "framework",
  "summary": "Stateful graph-based orchestration for multi-agent systems.",
  "org": "LangChain",
  "url": "https://langchain.com/langgraph",
  "tags": ["agent", "multi-agent", "stateful", "graph"],
  "perspectives": {
    "radar":      { "group": "Agent Orchestration", "maturity": "trial", "importance": 91 },
    "lifecycle":  { "stage": "agent-coordination", "focus": ["stateful-graph"] },
    "deployment": { "type": "self-hosted", "hosting": "self-managed", "control_level": "high" },
    "performance":{ "focus": ["stateful-execution", "multi-agent-coordination"] },
    "stack":      { "layer": "agent-runtime" },
    "cost":       { "model": "free", "tier": "free", "relative": "low", "note": "..." },
    "security":   { "data_residency": "self-controlled", "compliance": [], "risk_level": "low" },
    "openness":   { "license": "mit", "weights": "n/a", "source": "open" },
    "decision":   { "positioning": "stateful-agent-standard" }
  },
  "relations": [
    { "target": "CrewAI", "type": "alternative" },
    { "target": "Agentic Loop", "type": "implements" }
  ]
}
```

### 视角字段说明

| 视角 | 核心字段 | 用途 |
|------|---------|------|
| `radar` | `maturity`（adopt/trial/assess/hold）、`importance`（0-100）| 技术采用优先级 |
| `lifecycle` | `stage`、`focus` | 在 AI 任务流中的阶段定位 |
| `deployment` | `type`、`hosting`、`control_level` | 部署方式与控制程度 |
| `performance` | `focus`、`techniques` | 性能优化目标与手段 |
| `stack` | `layer` | 在技术栈中的层级位置 |
| `cost` | `model`、`tier`、`relative`、`note` | 定价模型与成本水平 |
| `security` | `data_residency`、`compliance`、`risk_level` | 数据主权与合规风险 |
| `openness` | `license`、`weights`、`source` | 许可证与开放程度 |
| `decision` | `positioning` | 战略定位标识 |

---

## 快速选型指南

### 按场景选型

| 场景 | 推荐条目 | 关键视角 |
|------|---------|---------|
| **生产级推理服务** | vLLM + H100 | `performance.focus: throughput` |
| **本地开发原型** | Ollama + Apple Silicon | `deployment.type: local` |
| **企业 RAG 系统** | Milvus + LangGraph + GPT-4o | `radar.maturity: adopt` |
| **自主 Agent 构建** | LangGraph + Agentic Loop | `decision.positioning: stateful-agent-standard` |
| **数据主权优先** | Llama 3 + vLLM + Langfuse | `security.data_residency: self-controlled` |
| **低成本高性能** | DeepSeek R1 + vLLM | `cost.relative: low` + `performance.focus: reasoning` |
| **无代码自动化** | n8n / Dify | `stack.layer: business-automation` |
| **企业合规编码** | GitHub Copilot Enterprise | `security.compliance: [FedRAMP, SOC2]` |

### 按技术雷达选型

| `maturity` | 含义 | 行动建议 |
|-----------|------|---------|
| `adopt` | 成熟可用 | 直接采用，无需过多评估 |
| `trial` | 值得试点 | 在具体项目中验证可行性 |
| `assess` | 持续观察 | 关注发展，暂不生产化 |

---

## 关系类型

条目间的 `relations` 使用以下标准类型：

| `type` 值 | 含义 |
|----------|------|
| `alternative` | 可替代关系，功能相似可互换 |
| `depends` | 依赖关系，需要目标条目才能运行 |
| `ecosystem` | 生态关系，深度集成但非强依赖 |
| `implements` | 实现关系，该条目实现了目标概念 |
| `implemented_by` | 被实现关系，目标条目实现了该概念 |
| `constrains` | 约束关系，目标条目对该条目施加限制 |

---

## 覆盖范围

```
Hardware      ████████████████████  14 条目  GPU/TPU/LPU 加速器、移动/边缘AI芯片、GPU互联
Infra         ████████████████████  17 条目  推理/训练/向量DB/状态记忆/网关/分布式计算
Runtime       ████████████████████  12 条目  模型/协议/具身AI
Reasoning     ████████████████████  6 条目   推理范式与约束
Orchestration ████████████████████  17 条目  工作流/Agent编排/RPA/可观测性
Application   ████████████████████  13 条目  终端产品

总计：79 个条目 × 9 个视角
```

---

## 为什么 L4 Reasoning 是架构的灵魂？

L4 Reasoning（推理范式）是本架构最核心、最独特的设计。它与传统技术栈的本质区别在于：

### 传统 Web Stack vs AI Stack

**传统 Stack（如 LAMP）**：纯粹的技术组件堆叠
- 每一层都是具体的软件（数据库 + 中间件 + 前端）
- 层与层之间是"调用关系"

**AI Stack**：包含认知能力的堆叠
- L1-L3 提供"能力"（算力、存储、智力）
- **L4 提供"思维方式"**（如何思考和解题）
- L5-L6 消费能力并交付价值

### L4 的不可或缺性

如果删掉 L4，就像在教人做菜时：
- ✅ 列出了"锅、铲子、炉子"（L1-L3 硬件/基础设施）
- ✅ 列出了"菜单"（L6 应用）
- ❌ 但删掉了"炒菜技巧"（L4 推理范式）

**没有 RAG 和 CoT，底层的 LLM 只是一个会接龙聊天的大语言模型，无法成为真正的智能体。**

### L4 的定位

- **不是具体软件**：RAG、CoT、Function Calling 不是可以 `npm install` 的包
- **是认知模式**：它们是"解题套路"和"思维框架"
- **是架构约束**：Context Window 定义了所有推理范式必须遵守的边界

### 层级角色

| 层级 | 角色 | 提供内容 |
|------|------|---------|
| L1-L3 | Capability Providers | 算力、存储、基础智力 |
| **L4** | **Cognitive Logic** | **如何思考、如何解题** |
| L5-L6 | Capability Consumers | 工作流、应用产品 |

---

## 不包含的技术

本ontology聚焦于**AI技术栈的核心组件**，以下通用基础设施不在收录范围：

### 通用网络设备
- **高速网络**：InfiniBand交换机、以太网交换机、光模块（400G/800G）
- **网络协议**：RoCE、TCP/IP、RDMA
- **说明**：虽然InfiniBand等技术在大规模AI训练集群中广泛使用，但它们是HPC通用技术，不是AI专用。GPU间互联（NVLink/NVSwitch）已收录，因为它们是AI芯片的专用互联技术。

### 通用存储设备
- **分布式存储**：Ceph、MinIO、GlusterFS
- **网络存储**：NAS、SAN、NVMe-oF
- **对象存储**：S3、Azure Blob、Google Cloud Storage
- **说明**：向量数据库（Milvus、Qdrant）已收录，因为它们是AI专用的embedding存储。

### 通用数据库
- **关系数据库**：PostgreSQL、MySQL、Oracle
- **NoSQL数据库**：MongoDB、Redis、Cassandra
- **时序数据库**：InfluxDB、TimescaleDB
- **说明**：这些是通用数据管理技术，不是AI专用。

### 通用容器与编排
- **容器运行时**：Docker、containerd、Podman
- **容器编排**：Kubernetes、Docker Swarm
- **说明**：AI专用的编排平台（Kubeflow、Ray）已收录。

### 物理基础设施
- **服务器硬件**：Dell、HPE、Supermicro服务器
- **机柜与布线**：42U机柜、PDU、KVM
- **电源与制冷**：UPS、液冷系统、精密空调
- **说明**：这些属于数据中心物理层，不属于技术栈范畴。

### 垂直领域完整方案
- **自动驾驶系统**：Tesla FSD、Waymo Driver、Apollo
- **人形机器人**：Tesla Optimus、Figure 01、Boston Dynamics Atlas
- **智能家居生态**：Apple HomeKit、Google Home、Amazon Alexa
- **说明**：这些是垂直领域的完整解决方案。本ontology收录的是通用AI技术组件（如边缘AI芯片Jetson Orin、具身AI模型RT-2），而不是特定行业的产品。

---

## 设计原则

1. **结构优于叙述**：所有描述均为可枚举的结构化字段，便于程序化处理
2. **多视角正交**：每个视角独立描述一个维度，视角间无冗余
3. **层次清晰**：6 层架构反映真实的技术依赖关系
   - **L1-L3 (能力提供者)**：Hardware → Infra → Runtime 提供算力、存储和基础智力
   - **L4 (认知逻辑)**：Reasoning 定义如何将原始智力转化为解决问题的逻辑
   - **L5-L6 (能力消费者)**：Orchestration → Application 将智力封装成工作流和应用
4. **决策导向**：每个条目的 `decision.positioning` 直接回答"为什么选它"
5. **持续演进**：随 AI 技术发展，条目的 `radar.maturity` 会动态调整
