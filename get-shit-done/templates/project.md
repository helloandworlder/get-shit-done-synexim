# PROJECT.md 模板

`.planning/PROJECT.md` 的模板 — 实时项目上下文文档。

<template>

```markdown
# [Project Name]

## What This Is

[Current accurate description — 2-3 sentences. What does this product do and who is it for?
Use the user's language and framing. Update whenever reality drifts from this description.]

## Core Value

[The ONE thing that matters most. If everything else fails, this must work.
One sentence that drives prioritization when tradeoffs arise.]

## Requirements

### Validated

<!-- Shipped and confirmed valuable. -->

(None yet — ship to validate)

### Active

<!-- Current scope. Building toward these. -->

- [ ] [Requirement 1]
- [ ] [Requirement 2]
- [ ] [Requirement 3]

### Out of Scope

<!-- Explicit boundaries. Includes reasoning to prevent re-adding. -->

- [Exclusion 1] — [why]
- [Exclusion 2] — [why]

## Context

[Background information that informs implementation:
- Technical environment or ecosystem
- Relevant prior work or experience
- User research or feedback themes
- Known issues to address]

## Constraints

- **[Type]**: [What] — [Why]
- **[Type]**: [What] — [Why]

Common types: Tech stack, Timeline, Budget, Dependencies, Compatibility, Performance, Security

## Key Decisions

<!-- Decisions that constrain future work. Add throughout project lifecycle. -->

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| [Choice] | [Why] | [✓ Good / ⚠️ Revisit / — Pending] |

---
*Last updated: [date] after [trigger]*
```

</template>

<guidelines>

**这是什么：**
- 产品的当前准确描述
- 用 2-3 句话描述它的用途和用途
- 使用用户的话语和框架
- 当产品发展超出此描述时进行更新

**核心价值：**
- 最重要的事情
- 其他一切都可能失败；这不能
- 当出现权衡时推动优先级
- 很少改变；如果确实如此，这将是一个重要的转折点

**要求 - 已验证：**
- 已交付并证明有价值的需求
- 格式：`- ✓ [Requirement] — [version/phase]`
- 这些已锁定 - 更改它们需要明确的讨论

**要求 - 活跃：**
- 当前范围正在构建
- 在发货和验证之前，这些都是假设
- 发货时移至“已验证”，如果无效则超出范围

**要求 - 超出范围：**
- 对我们不构建的内容有明确的界限
- 始终包含推理（防止以后重新添加）
- 包括：考虑并拒绝、推迟到未来、明确排除

**上下文：**
- 为实施决策提供信息的背景
- 技术环境、前期工作、用户反馈
- 需要解决的已知问题或技术债务
- 随着新环境的出现而更新

**限制：**
- 对实施选择的硬性限制
- 技术堆栈、时间表、预算、兼容性、依赖性
- 包括“为什么”——没有理由的约束会受到质疑

**关键决策：**
- 影响未来工作的重大选择
- 添加在整个项目中做出的决策
- 已知情况下跟踪结果：
  - ✓ 好 — decision 被证明是正确的
  - ⚠️ 重新访问 — decision 可能需要重新考虑
  - - 待定 - 评估还为时过早

**最后更新：**
- 始终注意文档更新的时间和原因
- 格式：`after Phase 2` 或 `after v1.0 milestone`
- 触发内容是否仍然准确的审查

</guidelines>

<evolution>

PROJECT.md 在整个项目生命周期中不断发展。

**每次相变后：**
1. 要求无效？ → 有理由移至范围之外
2. 要求已验证？ → 移至使用相位参考进行验证
3、新的需求出现了？ → 添加到活动
4. 记录的决定？ → 添加到关键决策
5.“这是什么”仍然准确吗？ → 如果有偏差则更新

**每个里程碑之后：**
1. 全面审查所有部分
2. 核心价值检查——仍然是正确的优先事项吗？
3. 审计超出范围——原因仍然有效吗？
4. 使用当前状态更新上下文（用户、反馈、指标）

</evolution>

<brownfield>

对于现有的代码库：

1. **首先通过 `/gsd:map-codebase` 映射代码库**

2. **从现有代码推断已验证的要求**：
   - 代码库实际上是做什么的？
   - 建立了哪些模式？
   - 什么是明显有效且依赖​​的？

3. **从用户那里收集主动需求**：
   - 当前推断的当前状态
   - 询问他们下一步想要构建什么

4. **初始化：**
   - 已验证 = 从现有代码推断
   - Active = 用户对此工作的目标
   - 超出范围 = 用户指定的边界
   - 上下文 = 包括当前代码库状态

</brownfield>

<state_reference>

STATE.md参考PROJECT.md：

```markdown
## Project Reference

See: .planning/PROJECT.md (updated [date])

**Core value:** [One-liner from Core Value section]
**Current focus:** [Current phase name]
```

这确保 Claude 读取当前的 PROJECT.md 上下文。

</state_reference>