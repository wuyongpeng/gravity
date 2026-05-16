# Performance 视角枚举定义

> **视角定位**：性能效率（Performance）视角面向**AI 工程师与系统优化师**，描述每项技术的核心性能特征、优化目标与实现技术手段，帮助团队在吞吐量、延迟、成本、内存等多个维度做出合理的性能权衡决策。

---

## 字段结构

```json
"performance": {
  "focus": ["<性能关注点1>", "<性能关注点2>"],
  "techniques": ["<优化技术1>", "<优化技术2>"]  // 可选
}
```

> **说明**：`focus` 描述该技术的核心性能目标；`techniques` 是实现这些目标所采用的具体技术手段，为可选字段。

---

## `focus` — 性能关注点枚举

按性能维度分为 **7 大类**，共 **30 个枚举值**：

---

### 维度 1 · 吞吐量 `throughput`

> 单位时间内处理请求或数据的能力，是推理服务与训练框架的核心指标。

| `focus` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `throughput` | 吞吐量 | CUDA、ROCm、vLLM、Milvus | infra |
| `batch-processing` | 批量处理 | Airflow | orchestration |
| `stateful-execution` | 有状态执行吞吐 | LangGraph | orchestration |
| `multi-agent-coordination` | 多 Agent 协调吞吐 | LangGraph | orchestration |

---

### 维度 2 · 延迟 `latency`

> 单次请求从发出到收到响应的时间，是用户体验的核心指标。

| `focus` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `latency` | 响应延迟 | TGI、ChatGPT | infra / application |
| `real-time` | 实时响应 | GPT-4o、Gemini (app) | runtime / application |
| `context-speed` | 上下文处理速度 | Cursor | application |

---

### 维度 3 · 内存效率 `memory`

> GPU/CPU 内存的使用效率，直接决定可运行的模型规模与并发能力。

| `focus` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `memory-efficiency` | 内存效率 | vLLM、Unsloth | infra |
| `training-speed` | 训练速度 | Unsloth | infra |
| `token-limit` | Token 预算管理 | Context Window | runtime |
| `attention-scaling` | 注意力机制扩展 | Context Window | runtime |
| `temporal-reasoning` | 时序推理效率 | Zep | runtime |

---

### 维度 4 · 推理质量 `reasoning`

> 模型在复杂任务上的推理深度与准确性，是智能能力的核心体现。

| `focus` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `reasoning-depth` | 推理深度 | o3、Claude (app) | runtime / application |
| `reasoning` | 推理能力 | DeepSeek R1 | runtime |
| `multimodal-inference` | 多模态推理 | GPT-4o | runtime |
| `multimodal` | 多模态理解 | Gemini 2.5 Pro | runtime |
| `long-context` | 长上下文处理 | Gemini 2.5 Pro、Claude 3.7 | runtime |
| `agentic-coding` | Agent 编码能力 | Claude 3.7 Sonnet | runtime |

---

### 维度 5 · 成本效率 `cost`

> 在保证质量的前提下降低计算成本，是生产环境的关键考量。

| `focus` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `cost-efficiency` | 成本效率 | ChatGPT、DeepSeek R1 | application / runtime |
| `efficient-inference` | 高效推理 | Mistral Large | runtime |
| `ease-of-use` | 易用性（降低使用成本） | Ollama | infra |

---

### 维度 6 · 可靠性 `reliability`

> 系统在长时间运行、高负载或故障场景下的稳定性与容错能力。

| `focus` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `fault-tolerance` | 容错能力 | Temporal | orchestration |
| `long-running-execution` | 长时任务执行 | Temporal | orchestration |
| `browser-control` | 浏览器控制稳定性 | Playwright | orchestration |

---

### 维度 7 · 生态灵活性 `flexibility`

> 框架对不同硬件、模型和使用场景的适配能力。

| `focus` 值 | 中文 | 代表条目 | 文件 |
|-----------|------|---------|------|
| `flexibility` | 框架灵活性 | PyTorch | infra |
| `ecosystem` | 生态系统完整性 | PyTorch | infra |
| `scale` | 大规模扩展能力 | Milvus | infra |
| `filtering` | 过滤查询性能 | Qdrant | infra |
| `kernel-optimization` | 内核级优化 | CUDA | infra |

---

## `techniques` — 优化技术枚举

描述实现性能目标所采用的具体技术手段。

| `techniques` 值 | 中文 | 含义 | 代表条目 |
|----------------|------|------|---------|
| `tensor-core` | 张量核心 | 利用 NVIDIA Tensor Core 加速矩阵运算 | CUDA |
| `cuda-kernel` | CUDA 内核 | 自定义 CUDA 内核优化计算图 | CUDA |
| `hip-kernel` | HIP 内核 | AMD GPU 的 HIP 内核优化 | ROCm |
| `paged-attention` | 分页注意力 | 动态管理 KV Cache 内存，提升并发 | vLLM |
| `continuous-batching` | 连续批处理 | 动态合并请求批次，提升 GPU 利用率 | vLLM、TGI |
| `torch.compile` | Torch 编译优化 | 将 PyTorch 模型编译为优化计算图 | PyTorch |
| `distributed-training` | 分布式训练 | 多 GPU/多节点并行训练 | PyTorch |
| `lora-optimization` | LoRA 优化 | 低秩适配微调，大幅降低 VRAM 需求 | Unsloth |
| `model-routing` | 模型路由 | 根据请求特征动态选择最优模型 | ChatGPT |
| `caching` | 缓存 | 缓存常见请求结果，降低重复计算 | ChatGPT |

---

## 性能维度权衡矩阵

不同角色关注的性能维度各有侧重：

| 角色 | 首要关注维度 | 代表指标 |
|------|------------|---------|
| **基础设施工程师** | 吞吐量 + 内存效率 | tokens/s、GPU 利用率 |
| **后端工程师** | 延迟 + 成本效率 | P99 延迟、$/1M tokens |
| **AI 工程师** | 推理质量 + 长上下文 | 准确率、上下文长度 |
| **运维工程师** | 可靠性 + 容错 | 可用性、MTTR |
| **产品经理** | 易用性 + 实时性 | 首字节时间、用户体验 |

---

## 各条目 performance 覆盖情况

### 缺少 performance 字段的条目（需补充）

| 条目 | 文件 | 建议补充的 `focus` |
|------|------|-----------------|
| GitHub Copilot | application | `latency`, `code-completion-speed` |
| Midjourney | application | `image-quality`, `generation-speed` |
| Stable Diffusion | application | `image-quality`, `memory-efficiency` |
| ElevenLabs | application | `audio-quality`, `real-time` |
| MCP | runtime | `tool-invocation-latency` |
| A2A | runtime | `agent-communication-latency` |
| RAG | runtime | `retrieval-accuracy`, `latency` |
| Chain-of-Thought | runtime | `reasoning-depth` |
| Function Calling | runtime | `tool-invocation-latency` |
| Prompt Engineering | runtime | `output-quality` |
| Fine-tuning | runtime | `training-speed`, `domain-accuracy` |
| Dify | orchestration | `workflow-throughput` |
| Flowise | orchestration | `workflow-throughput` |
| n8n | orchestration | `automation-throughput` |
| Zapier | orchestration | `integration-latency` |
| Agentic Loop | orchestration | `iteration-speed` |
| Human-in-the-Loop | orchestration | `approval-latency` |
| LangSmith | orchestration | `trace-ingestion-throughput` |
| Langfuse | orchestration | `trace-ingestion-throughput` |
