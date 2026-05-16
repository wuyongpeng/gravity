# Changelog

All notable changes to the AI Technology Ontology will be documented in this file.

## [1.1.0] - 2025-05-16

### 🎯 重大架构调整：L4 Reasoning 层重新定位

#### Added
- **L2 Infra**: 新增 "State & Memory" 组
  - 从 L3 移入 Mem0 (id: 15)
  - 从 L3 移入 Zep (id: 16)
  
- **L4 Reasoning**: 新增 "Context Constraint" 组
  - 从 L3 移入 Context Window (id: 42)
  
- **文档**: 新增 `ARCHITECTURE_RATIONALE.md` 详细说明架构设计理念

#### Changed
- **L3 Runtime**: 重新定义为 "Models & Protocols"
  - 移除 "Memory & Context" 组
  - 更新 subtitle: "Models, Protocols & Memory" → "Models & Protocols"
  - 更新 description: 强调"标准接口层"定位
  - 更新 group_types: 移除 "Memory & Context"
  
- **L4 层重命名**: "Techniques" → "Reasoning"
  - 文件重命名: `L4_techniques.json` → `L4_reasoning.json`
  - category: "Techniques" → "Reasoning"
  - subtitle: "AI Reasoning Techniques" → "Reasoning Paradigms"
  - description: 强调"认知逻辑层"定位
  - 所有 radar.group: "Reasoning Technique" → "Reasoning Paradigm"
  
- **README.md**: 全面更新
  - 架构图更新（反映 L4 新定位）
  - 新增"为什么 L4 Reasoning 是架构的灵魂？"章节
  - 更新设计原则（强调三层角色划分）
  - 更新统计数据（80 → 81 条目）
  - 更新文件列表（L4_techniques.json → L4_reasoning.json）

- **LA_overall.json**: 更新汇总文件
  - layer_order: "patterns" → "reasoning"
  - layers.patterns → layers.reasoning
  - 更新 category、subtitle、description

#### Statistics
| 层级 | v1.0 | v1.1 | 变化 |
|------|------|------|------|
| L1 Hardware | 14 | 14 | - |
| L2 Infra | 16 | 18 | +2 |
| L3 Runtime | 15 | 13 | -2 |
| L4 Reasoning | 5 | 6 | +1 |
| L5 Orchestration | 17 | 17 | - |
| L6 Application | 13 | 13 | - |
| **总计** | **80** | **81** | **+1** |

#### Rationale

**核心理念**: L4 Reasoning 是架构的灵魂，代表"认知逻辑层"

1. **Mem0/Zep → L2**: 本质是持久化存储基础设施，与向量数据库同属存储层
2. **Context Window → L4**: 是推理范式的约束概念，影响 RAG、记忆、Prompt 设计
3. **L4 重命名**: "Reasoning Paradigms" 更准确表达认知逻辑层的定位

**三层角色划分**:
- L1-L3: Capability Providers（能力提供者）
- L4: Cognitive Logic（认知逻辑）
- L5-L6: Capability Consumers（能力消费者）

---

## [1.0.0] - 2025-05-15

### Initial Release

#### Added
- 6 层架构定义
  - L1 Hardware: 14 条目
  - L2 Infra: 16 条目
  - L3 Runtime: 15 条目
  - L4 Techniques: 5 条目
  - L5 Orchestration: 17 条目
  - L6 Application: 13 条目

- 9 个视角维度
  - Radar (技术雷达)
  - Deployment (部署模式)
  - Lifecycle (生命周期)
  - Performance (性能效率)
  - Stack (技术栈定位)
  - Cost (成本模型)
  - Security (安全合规)
  - Openness (开放性)
  - Decision (战略定位)

- 完整的 README.md 文档
- 6 个层级的 JSON 数据文件
- LA_overall.json 汇总文件

#### Features
- 结构化的技术条目定义
- 多维度视角分析
- 关系类型定义（alternative, depends, ecosystem 等）
- 技术雷达成熟度评估
- 成本模型分类
- 安全合规标注

---

## 版本规范

本项目遵循 [Semantic Versioning](https://semver.org/):

- **MAJOR**: 架构层级调整、核心概念变更
- **MINOR**: 新增条目、新增视角、组织结构优化
- **PATCH**: 条目信息更新、错误修正、文档改进

---

**维护者**: AI Technology Ontology Team  
**仓库**: https://github.com/your-repo/ai-ontology
