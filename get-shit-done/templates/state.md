# 状态模板

`.planning/STATE.md` 的模板 — 该项目的鲜活记忆。

---

## 文件模板

```markdown
# Project State

## Project Reference

See: .planning/PROJECT.md (updated [date])

**Core value:** [One-liner from PROJECT.md Core Value section]
**Current focus:** [Current phase name]

## Current Position

Phase: [X] of [Y] ([Phase name])
Plan: [A] of [B] in current phase
Status: [Ready to plan / Planning / Ready to execute / In progress / Phase complete]
Last activity: [YYYY-MM-DD] — [What happened]

Progress: [░░░░░░░░░░] 0%

## Performance Metrics

**Velocity:**
- Total plans completed: [N]
- Average duration: [X] min
- Total execution time: [X.X] hours

**By Phase:**

| Phase | Plans | Total | Avg/Plan |
|-------|-------|-------|----------|
| - | - | - | - |

**Recent Trend:**
- Last 5 plans: [durations]
- Trend: [Improving / Stable / Degrading]

*Updated after each plan completion*

## Accumulated Context

### Decisions

Decisions are logged in PROJECT.md Key Decisions table.
Recent decisions affecting current work:

- [Phase X]: [Decision summary]
- [Phase Y]: [Decision summary]

### Pending Todos

[From .planning/todos/pending/ — ideas captured during sessions]

None yet.

### Blockers/Concerns

[Issues that affect future work]

None yet.

## Session Continuity

Last session: [YYYY-MM-DD HH:MM]
Stopped at: [Description of last completed action]
Resume file: [Path to .continue-here*.md if exists, otherwise "None"]
```

<purpose>

STATE.md 是该项目跨越所有阶段和会话的短期记忆。

**它解决的问题：** 信息是在摘要、问题和决策中捕获的，但没有系统地使用。会话在没有上下文的情况下开始。

**解决方案：** 单个小文件：
- Read 在每个工作流程中都是第一位
- 在每次重大行动后更新
- 包含累积上下文的摘要
- 启用即时会话恢复

</purpose>

<lifecycle>

**创建：** ROADMAP.md 创建后（init 期间）
- 参考 PROJECT.md（阅读当前上下文）
- 初始化空的累积上下文部分
- 将位置设置为“第一阶段准备好计划”

**阅读：** 每个工作流程的第一步
- 进度：向用户呈现状态
- 计划：告知规划决策
- 执行：了解当前位置
- 过渡：知道什么是完整的

**写作：** 在每次重大行动之后
- 执行：SUMMARY.md创建后
  - 更新位置（阶段、计划、状态）
  - 注意新的决定（详情见PROJECT.md）
  - 添加拦截器/concerns
- 转换：阶段标记完成后
  - 更新进度条
  - 清除已解决的拦截器
  - 刷新项目参考日期

</lifecycle>

<sections>

### 项目参考
指向 PROJECT.md 以获取完整上下文。包括：
- 核心价值（重要的一件事）
- 当前焦点（哪个阶段）
- 最后更新日期（如果过时则触发重新读取）

Claude 直接读取 PROJECT.md 的需求、约束和决策。

### 当前位置
我们现在所处的位置：
- Y 相 X — 哪个相
- B 计划 A — 阶段内的计划
- 状态 — 当前状态
- 上次活动 — 最近发生的事情
- 进度条——总体完成情况的视觉指示器

进度计算：（已完成计划）/（各阶段计划总和）×100%

### 性能指标
跟踪速度以了解执行模式：
- 已完成的总计划
- 每个计划的平均持续时间
- 每相故障
- 近期趋势（改善/稳定/下降）

每个计划完成后更新。

### 累积的上下文

**决策：** 参考 PROJECT.md 关键决策表，以及最近的决策摘要以供快速访问。完整的 decision 日志位于 PROJECT.md 中。

**待处理的待办事项：** 通过 /gsd:add-todo 捕获的想法
- 待办事项计数
- 参考.planning/todos/pending/
- 如果少则简要列出，如果多则计数（e.g.，“5 个待办事项 - 参见 /gsd:check-todos”）

**阻碍因素/担忧：**来自“下一阶段准备情况”部分
- 影响今后工作的问题
- 带有起始阶段的前缀
- 寻址时清零

### 会话连续性
启用即时恢复：
- 上次会议是什么时候
- 最后完成了什么
- 是否有 .continue-here 文件可以从中恢复

</sections>

<size_constraint>

将 STATE.md 保持在 100 行以下。

这是摘要，而不是档案。如果累积的上下文变得太大：
- 仅保留 3-5 个最近的决定摘要（完整登录 PROJECT.md）
- 仅保留活动的阻止程序，删除已解决的阻止程序

目标是“读一次，就知道我们在哪里”——如果太长，那就失败了。

</size_constraint>