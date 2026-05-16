# Deployment 视角枚举定义

> **视角定位**：部署形态（Deployment）视角面向**运维工程师与平台架构师**，描述每项技术的运行位置、托管方式与控制权归属，帮助团队在自主可控与便捷托管之间做出合理的部署决策。

---

## 字段结构

```json
"deployment": {
  "type": "<部署类型>",
  "hosting": "<托管方式>",       // 可选
  "control_level": "<控制等级>"  // 可选
}
```

---

## `type` — 部署类型

描述技术运行在哪里、由谁管理基础设施。

| 枚举值 | 中文 | 含义 | 典型场景 |
|--------|------|------|---------|
| `cloud-api` | 云端 API | 通过 HTTP API 调用云端托管模型或服务，无需管理任何基础设施 | 调用 OpenAI / Anthropic / Google API |
| `cloud-saas` | 云端 SaaS | 完全托管的云端软件服务，用户只使用产品界面 | Zapier、ChatGPT 网页版 |
| `managed-cloud` | 托管云平台 | 云厂商提供的托管 AI 服务，统一封装多个模型 API | AWS Bedrock |
| `self-hosted` | 自托管 | 在自有服务器或私有云上部署，完全掌控数据与配置 | vLLM、PyTorch、Milvus |
| `local` | 本地运行 | 在开发者本机运行，无需网络，适合开发调试 | Ollama |
| `hybrid` | 混合部署 | 同时支持云端与自托管，可按需切换 | Prefect |
| `desktop-cloud` | 桌面 + 云端 | 客户端安装在本地，计算能力依赖云端 | Cursor、Antigravity |
| `cloud-ide` | 云端 + IDE 插件 | 以 IDE 插件形式集成，后端能力在云端 | GitHub Copilot |

---

## `hosting` — 托管方式

描述服务的具体托管形式，作为 `type` 的补充说明。

| 枚举值 | 中文 | 含义 |
|--------|------|------|
| `managed-api` | 托管 API | 服务商直接提供 API 端点，按调用计费 |
| `managed` | 完全托管 | 云厂商负责所有基础设施运维 |
| `self-managed` | 自行管理 | 用户自行负责部署、扩缩容与运维 |

---

## `control_level` — 控制等级

描述用户对底层基础设施、数据与配置的掌控程度。

| 枚举值 | 中文 | 含义 | 适用场景 |
|--------|------|------|---------|
| `high` | 高控制 | 完全掌控数据、模型权重、网络与配置 | 数据合规要求高、需要定制化的场景 |
| `medium` | 中等控制 | 可配置关键参数，但基础设施由服务商管理 | 混合部署、托管平台 |
| `low` | 低控制 | 黑盒服务，用户只能调用 API，无法干预底层 | 快速原型、非敏感数据场景 |

---

## 各条目部署形态一览

### Infra

| 条目 | `type` | `hosting` | `control_level` |
|------|--------|-----------|----------------|
| CUDA | `self-hosted` | `self-managed` | `high` |
| ROCm | `self-hosted` | `self-managed` | `high` |
| vLLM | `self-hosted` | `self-managed` | `high` |
| TGI | `self-hosted` | `self-managed` | `high` |
| Ollama | `local` | `self-managed` | `high` |
| PyTorch | `self-hosted` | `self-managed` | `high` |
| TensorFlow | `self-hosted` | `self-managed` | `high` |
| Unsloth | `self-hosted` | `self-managed` | `high` |
| Milvus | `self-hosted` | `self-managed` | `high` |
| Qdrant | `self-hosted` | `self-managed` | `high` |
| LiteLLM | `self-hosted` | `self-managed` | `high` |
| AWS Bedrock | `managed-cloud` | `managed` | `medium` |

### Runtime

| 条目 | `type` | `hosting` | `control_level` |
|------|--------|-----------|----------------|
| GPT-4o | `cloud-api` | `managed-api` | `low` |
| o3 | `cloud-api` | `managed-api` | `low` |
| Claude 3.7 Sonnet | `cloud-api` | `managed-api` | `low` |
| Gemini 2.5 Pro | `cloud-api` | `managed-api` | `low` |
| Llama 3 | `self-hosted` | `self-managed` | `high` |
| Mistral Large | `cloud-api` | `managed-api` | `low` |
| DeepSeek R1 | `self-hosted` | `self-managed` | `high` |
| MCP | `self-hosted` | `self-managed` | `high` |
| A2A | `self-hosted` | `self-managed` | `high` |
| Mem0 | `self-hosted` | `self-managed` | `high` |
| Zep | `self-hosted` | `self-managed` | `high` |

### Orchestration

| 条目 | `type` | `hosting` | `control_level` |
|------|--------|-----------|----------------|
| Temporal | `self-hosted` | `self-managed` | `high` |
| Prefect | `hybrid` | `self-managed` | `medium` |
| Airflow | `self-hosted` | `self-managed` | `high` |
| LangGraph | `self-hosted` | `self-managed` | `high` |
| Dify | `self-hosted` | `self-managed` | `high` |
| Flowise | `self-hosted` | `self-managed` | `high` |
| n8n | `self-hosted` | `self-managed` | `high` |
| Zapier | `cloud-saas` | `managed` | `low` |
| Browser Use | `self-hosted` | `self-managed` | `high` |
| Stagehand | `self-hosted` | `self-managed` | `high` |
| Playwright | `self-hosted` | `self-managed` | `high` |
| LangSmith | `cloud-saas` | `managed` | `low` |
| Langfuse | `self-hosted` | `self-managed` | `high` |

### Application

| 条目 | `type` | `hosting` | `control_level` |
|------|--------|-----------|----------------|
| ChatGPT | `cloud-saas` | `managed-api` | `low` |
| Claude (app) | `cloud-saas` | `managed-api` | `low` |
| Gemini (app) | `cloud-saas` | `managed-api` | `low` |
| Cursor | `desktop-cloud` | `managed-api` | `medium` |
| Antigravity | `desktop-cloud` | `managed-api` | `medium` |
| GitHub Copilot | `cloud-ide` | `managed-api` | `low` |
| Midjourney | `cloud-saas` | `managed` | `low` |
| Stable Diffusion | `self-hosted` | `self-managed` | `high` |
| ElevenLabs | `cloud-saas` | `managed-api` | `low` |
| Perplexity | `cloud-saas` | `managed` | `low` |

---

## 控制权 vs 便捷性 权衡矩阵

```
高控制 ▲
      │  self-hosted ●●●●●●●●●●●●
      │  (CUDA/vLLM/PyTorch/Llama3...)
      │
      │  hybrid ●
      │  (Prefect)
      │
      │  desktop-cloud ●●
      │  (Cursor/Antigravity)
      │
      │  managed-cloud ●
      │  (AWS Bedrock)
      │
      │  cloud-ide ●
      │  (GitHub Copilot)
      │
      │  cloud-api ●●●●●
      │  (GPT-4o/Claude/Gemini...)
      │
      │  cloud-saas ●●●●●●
      │  (ChatGPT/Zapier/Midjourney...)
低控制 └──────────────────────────────▶ 高便捷
```
