# AI Technology Ontology 架构设计理念

## 核心设计哲学

本 ontology 采用 **6 层架构**，体现了 AI 技术栈从物理算力到认知逻辑再到应用产品的完整链路。

### 三层角色划分

```
┌─────────────────────────────────────────┐
│  L6 Application  │                      │
│  L5 Orchestration│  Capability Consumers│
├─────────────────────────────────────────┤
│  L4 Reasoning    │  Cognitive Logic     │  ← 架构灵魂
├─────────────────────────────────────────┤
│  L3 Runtime      │                      │
│  L2 Infra        │  Capability Providers│
│  L1 Hardware     │                      │
└─────────────────────────────────────────┘
```

---

## L4 Reasoning：架构的灵魂

### 为什么 L4 是最核心的设计？

**AI Stack 与传统 Web Stack 的本质区别：**

| 维度 | 传统 Stack (LAMP) | AI Stack |
|------|------------------|----------|
| 组成 | 纯技术组件堆叠 | 技术 + 认知能力堆叠 |
| 层级性质 | 每层都是具体软件 | L4 是"思维方式" |
| 层间关系 | 调用关系 | 能力提供 → 认知逻辑 → 能力消费 |

### L4 的不可或缺性

**类比：教人做菜**

- ✅ L1-L3：锅、铲子、炉子（硬件/基础设施）
- ✅ L6：菜单（应用产品）
- ❌ 如果删掉 L4：缺少"炒菜技巧"

**没有 RAG 和 CoT，底层的 LLM 只是一个会接龙聊天的大语言模型，无法成为真正的智能体。**

### L4 的独特性

1. **不是具体软件**
   - RAG、CoT、Function Calling 不是可以 `npm install` 的包
   - 它们是"解题套路"和"思维框架"

2. **是认知模式**
   - 定义了如何将 L3 的原始智力转化为解决具体问题的逻辑
   - 是 AI 工程师必须掌握的核心概念

3. **是架构约束**
   - Context Window 定义了所有推理范式必须遵守的边界
   - 影响 RAG、记忆架构、Prompt Engineering 的设计

---

## 层级详解

### L1 Hardware - 物理加速器
**角色**：Capability Provider  
**提供**：原始算力

- 数据中心 AI 芯片（H100、TPU、Groq LPU）
- 桌面 AI 芯片（Apple Silicon）
- 移动 AI 芯片（Snapdragon、Tensor）
- 边缘 AI 芯片（Jetson Orin、Hailo-8）
- GPU 互联（NVLink、NVSwitch）

### L2 Infra - 基础设施与服务
**角色**：Capability Provider  
**提供**：计算与存储能力

- GPU 平台（CUDA、ROCm）
- 模型服务（vLLM、TGI、Ollama）
- 训练与微调（PyTorch、Unsloth）
- 向量数据库（Milvus、Qdrant、Weaviate）
- **状态与记忆**（Mem0、Zep）← 新增组
- 网关与代理（LiteLLM）
- 分布式计算（Ray）

**设计决策**：
- Mem0/Zep 从 L3 移至 L2，因为它们本质是**持久化存储基础设施**
- 与向量数据库并列，强调外部化记忆的存储属性

### L3 Runtime - 模型与协议
**角色**：Capability Provider  
**提供**：基础智力

- 前沿模型（GPT-4o、Claude、Llama 3、DeepSeek R1）
- 多模态与具身模型（RT-2、OpenVLA、Octo）
- 协议（MCP、A2A）

**设计决策**：
- 移除 Mem0/Zep（移至 L2）
- 移除 Context Window（移至 L4）
- 更纯粹：只保留**模型本身**和**通信协议**
- 定位：连接底层 Infra 和上层 Logic 的**标准接口层**

### L4 Reasoning - 推理范式
**角色**：Cognitive Logic  
**提供**：思维方式与约束

- 知识与检索（RAG）
- 推理范式（Chain-of-Thought、Prompt Engineering）
- 工具使用（Function Calling）
- 模型适配（Fine-tuning）
- **上下文约束**（Context Window）← 新增组

**设计决策**：
- 从 "Techniques" 重命名为 "Reasoning Paradigms"
- 强调这是**认知逻辑层**，不是具体软件
- Context Window 作为约束概念，影响所有推理范式的设计

**为什么叫 "Paradigms"？**
- 在技术圈（尤其 AI）有强烈共识感
- 代表一种思考/解决问题的基础范式
- 位于 Runtime（模型本身）和 Orchestration（流程编排）之间

### L5 Orchestration - 工作流与自动化编排
**角色**：Capability Consumer  
**提供**：执行流程封装

- 工作流引擎（Temporal、Prefect、Airflow、Kubeflow）
- Agent 编排（LangGraph、CrewAI、Dify、n8n）
- RPA 与计算机使用（Browser Use、Playwright）
- 评估与可观测性（LangSmith、Langfuse）
- 编排概念（Agentic Loop、Human-in-the-Loop）

### L6 Application - 终端产品与平台
**角色**：Capability Consumer  
**提供**：用户价值交付

- 通用助手（ChatGPT、Claude、Gemini）
- 编码助手（Cursor、Antigravity、GitHub Copilot）
- 创意媒体（Midjourney、Stable Diffusion、ElevenLabs）
- AI 搜索与研究（Perplexity）
- 边缘 AI 设备（Rabbit R1、Meta Ray-Ban Smart Glasses）

---

## 架构演进历史

### v1.0 → v1.1 重大调整（2025-05-16）

#### 调整内容

1. **L2 Infra**
   - ✅ 新增 "State & Memory" 组
   - ✅ Mem0、Zep 从 L3 移入

2. **L3 Runtime**
   - ✅ 重新定义为 "Models & Protocols"
   - ✅ 移除 Mem0、Zep（→ L2）
   - ✅ 移除 Context Window（→ L4）
   - ✅ 移除 "Memory & Context" 组

3. **L4 重命名**
   - ✅ "Techniques" → "Reasoning Paradigms"
   - ✅ 新增 "Context Constraint" 组
   - ✅ Context Window 从 L3 移入

4. **文件重命名**
   - ✅ `L4_techniques.json` → `L4_reasoning.json`

#### 调整理由

| 调整 | 理由 |
|------|------|
| Mem0/Zep → L2 | 本质是持久化存储基础设施，与向量数据库同属存储层 |
| Context Window → L4 | 是推理范式的约束概念，影响 RAG、记忆、Prompt 设计 |
| L4 重命名 | "Reasoning Paradigms" 更准确表达认知逻辑层的定位 |

#### 统计变化

| 层级 | v1.0 | v1.1 | 变化 |
|------|------|------|------|
| L1 Hardware | 14 | 14 | - |
| L2 Infra | 16 | 18 | +2 (Mem0, Zep) |
| L3 Runtime | 15 | 13 | -2 (Mem0, Zep, Context Window) |
| L4 Reasoning | 5 | 6 | +1 (Context Window) |
| L5 Orchestration | 17 | 17 | - |
| L6 Application | 13 | 13 | - |
| **总计** | **80** | **81** | **+1** |

---

## 设计原则

1. **结构优于叙述**  
   所有描述均为可枚举的结构化字段，便于程序化处理

2. **多视角正交**  
   每个视角独立描述一个维度，视角间无冗余

3. **层次清晰**  
   6 层架构反映真实的技术依赖关系：
   - L1-L3：能力提供者
   - L4：认知逻辑
   - L5-L6：能力消费者

4. **决策导向**  
   每个条目的 `decision.positioning` 直接回答"为什么选它"

5. **持续演进**  
   随 AI 技术发展，条目的 `radar.maturity` 会动态调整

---

## 常见问题

### Q1: 为什么 L4 不是具体软件层？

**A**: AI Stack 与传统 Stack 的本质区别在于包含了"认知能力的堆叠"。

- 传统 Stack：每层都是具体软件（MySQL、Apache、PHP）
- AI Stack：L4 是"思维方式"（RAG、CoT、Function Calling）

如果删掉 L4，就失去了"如何让模型思考"的核心逻辑。

### Q2: 为什么 Mem0/Zep 在 L2 而不是 L3？

**A**: 它们的核心价值是**外部化记忆**：

- 让信息跨会话保存、检索、更新
- 独立于单次上下文窗口扩展
- 本质是持久化存储基础设施

与向量数据库（Milvus、Qdrant）同属存储层。

### Q3: 为什么 Context Window 在 L4 而不是 L3？

**A**: Context Window 是一个**约束概念**：

- 决定了 RAG 如何设计（检索多少文档）
- 决定了记忆架构如何设计（何时外部化）
- 决定了 Prompt Engineering 如何优化（如何压缩上下文）

它不是模型的"能力"，而是推理范式必须遵守的"边界"。

### Q4: L4 的架构不对称（其他层是组件，L4 是概念）是否合理？

**A**: 这正是 AI Stack 的独特之处：

- L1-L3、L5-L6：组件层（具体的工具/产品）
- L4：方法论层（抽象的思维方式）

虽然不对称，但语义清晰，且反映了 AI 技术栈的真实结构。

---

## 参考资料

- [AI Technology Ontology README](README.md)
- [Layer 4 Reasoning Paradigms](L4_reasoning.json)
- [Architecture Evolution Discussion](https://github.com/your-repo/discussions/1)

---

**最后更新**: 2025-05-16  
**版本**: v1.1  
**维护者**: AI Technology Ontology Team
