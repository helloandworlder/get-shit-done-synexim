# 研究摘要模板

`.planning/research/SUMMARY.md` 模板 — 具有路线图含义的项目研究执行摘要。

<template>

```markdown
# Project Research Summary

**Project:** [name from PROJECT.md]
**Domain:** [inferred domain type]
**Researched:** [date]
**Confidence:** [HIGH/MEDIUM/LOW]

## Executive Summary

[2-3 paragraph overview of research findings]

- What type of product this is and how experts build it
- The recommended approach based on research
- Key risks and how to mitigate them

## Key Findings

### Recommended Stack

[Summary from STACK.md — 1-2 paragraphs]

**Core technologies:**
- [Technology]: [purpose] — [why recommended]
- [Technology]: [purpose] — [why recommended]
- [Technology]: [purpose] — [why recommended]

### Expected Features

[Summary from FEATURES.md]

**Must have (table stakes):**
- [Feature] — users expect this
- [Feature] — users expect this

**Should have (competitive):**
- [Feature] — differentiator
- [Feature] — differentiator

**Defer (v2+):**
- [Feature] — not essential for launch

### Architecture Approach

[Summary from ARCHITECTURE.md — 1 paragraph]

**Major components:**
1. [Component] — [responsibility]
2. [Component] — [responsibility]
3. [Component] — [responsibility]

### Critical Pitfalls

[Top 3-5 from PITFALLS.md]

1. **[Pitfall]** — [how to avoid]
2. **[Pitfall]** — [how to avoid]
3. **[Pitfall]** — [how to avoid]

## Implications for Roadmap

Based on research, suggested phase structure:

### Phase 1: [Name]
**Rationale:** [why this comes first based on research]
**Delivers:** [what this phase produces]
**Addresses:** [features from FEATURES.md]
**Avoids:** [pitfall from PITFALLS.md]

### Phase 2: [Name]
**Rationale:** [why this order]
**Delivers:** [what this phase produces]
**Uses:** [stack elements from STACK.md]
**Implements:** [architecture component]

### Phase 3: [Name]
**Rationale:** [why this order]
**Delivers:** [what this phase produces]

[Continue for suggested phases...]

### Phase Ordering Rationale

- [Why this order based on dependencies discovered]
- [Why this grouping based on architecture patterns]
- [How this avoids pitfalls from research]

### Research Flags

Phases likely needing deeper research during planning:
- **Phase [X]:** [reason — e.g., "complex integration, needs API research"]
- **Phase [Y]:** [reason — e.g., "niche domain, sparse documentation"]

Phases with standard patterns (skip research-phase):
- **Phase [X]:** [reason — e.g., "well-documented, established patterns"]

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| Stack | [HIGH/MEDIUM/LOW] | [reason] |
| Features | [HIGH/MEDIUM/LOW] | [reason] |
| Architecture | [HIGH/MEDIUM/LOW] | [reason] |
| Pitfalls | [HIGH/MEDIUM/LOW] | [reason] |

**Overall confidence:** [HIGH/MEDIUM/LOW]

### Gaps to Address

[Any areas where research was inconclusive or needs validation during implementation]

- [Gap]: [how to handle during planning/execution]
- [Gap]: [how to handle during planning/execution]

## Sources

### Primary (HIGH confidence)
- [Context7 library ID] — [topics]
- [Official docs URL] — [what was checked]

### Secondary (MEDIUM confidence)
- [Source] — [finding]

### Tertiary (LOW confidence)
- [Source] — [finding, needs validation]

---
*Research completed: [date]*
*Ready for roadmap: yes*
```

</template>

<guidelines>

**执行摘要：**
- Write 适合只会阅读本节的人
- 包括关键建议和主要风险
- 最多 2-3 段

**主要发现：**
- 总结，不要重复完整的文档
- 详细文档链接（STACK.md、FEATURES.md 等）
- 关注对路线图决策重要的事情

**对路线图的影响：**
- 这是最重要的部分
- 直接通知路线图创建
- 明确阶段建议和理由
- 包括每个建议阶段的研究标志

**信心评估：**
- 对不确定性保持诚实
- 注意规划过程中需要解决的差距
- 高 = 经官方来源验证
- MEDIUM = 社区共识，多个来源一致同意
- 低 = 单一来源或推断

**与路线图创建集成：**
- 该文件在路线图创建期间作为上下文加载
- 此处的阶段建议成为路线图的起点
- 研究标志告知阶段规划

</guidelines>