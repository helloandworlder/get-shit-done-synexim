# 陷阱研究模板

`.planning/research/PITFALLS.md` 模板 — 项目领域中要避免的常见错误。

<template>

```markdown
# Pitfalls Research

**Domain:** [domain type]
**Researched:** [date]
**Confidence:** [HIGH/MEDIUM/LOW]

## Critical Pitfalls

### Pitfall 1: [Name]

**What goes wrong:**
[Description of the failure mode]

**Why it happens:**
[Root cause — why developers make this mistake]

**How to avoid:**
[Specific prevention strategy]

**Warning signs:**
[How to detect this early before it becomes a problem]

**Phase to address:**
[Which roadmap phase should prevent this]

---

### Pitfall 2: [Name]

**What goes wrong:**
[Description of the failure mode]

**Why it happens:**
[Root cause — why developers make this mistake]

**How to avoid:**
[Specific prevention strategy]

**Warning signs:**
[How to detect this early before it becomes a problem]

**Phase to address:**
[Which roadmap phase should prevent this]

---

### Pitfall 3: [Name]

**What goes wrong:**
[Description of the failure mode]

**Why it happens:**
[Root cause — why developers make this mistake]

**How to avoid:**
[Specific prevention strategy]

**Warning signs:**
[How to detect this early before it becomes a problem]

**Phase to address:**
[Which roadmap phase should prevent this]

---

[Continue for all critical pitfalls...]

## Technical Debt Patterns

Shortcuts that seem reasonable but create long-term problems.

| Shortcut | Immediate Benefit | Long-term Cost | When Acceptable |
|----------|-------------------|----------------|-----------------|
| [shortcut] | [benefit] | [cost] | [conditions, or "never"] |
| [shortcut] | [benefit] | [cost] | [conditions, or "never"] |
| [shortcut] | [benefit] | [cost] | [conditions, or "never"] |

## Integration Gotchas

Common mistakes when connecting to external services.

| Integration | Common Mistake | Correct Approach |
|-------------|----------------|------------------|
| [service] | [what people do wrong] | [what to do instead] |
| [service] | [what people do wrong] | [what to do instead] |
| [service] | [what people do wrong] | [what to do instead] |

## Performance Traps

Patterns that work at small scale but fail as usage grows.

| Trap | Symptoms | Prevention | When It Breaks |
|------|----------|------------|----------------|
| [trap] | [how you notice] | [how to avoid] | [scale threshold] |
| [trap] | [how you notice] | [how to avoid] | [scale threshold] |
| [trap] | [how you notice] | [how to avoid] | [scale threshold] |

## Security Mistakes

Domain-specific security issues beyond general web security.

| Mistake | Risk | Prevention |
|---------|------|------------|
| [mistake] | [what could happen] | [how to avoid] |
| [mistake] | [what could happen] | [how to avoid] |
| [mistake] | [what could happen] | [how to avoid] |

## UX Pitfalls

Common user experience mistakes in this domain.

| Pitfall | User Impact | Better Approach |
|---------|-------------|-----------------|
| [pitfall] | [how users suffer] | [what to do instead] |
| [pitfall] | [how users suffer] | [what to do instead] |
| [pitfall] | [how users suffer] | [what to do instead] |

## "Looks Done But Isn't" Checklist

Things that appear complete but are missing critical pieces.

- [ ] **[Feature]:** Often missing [thing] — verify [check]
- [ ] **[Feature]:** Often missing [thing] — verify [check]
- [ ] **[Feature]:** Often missing [thing] — verify [check]
- [ ] **[Feature]:** Often missing [thing] — verify [check]

## Recovery Strategies

When pitfalls occur despite prevention, how to recover.

| Pitfall | Recovery Cost | Recovery Steps |
|---------|---------------|----------------|
| [pitfall] | LOW/MEDIUM/HIGH | [what to do] |
| [pitfall] | LOW/MEDIUM/HIGH | [what to do] |
| [pitfall] | LOW/MEDIUM/HIGH | [what to do] |

## Pitfall-to-Phase Mapping

How roadmap phases should address these pitfalls.

| Pitfall | Prevention Phase | Verification |
|---------|------------------|--------------|
| [pitfall] | Phase [X] | [how to verify prevention worked] |
| [pitfall] | Phase [X] | [how to verify prevention worked] |
| [pitfall] | Phase [X] | [how to verify prevention worked] |

## Sources

- [Post-mortems referenced]
- [Community discussions]
- [Official "gotchas" documentation]
- [Personal experience / known issues]

---
*Pitfalls research for: [domain]*
*Researched: [date]*
```

</template>

<guidelines>

**关键陷阱：**
- 关注特定领域的问题，而不是一般性错误
- 包括警告信号——及早发现可以预防灾难
- 链接到特定阶段——使陷阱变得可操作

**技术债务：**
- 现实一些——一些捷径是可以接受的
- 请注意快捷方式“永远不可接受”与“仅在 MVP 中”的情况
- 包括长期成本以告知权衡决策

**性能陷阱：**
- 包括规模阈值（“突破 10,000 个用户”）
- 关注与该项目预期规模相关的内容
- 不要针对假设规模进行过度设计

**安全错误：**
- 超越 OWASP 基础知识 — 特定领域的问题
- 示例：社区平台的安全性 concerns 与电子商务不同
- 包括优先考虑的风险级别

**“看起来完成但实际上没有”：**
- 执行期间验证的清单格式
- 演示与生产中常见
- 防止“它可以在我的机器上运行”问题

**陷阱到阶段映射：**
- 对于路线图创建至关重要
- 每个陷阱都应该映射到一个可以防止它发生的阶段
- 告知阶段顺序和成功标准

</guidelines>