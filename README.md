# Project Inception Skill

## 概述

**Project Inception** 是一个用于 Codex 和 VS Code 的 Skill，用于指导软件项目从初始构想经过批准的需求、DDD 启发的领域设计、生命周期和扩展设计、技术选择、技术架构，最后到解耦的实现计划。

该 Skill 强制执行明确的批准门禁，确保项目设计的完整性和可追溯性。**在此 Skill 激活时，不允许脚手架搭建、编码、安装依赖或实现行为。**

## 核心特性

### 1. 项目设计流程（6 个阶段）

- **Phase 0**: 探索上下文 - 检查现有文件、文档、代码、版本历史和约束条件
- **Phase 1**: 需求分析 - 建立项目目的、用户、范围、成功指标、交付阶段
- **Phase 2**: 领域和业务分解 - DDD 建模、界限上下文、聚合、实体、值对象、领域事件
- **Phase 3**: 生命周期和扩展设计 - 状态转移、失败路径、恢复、模式评估、扩展机制
- **Phase 4**: 技术和架构 - 定量约束、技术选型、运行时组件、依赖关系、持久化、可观测性
- **Phase 5**: 实现规划 - 路线图、任务分解、里程碑、集成点、完整可追溯性

### 2. 工作顺序：Whole, Parts, Safety Net

每个阶段都遵循：

1. **Whole**: 整体目标、边界、主流程、主要业务地图、管制约束
2. **Parts**: 分解复杂能力、上下文、职责、流程、计划
3. **Safety Net**: 审计遗漏、跨边界流、异常路径、降级、回滚、决策追踪中断

**不要** 从设计孤立的类、表、API、插件或 UI 组件开始。

### 3. 核心规则

- 使用 `$brainstorming` 逐个澄清意图
- 优先使用事实而非假设
- 分离业务需求和实现选择
- 按比例应用 DDD（记录为什么选择完整、轻量或最小建模）
- 在选择模式前识别生命周期和实际变化点
- 记录为何选择或拒绝某个模式/中间件/插件
- 从量化约束选择技术（明确说明何时不需要中间件）
- 维护完整的需求到测试可追溯链
- 复杂职责得到自己的文档；简单职责保留在概览中（约 10-20 行）
- 实现计划与需求和设计文档分开

### 4. 批准门禁

- ✋ **不允许** 在此 Skill 活跃时进行脚手架、编码或实现
- 每个阶段必须通过 self-review 和用户显式批准
- 上游变更触发下游文档标记为过时并返回最早受影响的阶段

## 使用场景

在以下情况下使用此 Skill：

- 🚀 开始新的软件项目
- 🔄 重启设计不足的项目
- 📋 编码前分解需求
- 🏗️ 用户要求项目启动、需求分析、业务/领域设计、架构设计或实现规划

## 使用方法

### 通过 Codex/Copilot Chat

```
Use $project-inception to guide this project from requirements to approved plans
```

或

```
I need to design a new project for [your project description]
```

## 文档结构

Skill 指导创建的项目文档结构：

```
docs/project/
├── 00-index.md                    # 导航和批准状态
├── requirements/
│   ├── 00-overview.md             # 用户、范围、场景、交付阶段
│   ├── 01-scope-and-constraints.md # 包含/排除、假设、约束
│   └── <capability>-requirements.md # 复杂能力的详细需求
├── domain/
│   ├── 00-domain-map.md           # 领域、上下文、参与者、流
│   └── <context>-design.md        # 每个上下文的 DDD 设计
├── responsibilities/
│   ├── 00-responsibility-map.md   # 职责、所有者、依赖
│   └── <responsibility>-design.md # 复杂职责的详细设计
├── architecture/
│   ├── 00-lifecycle-and-extension-model.md # 生命周期、状态、模式
│   ├── 01-technical-selection.md          # 架构决策记录 (ADR)
│   └── 02-technical-architecture.md       # 运行时组件、依赖、APIs
└── plans/
    ├── 00-roadmap.md               # 里程碑、依赖顺序、集成序列
    └── <responsibility>-plan.md    # 复杂职责的实现计划

references/                         # Skill 参考文档
├── document-structure.md           # 文档分离规则和元数据格式
├── requirements.md                 # 需求编写指南
├── domain-design.md                # DDD 建模指南
├── responsibility-design.md        # 职责设计指南
├── lifecycle-and-patterns.md       # 生命周期和模式决策表
├── technical-architecture.md       # 架构指南和解耦规则
├── implementation-planning.md      # 实现顺序和计划内容
└── final-audit.md                  # 最终完整性检查单
```

## 可追溯性 ID 格式

```
REQ-<AREA>-001      # 需求 ID
CTX-<NAME>          # 上下文 ID
RESP-<NAME>         # 职责 ID
ADR-001             # 架构决策记录
PLAN-<AREA>-001     # 实现计划 ID
TEST-<AREA>-001     # 测试 ID
```

### 完整追溯链

```
Requirement
  ↓ (maps to)
Bounded Context
  ↓ (owns)
Responsibility
  ↓ (implemented via)
Architecture Decision
  ↓ (decomposed into)
Implementation Plan
  ↓ (verified by)
Acceptance Test
```

## 批准记录

每个受管文档应以元数据开头：

```yaml
Document ID: REQ-CORE-001
Status: Draft | Approved | Superseded
Approved by: <user or role>
Approved at: <date>
Depends on: [document IDs]
Supersedes: [document IDs]
```

## 强制门禁 (Hard Gate)

### 不允许在此 Skill 激活时：
- ❌ 脚手架搭建
- ❌ 编码或实现
- ❌ 安装项目依赖
- ❌ 实现行为

### 进入下一阶段的条件：
1. 当前阶段文档通过 self-review（使用相应的安全网审计）
2. 用户显式批准整个阶段

### 上游变更处理：
如果用户改变已批准的上游决策，受影响的下游文档标记为 **Superseded**，工作流返回最早受影响的阶段。

## 最佳实践

1. **严格按顺序**: 完成一个阶段才进入下一个，不跳跃
2. **显式批准**: 对完整的阶段内容进行明确批准，不接受隐式同意
3. **Whole 优先**: 每个阶段从整体开始，再分解复杂部分
4. **事实优先**: 优先使用现有代码和文档的事实，而不是假设
5. **完整追溯**: 确保从需求到接受测试的完整链
6. **记录决策**: 清晰记录为什么接纳或拒绝每个选择

## 文档分离规则

| 类别 | 包含内容 | 不包含内容 |
|------|---------|---------|
| 需求 | 用户需求、业务规则、约束、接受标准 | 框架设计、类设计 |
| 领域 | 业务语言、上下文、聚合、规则、事件 | 实现技术、UI/存储 |
| 职责 | 边界、合约、依赖、错误处理、扩展点 | 特定类名、数据库表 |
| 架构 | 生命周期、模式决策、技术选型、运行时 | 实现步骤、代码 |
| 计划 | 顺序、依赖、里程碑、集成、接受检查 | 架构决策、需求 |

## 自适应文档分割

**保留在概览中**：当 10-20 行能完整定义时

**创建独立文档**：当项目有以下特征时
- 独立的工作流或生命周期
- 多个状态或转移
- 非平凡的业务规则
- 公共合约或集成边界
- 专用数据模型
- 多个失败模式
- 安全、性能或迁移风险
- 多个实现里程碑

## 每个阶段的安全网审计

见 [references/](references/) 目录中的相应指南：

- **需求安全网**: [requirements.md](references/requirements.md)
- **领域安全网**: [domain-design.md](references/domain-design.md)
- **职责安全网**: [responsibility-design.md](references/responsibility-design.md)
- **生命周期和扩展安全网**: [lifecycle-and-patterns.md](references/lifecycle-and-patterns.md)
- **架构安全网**: [technical-architecture.md](references/technical-architecture.md)
- **最终完整性审计**: [final-audit.md](references/final-audit.md)

## 常见问题

| 问题 | 解决方案 |
|------|---------|
| 如何知道 DDD 建模的深度？ | 见 [domain-design.md](references/domain-design.md) 的"Decide DDD Depth" |
| 何时拆分文档？ | 见 [document-structure.md](references/document-structure.md) 的"Adaptive Splitting" |
| 需求何时测试不足？ | 见 [requirements.md](references/requirements.md) 的"Requirement Quality" |
| 如何处理跨上下文的流？ | 见 [domain-design.md](references/domain-design.md) 的"Bounded Context Design" |
| 何时使用模式？ | 见 [lifecycle-and-patterns.md](references/lifecycle-and-patterns.md) 的"Pattern Decision Table" |
| 如何避免无批准的实现跳跃？ | 使用 [final-audit.md](references/final-audit.md) 的"Traceability"部分 |

## 关键文件

- **SKILL.md** - Skill 完整定义和工作流
- **references/** - 每个阶段的详细指南
  - [document-structure.md](references/document-structure.md) - 文档组织
  - [requirements.md](references/requirements.md) - 需求编写
  - [domain-design.md](references/domain-design.md) - DDD 建模
  - [responsibility-design.md](references/responsibility-design.md) - 职责划分
  - [lifecycle-and-patterns.md](references/lifecycle-and-patterns.md) - 生命周期和模式
  - [technical-architecture.md](references/technical-architecture.md) - 架构设计
  - [implementation-planning.md](references/implementation-planning.md) - 实现规划
  - [final-audit.md](references/final-audit.md) - 最终检查单

## 版本历史

### v1.0.0 (2026-06-22)
- 初始发布
- 完整的 6 阶段项目设计流程
- Whole, Parts, Safety Net 工作顺序
- 强制批准门禁
- 需求到测试的完整可追溯性
- DDD 和生命周期建模
- 文档分离和自适应规则

## 许可证

MIT

