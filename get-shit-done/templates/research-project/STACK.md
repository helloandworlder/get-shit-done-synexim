# 堆栈研究模板

`.planning/research/STACK.md` 模板 — 项目领域的推荐技术。

<template>

```markdown
# Stack Research

**Domain:** [domain type]
**Researched:** [date]
**Confidence:** [HIGH/MEDIUM/LOW]

## Recommended Stack

### Core Technologies

| Technology | Version | Purpose | Why Recommended |
|------------|---------|---------|-----------------|
| [name] | [version] | [what it does] | [why experts use it for this domain] |
| [name] | [version] | [what it does] | [why experts use it for this domain] |
| [name] | [version] | [what it does] | [why experts use it for this domain] |

### Supporting Libraries

| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| [name] | [version] | [what it does] | [specific use case] |
| [name] | [version] | [what it does] | [specific use case] |
| [name] | [version] | [what it does] | [specific use case] |

### Development Tools

| Tool | Purpose | Notes |
|------|---------|-------|
| [name] | [what it does] | [configuration tips] |
| [name] | [what it does] | [configuration tips] |

## Installation

```bash
# 核心
npm 安装 [packages]

# 支持
npm 安装 [packages]

# 开发依赖
npm安装-D [packages]
```

## Alternatives Considered

| Recommended | Alternative | When to Use Alternative |
|-------------|-------------|-------------------------|
| [our choice] | [other option] | [conditions where alternative is better] |
| [our choice] | [other option] | [conditions where alternative is better] |

## What NOT to Use

| Avoid | Why | Use Instead |
|-------|-----|-------------|
| [technology] | [specific problem] | [recommended alternative] |
| [technology] | [specific problem] | [recommended alternative] |

## Stack Patterns by Variant

**If [condition]:**
- Use [variation]
- Because [reason]

**If [condition]:**
- Use [variation]
- Because [reason]

## Version Compatibility

| Package A | Compatible With | Notes |
|-----------|-----------------|-------|
| [package@version] | [package@version] | [compatibility notes] |

## Sources

- [Context7 library ID] — [topics fetched]
- [Official docs URL] — [what was verified]
- [Other source] — [confidence level]

---
*Stack research for: [domain]*
*Researched: [date]*
```

</template>

<guidelines>

**核心技术：**
- 包括特定版本号
- 解释为什么这是 standard 选择，而不仅仅是它的用途
- 关注影响架构决策的技术

**支持库：**
- 包括该领域常用的库
- 注意何时需要每个库（并非所有项目都需要所有库）

**替代方案：**
- 不要只是放弃替代方案
- 解释替代方案何时有意义
- 如果用户不同意，帮助他们做出明智的决定

**不应该使用什么：**
- 主动警告过时或有问题的选择
- 解释具体问题，而不仅仅是“它是旧的”
- 提供推荐的替代方案

**版本兼容性：**
- 注意任何已知的兼容性问题
- 对于避免以后的调试时间至关重要

</guidelines>