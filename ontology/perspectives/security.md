# Security 视角枚举定义

> **视角定位**：安全合规（Security）视角面向**安全工程师、合规负责人与企业架构师**，描述每项技术的数据驻留位置、合规认证与安全风险等级，帮助团队在技术选型时评估数据主权、监管合规与安全暴露面，尤其适用于金融、医疗、政府等高合规要求场景。

---

## 字段结构

```json
"security": {
  "data_residency": "<数据驻留>",
  "compliance": ["<合规标准1>", "<合规标准2>"],
  "risk_level": "<风险等级>",
  "note": "..."   // 可选，补充说明
}
```

> **说明**：`data_residency` 描述数据存储与处理的地理位置；`compliance` 列出已获得的合规认证；`risk_level` 是综合评估的安全风险等级；`note` 补充具体安全注意事项。

---

## `data_residency` — 数据驻留枚举

共 **7 个枚举值**，描述数据的物理存储与处理位置：

| `data_residency` 值 | 中文 | 含义 | 典型条目 |
|--------------------|------|------|---------|
| `self-controlled` | 自主控制 | 数据完全在用户自有基础设施中处理，不离开本地 | Airflow、vLLM、Llama 3、Langfuse |
| `us` | 美国 | 数据在美国数据中心处理，受 US 法律管辖 | ChatGPT、Claude、LangSmith、Cursor |
| `eu` | 欧盟 | 数据在欧盟数据中心处理，受 GDPR 严格保护 | 部分 AWS Bedrock 区域 |
| `cn` | 中国 | 数据在中国境内处理，受中国数据安全法管辖 | 国内部署场景 |
| `any` | 任意区域 | 支持多区域部署，用户可选择数据驻留位置 | AWS Bedrock（多区域）|
| `depends-on-model` | 取决于模型 | 数据驻留位置由所调用的底层模型决定 | Agentic Loop（概念层）|
| `depends-on-impl` | 取决于实现 | 数据驻留位置由具体实现方式决定 | Human-in-the-Loop（概念层）|

---

## `compliance` — 合规认证枚举

列出常见的安全合规认证标准：

| 认证标准 | 全称 | 适用场景 | 代表条目 |
|---------|------|---------|---------|
| `SOC2` | Service Organization Control 2 | 云服务安全控制审计 | ChatGPT、Claude、Cursor、LangSmith |
| `GDPR` | General Data Protection Regulation | 欧盟数据保护法规 | ChatGPT、Claude、n8n、Langfuse |
| `HIPAA` | Health Insurance Portability and Accountability Act | 美国医疗数据保护 | ChatGPT Enterprise、Claude Enterprise |
| `ISO27001` | ISO/IEC 27001 | 信息安全管理体系国际标准 | Gemini、GitHub Copilot、Antigravity |
| `FedRAMP` | Federal Risk and Authorization Management Program | 美国联邦政府云服务认证 | GitHub Copilot Enterprise |
| `PCI-DSS` | Payment Card Industry Data Security Standard | 支付卡行业数据安全标准 | 金融场景专用 |

> **说明**：空数组 `[]` 表示该工具尚未获得正式合规认证，不代表不安全，通常见于开源工具或早期产品。

---

## `risk_level` — 安全风险等级枚举

综合评估数据泄露、滥用与合规违规的风险：

| `risk_level` 值 | 中文 | 含义 | 判断依据 |
|----------------|------|------|---------|
| `low` | 低风险 | 数据自主控制或有强合规保障，风险可控 | 自托管 / 强合规认证 / 无外部数据传输 |
| `medium` | 中等风险 | 数据流经第三方服务器，需评估数据处理协议 | 云 SaaS / 有限合规认证 / 数据可能用于训练 |
| `high` | 高风险 | 自主执行能力强，缺乏人工监督，或数据高度敏感 | 自主 Agent / 浏览器控制 / 无监督执行 |

---

## 各层安全分布

### Hardware 层（物理加速器）

| 条目 | data_residency | compliance | risk_level | 说明 |
|------|---------------|------------|------------|------|
| H100 | `self-controlled` | [] | `low` | 物理硬件，数据完全自主控制 |
| H200 | `self-controlled` | [] | `low` | 物理硬件，数据完全自主控制 |
| A100 | `self-controlled` | [] | `low` | 物理硬件，数据完全自主控制 |
| Apple Silicon | `self-controlled` | [] | `low` | 本地设备，数据不离开本机 |
| Google TPU v5 | `us` | `[SOC2, ISO27001]` | `medium` | Google Cloud 托管，数据在 GCP 处理 |
| Groq LPU | `us` | `[SOC2]` | `medium` | Groq Cloud 推理，数据流经 Groq 服务器 |

### Infra 层（基础设施）

| 条目 | data_residency | compliance | risk_level | 说明 |
|------|---------------|------------|------------|------|
| vLLM | `self-controlled` | [] | `low` | 开源自托管，数据不离开本地 |
| TGI | `self-controlled` | [] | `low` | 开源自托管；HuggingFace 托管版数据在 HF 服务器 |
| Ollama | `self-controlled` | [] | `low` | 纯本地运行，零外部数据传输 |
| PyTorch | `self-controlled` | [] | `low` | 本地训练框架，无数据外传 |
| Unsloth | `self-controlled` | [] | `low` | 本地微调工具，无数据外传 |
| Milvus | `self-controlled` | [] | `low` | 开源自托管；Zilliz Cloud 版数据在云端 |
| Qdrant | `self-controlled` | [] | `low` | 开源自托管；Cloud 版数据在云端 |
| LiteLLM | `self-controlled` | [] | `low` | 代理层自托管；实际数据流向取决于后端模型 |
| AWS Bedrock | `any` | `[SOC2, GDPR, HIPAA, ISO27001]` | `medium` | 企业级合规；数据在所选 AWS 区域处理 |
| CUDA | `self-controlled` | [] | `low` | 本地 GPU 工具包，无数据外传 |
| ROCm | `self-controlled` | [] | `low` | 开源 GPU 工具包，无数据外传 |
| TensorFlow | `self-controlled` | [] | `low` | 开源训练框架，无数据外传 |

### Runtime 层（模型运行时）

| 条目 | data_residency | compliance | risk_level | 说明 |
|------|---------------|------------|------------|------|
| GPT-4o | `us` | `[SOC2, GDPR]` | `medium` | 数据流经 OpenAI 服务器；Enterprise 可关闭训练 |
| o3 | `us` | `[SOC2, GDPR]` | `medium` | 同 GPT-4o；高推理成本场景需评估数据敏感性 |
| Claude 3.7 Sonnet | `us` | `[SOC2, GDPR, HIPAA]` | `medium` | Constitutional AI 安全设计；Enterprise 数据隔离 |
| Gemini 2.5 Pro | `us` | `[SOC2, GDPR, ISO27001]` | `medium` | Google 企业级安全；Workspace 数据默认不用于训练 |
| Llama 3 | `self-controlled` | [] | `low` | 开源权重自托管，数据完全自主控制 |
| Mistral Large | `eu` | `[GDPR]` | `low` | 欧洲公司，GDPR 原生合规；数据在欧盟处理 |
| DeepSeek R1 | `cn` | [] | `medium` | 中国公司；数据可能在中国服务器处理；敏感数据建议自托管 |
| MCP | `self-controlled` | [] | `low` | 开放协议；安全性取决于具体实现 |
| A2A | `self-controlled` | [] | `low` | 开放协议；安全性取决于具体实现 |
| Mem0 | `self-controlled` | [] | `low` | 开源版自托管；Cloud 版数据在 Mem0 服务器 |
| Zep | `self-controlled` | [] | `low` | 开源版自托管；Cloud 版数据在 Zep 服务器 |
| Context Window | `depends-on-model` | [] | `medium` | 安全性完全取决于所使用的底层模型 |

### Patterns 层（推理范式）

| 条目 | data_residency | compliance | risk_level | 说明 |
|------|---------------|------------|------------|------|
| RAG | `depends-on-impl` | [] | `medium` | 检索内容可能包含敏感数据；需控制向量库访问权限 |
| Chain-of-Thought | `depends-on-model` | [] | `low` | 提示技术；安全性取决于底层模型 |
| Prompt Engineering | `depends-on-model` | [] | `low` | 提示技术；注意 Prompt Injection 攻击风险 |
| Function Calling | `depends-on-model` | [] | `medium` | 工具调用可能触发外部系统操作；需严格权限控制 |
| Fine-tuning | `self-controlled` | [] | `low` | 训练数据自主控制；注意训练数据中的敏感信息泄露 |

### Orchestration 层（编排）

| 条目 | data_residency | compliance | risk_level | 说明 |
|------|---------------|------------|------------|------|
| Temporal | `self-controlled` | `[SOC2]` | `low` | 自托管工作流状态；Cloud 版有 SOC2 认证 |
| Prefect | `self-controlled` | `[SOC2]` | `low` | 自托管免费；Cloud 版有 SOC2 认证 |
| Airflow | `self-controlled` | [] | `low` | 完全自托管，数据不离开本地 |
| LangGraph | `self-controlled` | [] | `low` | 开源库自托管；LangGraph Cloud 版数据在 LangChain 服务器 |
| CrewAI | `self-controlled` | [] | `low` | 开源自托管，数据完全自主控制 |
| Dify | `self-controlled` | [] | `low` | 开源自托管；Cloud 版数据在 Dify 服务器 |
| Flowise | `self-controlled` | [] | `low` | 完全开源自托管，数据不离开本地 |
| n8n | `self-controlled` | `[GDPR]` | `low` | 自托管优先；GDPR 合规；Cloud 版数据在欧盟 |
| Zapier | `us` | `[SOC2, GDPR]` | `medium` | 所有数据流经 Zapier 服务器；敏感工作流需评估 |
| Browser Use | `self-controlled` | [] | `medium` | 浏览器 Agent 可访问任意页面内容；建议沙箱执行 |
| Stagehand | `self-controlled` | [] | `medium` | 浏览器控制能力强；需限制可访问的页面范围 |
| Playwright | `self-controlled` | [] | `low` | 本地浏览器自动化，无外部数据传输 |
| LangSmith | `us` | `[SOC2]` | `medium` | Trace 数据（含 Prompt/Response）发送至 LangSmith 服务器 |
| Langfuse | `self-controlled` | `[GDPR]` | `low` | 开源自托管；Trace 数据完全自主控制 |
| Agentic Loop | `depends-on-model` | [] | `high` | 自主执行无监督；需严格限制工具权限与执行范围 |
| Human-in-the-Loop | `self-controlled` | [] | `low` | 人工监督显著降低自主 Agent 风险 |

### Application 层（终端产品）

| 条目 | data_residency | compliance | risk_level | 说明 |
|------|---------------|------------|------------|------|
| ChatGPT | `us` | `[SOC2, GDPR, HIPAA]` | `medium` | 对话可能用于训练；Enterprise 可关闭；建议敏感数据脱敏 |
| Claude | `us` | `[SOC2, GDPR, HIPAA]` | `medium` | Constitutional AI 安全设计；Enterprise 数据隔离 |
| Gemini | `us` | `[SOC2, GDPR, ISO27001]` | `medium` | Workspace 集成；企业版数据默认不用于训练 |
| Cursor | `us` | `[SOC2]` | `medium` | 代码发送至 Cursor 服务器；Privacy Mode 可禁用存储 |
| Antigravity | `us` | `[SOC2, ISO27001]` | `medium` | Google 企业级安全；Enterprise 强数据隔离 |
| GitHub Copilot | `us` | `[SOC2, GDPR, ISO27001, FedRAMP]` | `low` | Enterprise 代码不用于训练；合规认证最完整 |
| Midjourney | `us` | [] | `medium` | 低层级生成图像默认公开；Stealth 模式需 Pro+ |
| Stable Diffusion | `self-controlled` | [] | `low` | 本地运行，无外部数据传输；完全数据主权 |
| ElevenLabs | `us` | `[GDPR]` | `medium` | 语音克隆涉及生物特征数据；平台有滥用检测机制 |
| Perplexity | `us` | `[GDPR]` | `low` | 搜索查询处理；默认不持久化用户数据 |

---

## 安全决策框架

### 数据敏感性分级与工具选型

| 数据敏感级别 | 典型场景 | 推荐 `data_residency` | 推荐 `risk_level` |
|------------|---------|----------------------|-----------------|
| **公开数据** | 通用问答、创意生成 | `us` / `eu` 均可 | `low` / `medium` |
| **内部数据** | 代码、文档、业务流程 | `self-controlled` 优先 | `low` |
| **敏感数据** | 用户 PII、财务数据 | `self-controlled` 必须 | `low` |
| **受监管数据** | 医疗、金融、政府 | `self-controlled` + 合规认证 | `low` + 特定合规 |

### 合规要求快速匹配

| 监管要求 | 必须满足的条件 | 推荐工具类型 |
|---------|-------------|------------|
| **GDPR 合规** | `data_residency: eu` 或 `self-controlled` | Mistral Large、自托管开源工具 |
| **HIPAA 合规** | `compliance` 包含 `HIPAA` | ChatGPT Enterprise、Claude Enterprise、AWS Bedrock |
| **FedRAMP 合规** | `compliance` 包含 `FedRAMP` | GitHub Copilot Enterprise |
| **数据主权** | `data_residency: self-controlled` | 所有开源自托管工具 |
| **中国合规** | `data_residency: cn` 或 `self-controlled` | 自托管 Llama 3、DeepSeek R1 |

### 高风险场景安全加固建议

| 高风险场景 | 涉及条目 | 加固措施 |
|----------|---------|---------|
| **自主 Agent 执行** | Agentic Loop | 限制工具权限、设置 Token 预算、启用 Human-in-the-Loop |
| **浏览器控制** | Browser Use、Stagehand | 沙箱隔离、限制可访问域名、禁止访问敏感系统 |
| **代码发送云端** | Cursor、GitHub Copilot | 启用 Privacy Mode、脱敏敏感变量名 |
| **Trace 数据外传** | LangSmith | 切换至 Langfuse 自托管版 |
| **语音克隆** | ElevenLabs | 严格验证声音授权、启用水印 |

---

## 安全风险热力图

```
                    data_residency
              self-controlled    us/eu      cn
             ┌──────────────┬──────────┬──────────┐
risk_level   │ Airflow      │ ChatGPT  │ DeepSeek │
= low        │ vLLM         │ Claude   │ R1(self) │
             │ Llama 3      │ Gemini   │          │
             │ Langfuse     │ Copilot  │          │
             ├──────────────┼──────────┼──────────┤
risk_level   │ RAG          │ Zapier   │ DeepSeek │
= medium     │ Browser Use  │ LangSmith│ R1(cloud)│
             │ Func Calling │ Cursor   │          │
             ├──────────────┼──────────┼──────────┤
risk_level   │ Agentic Loop │          │          │
= high       │ (无监督执行) │          │          │
             └──────────────┴──────────┴──────────┘
```

> **最安全区间**：`self-controlled` + `risk_level: low` — 以开源自托管工具为代表，适合高合规要求场景。
