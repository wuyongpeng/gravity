# Openness 视角枚举定义

> **视角定位**：开放性（Openness）视角面向**技术架构师与开源策略负责人**，描述每项技术的许可证类型、模型权重开放程度与源代码开放程度，帮助团队评估技术的可定制性、供应商锁定风险与商业使用合规性，尤其适用于需要自主可控或二次开发的场景。

---

## 字段结构

```json
"openness": {
  "license": "<许可证>",
  "weights": "<权重开放性>",
  "source": "<源码开放性>"
}
```

> **说明**：`license` 描述软件或模型的授权协议；`weights` 仅适用于 AI 模型，描述模型参数的开放程度；`source` 描述源代码的可获取程度。

---

## `license` — 许可证枚举

### 开源许可证

| `license` 值 | 全称 | 商业使用 | 修改分发 | 代表条目 |
|-------------|------|---------|---------|---------|
| `mit` | MIT License | ✅ 允许 | ✅ 允许 | LangGraph、CrewAI、Temporal、Langfuse、Browser Use |
| `apache-2.0` | Apache License 2.0 | ✅ 允许 | ✅ 允许（需保留声明）| Airflow、Prefect、Dify、Flowise、Playwright、ROCm |
| `gpl-3.0` | GNU General Public License v3 | ⚠️ 衍生品须开源 | ✅ 允许（须开源）| 部分 GNU 工具 |
| `lgpl-3.0` | GNU Lesser GPL v3 | ✅ 允许（动态链接）| ✅ 允许 | 部分库 |
| `bsd-3-clause` | BSD 3-Clause License | ✅ 允许 | ✅ 允许 | 部分学术工具 |

### 模型专用许可证

| `license` 值 | 全称 | 商业使用 | 修改分发 | 代表条目 |
|-------------|------|---------|---------|---------|
| `llama-community` | Meta Llama Community License | ⚠️ MAU>700M 需授权 | ✅ 允许 | Llama 3 |
| `mistral-research` | Mistral Research License | ⚠️ 研究用途免费 | ✅ 允许 | Mistral 系列 |
| `deepseek-license` | DeepSeek Model License | ✅ 允许（有限制）| ✅ 允许 | DeepSeek R1 |
| `creativeml-openrail-m` | CreativeML Open RAIL-M | ✅ 允许（禁止滥用）| ✅ 允许 | Stable Diffusion |
| `open-concept` | 开放概念（无许可证约束）| ✅ 允许 | ✅ 允许 | Agentic Loop、Human-in-the-Loop |

### 特殊许可证

| `license` 值 | 全称 | 商业使用 | 修改分发 | 代表条目 |
|-------------|------|---------|---------|---------|
| `fair-code` | Fair-code License | ⚠️ 自托管免费，SaaS 需授权 | ✅ 允许 | n8n |
| `sspl` | Server Side Public License | ⚠️ 提供服务须开源 | ✅ 允许 | MongoDB（参考）|

### 专有许可证

| `license` 值 | 全称 | 商业使用 | 修改分发 | 代表条目 |
|-------------|------|---------|---------|---------|
| `proprietary` | 专有许可证 | ⚠️ 按协议授权 | ❌ 不允许 | ChatGPT、Claude、Cursor、LangSmith、Zapier |
| `nvidia-eula` | NVIDIA End User License Agreement | ⚠️ 按协议授权 | ❌ 不允许 | CUDA |

---

## `weights` — 模型权重开放性枚举

仅适用于 AI 模型类条目：

| `weights` 值 | 中文 | 含义 | 代表条目 |
|-------------|------|------|---------|
| `open` | 开放权重 | 模型参数公开可下载，可本地部署与微调 | Llama 3、Mistral Large、DeepSeek R1、Stable Diffusion |
| `closed` | 闭源权重 | 模型参数不公开，只能通过 API 访问 | GPT-4o、o3、Claude 3.7、Gemini 2.5 Pro |
| `n/a` | 不适用 | 非模型类工具，无权重概念 | Airflow、LangGraph、Cursor、Playwright |

---

## `source` — 源码开放性枚举

| `source` 值 | 中文 | 含义 | 代表条目 |
|------------|------|------|---------|
| `open` | 开源 | 源代码完全公开，可自由查看、修改、贡献 | vLLM、Airflow、LangGraph、Langfuse、Playwright |
| `closed` | 闭源 | 源代码不公开，黑盒使用 | ChatGPT、Claude、Cursor、LangSmith、Zapier |
| `partial` | 部分开源 | 核心代码开源，部分组件或训练代码闭源 | Stable Diffusion（推理开源，训练数据闭源）|

---

## 各层开放性分布

### Hardware 层（物理加速器）

| 条目 | license | weights | source | 说明 |
|------|---------|---------|--------|------|
| H100 | `nvidia-eula` | `n/a` | `closed` | NVIDIA 专有硬件；驱动闭源 |
| H200 | `nvidia-eula` | `n/a` | `closed` | NVIDIA 专有硬件；驱动闭源 |
| A100 | `nvidia-eula` | `n/a` | `closed` | NVIDIA 专有硬件；驱动闭源 |
| Apple Silicon | `proprietary` | `n/a` | `closed` | Apple 专有芯片；Metal 框架部分开源 |
| Google TPU v5 | `proprietary` | `n/a` | `closed` | Google 专有硬件；仅通过 GCP 访问 |
| Groq LPU | `proprietary` | `n/a` | `closed` | Groq 专有芯片架构；API 访问 |

### Infra 层（基础设施）

| 条目 | license | weights | source | 说明 |
|------|---------|---------|--------|------|
| vLLM | `apache-2.0` | `n/a` | `open` | 完全开源；社区活跃 |
| TGI | `apache-2.0` | `n/a` | `open` | HuggingFace 开源项目 |
| Ollama | `mit` | `n/a` | `open` | 完全开源 |
| PyTorch | `bsd-3-clause` | `n/a` | `open` | Meta 开源；社区最活跃的训练框架 |
| Unsloth | `apache-2.0` | `n/a` | `open` | 开源微调工具；Pro 版闭源 |
| Milvus | `apache-2.0` | `n/a` | `open` | Linux Foundation 开源项目 |
| Qdrant | `apache-2.0` | `n/a` | `open` | 完全开源 |
| LiteLLM | `mit` | `n/a` | `open` | 完全开源；Enterprise 版闭源扩展 |
| AWS Bedrock | `proprietary` | `n/a` | `closed` | AWS 托管服务；底层模型各有许可证 |
| CUDA | `nvidia-eula` | `n/a` | `closed` | NVIDIA 专有工具包；部分库开源 |
| ROCm | `apache-2.0` | `n/a` | `open` | AMD 完全开源 GPU 软件栈 |
| TensorFlow | `apache-2.0` | `n/a` | `open` | Google 开源；社区活跃度下降 |

### Runtime 层（模型运行时）

| 条目 | license | weights | source | 说明 |
|------|---------|---------|--------|------|
| GPT-4o | `proprietary` | `closed` | `closed` | OpenAI 完全闭源 |
| o3 | `proprietary` | `closed` | `closed` | OpenAI 完全闭源 |
| Claude 3.7 Sonnet | `proprietary` | `closed` | `closed` | Anthropic 完全闭源 |
| Gemini 2.5 Pro | `proprietary` | `closed` | `closed` | Google 完全闭源 |
| Llama 3 | `llama-community` | `open` | `partial` | Meta 开放权重；训练代码部分开源 |
| Mistral Large | `proprietary` | `closed` | `closed` | Mistral AI 闭源旗舰模型 |
| DeepSeek R1 | `deepseek-license` | `open` | `partial` | 权重开放；训练代码部分开源 |
| MCP | `mit` | `n/a` | `open` | Anthropic 开放协议规范 |
| A2A | `apache-2.0` | `n/a` | `open` | Google 开放协议规范 |
| Mem0 | `apache-2.0` | `n/a` | `open` | 完全开源 |
| Zep | `apache-2.0` | `n/a` | `open` | 完全开源 |
| Context Window | `open-concept` | `n/a` | `open` | 架构概念，无许可证约束 |

### Patterns 层（推理范式）

| 条目 | license | weights | source | 说明 |
|------|---------|---------|--------|------|
| RAG | `open-concept` | `n/a` | `open` | 开放架构模式；多种开源实现 |
| Chain-of-Thought | `open-concept` | `n/a` | `open` | 学术提示技术；无许可证约束 |
| Prompt Engineering | `open-concept` | `n/a` | `open` | 工程实践；无许可证约束 |
| Function Calling | `open-concept` | `n/a` | `open` | 开放技术模式；各平台实现各异 |
| Fine-tuning | `open-concept` | `depends-on-base-model` | `open` | 技术方法开放；权重取决于基础模型 |

### Orchestration 层（编排）

| 条目 | license | weights | source | 说明 |
|------|---------|---------|--------|------|
| Temporal | `mit` | `n/a` | `open` | 完全开源；Cloud 版闭源 |
| Prefect | `apache-2.0` | `n/a` | `open` | 完全开源；Cloud 版闭源 |
| Airflow | `apache-2.0` | `n/a` | `open` | Apache 顶级项目；完全开源 |
| LangGraph | `mit` | `n/a` | `open` | 完全开源 |
| CrewAI | `mit` | `n/a` | `open` | 完全开源 |
| Dify | `apache-2.0` | `n/a` | `open` | 完全开源；Cloud 版闭源 |
| Flowise | `apache-2.0` | `n/a` | `open` | 完全开源 |
| n8n | `fair-code` | `n/a` | `open` | 源码公开；SaaS 商业使用需授权 |
| Zapier | `proprietary` | `n/a` | `closed` | 完全闭源 SaaS |
| Browser Use | `mit` | `n/a` | `open` | 完全开源 |
| Stagehand | `mit` | `n/a` | `open` | SDK 开源；Browserbase 平台闭源 |
| Playwright | `apache-2.0` | `n/a` | `open` | Microsoft 开源；完全开放 |
| LangSmith | `proprietary` | `n/a` | `closed` | LangChain 闭源 SaaS 产品 |
| Langfuse | `mit` | `n/a` | `open` | 完全开源；Cloud 版闭源扩展 |
| Agentic Loop | `open-concept` | `n/a` | `open` | 开放架构概念 |
| Human-in-the-Loop | `open-concept` | `n/a` | `open` | 开放设计模式 |

### Application 层（终端产品）

| 条目 | license | weights | source | 说明 |
|------|---------|---------|--------|------|
| ChatGPT | `proprietary` | `closed` | `closed` | OpenAI 完全闭源产品 |
| Claude | `proprietary` | `closed` | `closed` | Anthropic 完全闭源产品 |
| Gemini | `proprietary` | `closed` | `closed` | Google 完全闭源产品 |
| Cursor | `proprietary` | `n/a` | `closed` | Anysphere 闭源 IDE |
| Antigravity | `proprietary` | `n/a` | `closed` | Google 闭源 IDE |
| GitHub Copilot | `proprietary` | `n/a` | `closed` | Microsoft/GitHub 闭源产品 |
| Midjourney | `proprietary` | `closed` | `closed` | 完全闭源；生成内容版权复杂 |
| Stable Diffusion | `creativeml-openrail-m` | `open` | `partial` | 权重开放；禁止特定滥用场景 |
| ElevenLabs | `proprietary` | `closed` | `closed` | 完全闭源 SaaS |
| Perplexity | `proprietary` | `closed` | `closed` | 完全闭源 SaaS |

---

## 开放性决策框架

### 开放性 vs 能力权衡

| 场景需求 | 推荐开放性策略 | 代表选择 |
|---------|-------------|---------|
| **最高能力，不在意锁定** | `weights: closed` + `source: closed` | GPT-4o、Claude 3.7、Gemini 2.5 Pro |
| **能力与自主可控平衡** | `weights: open` + `source: partial` | Llama 3、DeepSeek R1 |
| **完全自主可控** | `weights: open` + `source: open` | Llama 3（自托管）+ vLLM |
| **工具链完全开源** | `license: apache-2.0/mit` + `source: open` | Airflow、LangGraph、Langfuse、Playwright |
| **避免 GPL 传染** | `license: mit/apache-2.0/bsd` | 大多数 AI 工具链 |

### 商业使用合规检查

| 使用场景 | 需要检查的许可证 | 风险点 |
|---------|---------------|-------|
| **SaaS 产品集成** | `fair-code`（n8n）| 提供 SaaS 服务需要商业授权 |
| **大规模用户部署** | `llama-community`（Llama 3）| MAU > 700M 需要 Meta 授权 |
| **图像生成商业化** | `creativeml-openrail-m`（SD）| 禁止特定滥用场景；需遵守使用条款 |
| **模型微调再分发** | `deepseek-license`（DeepSeek）| 需遵守 DeepSeek 使用限制 |
| **企业内部工具** | 大多数 `mit/apache-2.0` | 通常无限制，注意保留版权声明 |

### 供应商锁定风险评估

```
开放性高（低锁定风险）          开放性低（高锁定风险）
        ←─────────────────────────────────→
  Llama 3    DeepSeek R1    GPT-4o    ChatGPT
  vLLM       Mistral        Claude    Cursor
  Airflow    (API 访问)     Gemini    LangSmith
  LangGraph                           Zapier
  Playwright
```

---

## 开放性全景图

```
┌─────────────────────────────────────────────────────────────────┐
│  完全开源（source: open + weights: open/n/a）                     │
│  vLLM · TGI · Ollama · PyTorch · Milvus · Qdrant · LiteLLM     │
│  Airflow · LangGraph · CrewAI · Dify · Flowise · Playwright     │
│  Langfuse · Browser Use · Llama 3 · DeepSeek R1 · MCP · A2A    │
├─────────────────────────────────────────────────────────────────┤
│  部分开源（source: partial 或 fair-code）                         │
│  Stable Diffusion · Unsloth · n8n · Stagehand · Temporal        │
│  Prefect · Mem0 · Zep                                           │
├─────────────────────────────────────────────────────────────────┤
│  完全闭源（source: closed + weights: closed/n/a）                 │
│  GPT-4o · o3 · Claude 3.7 · Gemini 2.5 Pro · Mistral Large     │
│  ChatGPT · Claude(app) · Gemini(app) · Cursor · Antigravity     │
│  GitHub Copilot · Midjourney · ElevenLabs · Perplexity          │
│  LangSmith · Zapier · CUDA · AWS Bedrock · H100/H200/A100       │
└─────────────────────────────────────────────────────────────────┘
```
