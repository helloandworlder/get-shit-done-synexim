# 架构研究模板

`.planning/research/ARCHITECTURE.md` 模板 — 项目域的系统结构模式。

<template>

```markdown
# Architecture Research

**Domain:** [domain type]
**Researched:** [date]
**Confidence:** [HIGH/MEDIUM/LOW]

## Standard Architecture

### System Overview

```
┌──────────────────────────────────────────────────────────────┐
│ [Layer Name] │
├──────────────────────────────────────────────────────────────┤
│ ┌──────────┐ ┌────────┐ ┌──────────┐ ┌──────────┐ │
│ │ [Comp] │ │ [Comp] │ │ [Comp] │ │ [Comp] │ │
│ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ │
│ │ │ │ │ │
├────────┴────────────┴────────────┴────────────┴──────────────┤
│ [Layer Name] │
├──────────────────────────────────────────────────────────────┤
│ ┌────────────────────────────────────────────────────┐ │
│ │ [Component] │ │
│ └────────────────────────────────────────────────────┘ │
├──────────────────────────────────────────────────────────────┤
│ [Layer Name] │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ │
│ │ [Store] │ │ [Store] │ │ [Store] │ │
│ └──────────┘ └──────────┘ └──────────┘ │
└──────────────────────────────────────────────────────────────┘
```

### Component Responsibilities

| Component | Responsibility | Typical Implementation |
|-----------|----------------|------------------------|
| [name] | [what it owns] | [how it's usually built] |
| [name] | [what it owns] | [how it's usually built] |
| [name] | [what it owns] | [how it's usually built] |

## Recommended Project Structure

```
源代码/
├── [folder]/#[purpose]
│ ├── [subfolder]/ # [purpose]
│ └── index.ts # [purpose]
├── [folder]/#[purpose]
│ ├── [subfolder]/ # [purpose]
│ └── types.ts # [purpose]
├── [folder]/#[purpose]
└── [folder]/#[purpose]
```

### Structure Rationale

- **[folder]/:** [why organized this way]
- **[folder]/:** [why organized this way]

## Architectural Patterns

### Pattern 1: [Pattern Name]

**What:** [description]
**When to use:** [conditions]
**Trade-offs:** [pros and cons]

**Example:**
```打字稿
// [Brief code example showing the pattern]
```

### Pattern 2: [Pattern Name]

**What:** [description]
**When to use:** [conditions]
**Trade-offs:** [pros and cons]

**Example:**
```打字稿
// [Brief code example showing the pattern]
```

### Pattern 3: [Pattern Name]

**What:** [description]
**When to use:** [conditions]
**Trade-offs:** [pros and cons]

## Data Flow

### Request Flow

```
[User Action]
    ↓
[Component] → [Handler] → [Service] → [Data Store]
    ↓ ↓ ↓ ↓
[Response] ← [Transform] ← [Query] ← [Database]
```

### State Management

```
[State Store]
    ↓（订阅）
[Components] ←→ [Actions] → [Reducers/Mutations] → [State Store]
```

### Key Data Flows

1. **[Flow name]:** [description of how data moves]
2. **[Flow name]:** [description of how data moves]

## Scaling Considerations

| Scale | Architecture Adjustments |
|-------|--------------------------|
| 0-1k users | [approach — usually monolith is fine] |
| 1k-100k users | [approach — what to optimize first] |
| 100k+ users | [approach — when to consider splitting] |

### Scaling Priorities

1. **First bottleneck:** [what breaks first, how to fix]
2. **Second bottleneck:** [what breaks next, how to fix]

## Anti-Patterns

### Anti-Pattern 1: [Name]

**What people do:** [the mistake]
**Why it's wrong:** [the problem it causes]
**Do this instead:** [the correct approach]

### Anti-Pattern 2: [Name]

**What people do:** [the mistake]
**Why it's wrong:** [the problem it causes]
**Do this instead:** [the correct approach]

## Integration Points

### External Services

| Service | Integration Pattern | Notes |
|---------|---------------------|-------|
| [service] | [how to connect] | [gotchas] |
| [service] | [how to connect] | [gotchas] |

### Internal Boundaries

| Boundary | Communication | Notes |
|----------|---------------|-------|
| [module A ↔ module B] | [API/events/direct] | [considerations] |

## Sources

- [Architecture references]
- [Official documentation]
- [Case studies]

---
*Architecture research for: [domain]*
*Researched: [date]*
```

</template>

<guidelines>

**系统概述：**
- 为了清晰起见，使用 ASCII 框图（├── └── │ ─ 仅用于结构可视化）
- 显示主要组件及其关系
- 不要过于详细——这是概念性的，而不是实现性的

**项目结构：**
- 具体说明文件夹组织
- 解释分组的理由
- 匹配所选堆栈的约定

**图案：**
- 包括有用的代码示例
- 诚实地解释权衡
- 注意模式对于小型项目的杀伤力

**缩放考虑因素：**
- 现实一点——大多数项目不需要规模达到数百万
- 关注“首先突破的是什么”而不是理论限制
- 避免过早的优化建议

**反模式：**
- 特定于该域
- 包括要做什么
- 有助于防止实施过程中的常见错误

</guidelines>
