# 特征研究模板

`.planning/research/FEATURES.md` 模板 — 项目域的功能景观。

<template>

```markdown
# Feature Research

**Domain:** [domain type]
**Researched:** [date]
**Confidence:** [HIGH/MEDIUM/LOW]

## Feature Landscape

### Table Stakes (Users Expect These)

Features users assume exist. Missing these = product feels incomplete.

| Feature | Why Expected | Complexity | Notes |
|---------|--------------|------------|-------|
| [feature] | [user expectation] | LOW/MEDIUM/HIGH | [implementation notes] |
| [feature] | [user expectation] | LOW/MEDIUM/HIGH | [implementation notes] |
| [feature] | [user expectation] | LOW/MEDIUM/HIGH | [implementation notes] |

### Differentiators (Competitive Advantage)

Features that set the product apart. Not required, but valuable.

| Feature | Value Proposition | Complexity | Notes |
|---------|-------------------|------------|-------|
| [feature] | [why it matters] | LOW/MEDIUM/HIGH | [implementation notes] |
| [feature] | [why it matters] | LOW/MEDIUM/HIGH | [implementation notes] |
| [feature] | [why it matters] | LOW/MEDIUM/HIGH | [implementation notes] |

### Anti-Features (Commonly Requested, Often Problematic)

Features that seem good but create problems.

| Feature | Why Requested | Why Problematic | Alternative |
|---------|---------------|-----------------|-------------|
| [feature] | [surface appeal] | [actual problems] | [better approach] |
| [feature] | [surface appeal] | [actual problems] | [better approach] |

## Feature Dependencies

```
[Feature A]
    └──需要──> [Feature B]
                       └──需要──> [Feature C]

[Feature D] ──增强──> [Feature A]

[Feature E]──冲突──> [Feature F]
```

### Dependency Notes

- **[Feature A] requires [Feature B]:** [why the dependency exists]
- **[Feature D] enhances [Feature A]:** [how they work together]
- **[Feature E] conflicts with [Feature F]:** [why they're incompatible]

## MVP Definition

### Launch With (v1)

Minimum viable product — what's needed to validate the concept.

- [ ] [Feature] — [why essential]
- [ ] [Feature] — [why essential]
- [ ] [Feature] — [why essential]

### Add After Validation (v1.x)

Features to add once core is working.

- [ ] [Feature] — [trigger for adding]
- [ ] [Feature] — [trigger for adding]

### Future Consideration (v2+)

Features to defer until product-market fit is established.

- [ ] [Feature] — [why defer]
- [ ] [Feature] — [why defer]

## Feature Prioritization Matrix

| Feature | User Value | Implementation Cost | Priority |
|---------|------------|---------------------|----------|
| [feature] | HIGH/MEDIUM/LOW | HIGH/MEDIUM/LOW | P1/P2/P3 |
| [feature] | HIGH/MEDIUM/LOW | HIGH/MEDIUM/LOW | P1/P2/P3 |
| [feature] | HIGH/MEDIUM/LOW | HIGH/MEDIUM/LOW | P1/P2/P3 |

**Priority key:**
- P1: Must have for launch
- P2: Should have, add when possible
- P3: Nice to have, future consideration

## Competitor Feature Analysis

| Feature | Competitor A | Competitor B | Our Approach |
|---------|--------------|--------------|--------------|
| [feature] | [how they do it] | [how they do it] | [our plan] |
| [feature] | [how they do it] | [how they do it] | [our plan] |

## Sources

- [Competitor products analyzed]
- [User research or feedback sources]
- [Industry standards referenced]

---
*Feature research for: [domain]*
*Researched: [date]*
```

</template>

<guidelines>

**赌桌赌注：**
- 这些对于发布来说是不可协商的
- 用户不会因为拥有它们而给予赞扬，而是因为错过它们而受到惩罚
- 示例：没有用户配置文件的社区平台已损坏

**差异化因素：**
- 这些是你竞争的地方
- 应与 PROJECT.md 的核心价值保持一致
- 不要试图在所有事情上都与众不同

**反特征：**
- 通过记录看似不错但实际并不好的内容来防止范围蔓延
- 包括替代方法
- 示例：“实时一切”通常会带来没有价值的复杂性

**功能依赖性：**
- 对于路线图阶段排序至关重要
- 如果A需要B，B必须处于较早阶段
- 冲突告诉我们哪些内容不能在同一阶段结合

**MVP 定义：**
- 对真正最低限度的事情要毫不留情
- “很高兴拥有”不是 MVP
- 以更少的资源启动，验证，然后扩展

</guidelines>