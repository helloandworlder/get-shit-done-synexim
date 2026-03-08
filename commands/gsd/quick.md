---
name: gsd:quick
description: 在保留 GSD 保障的前提下执行快速任务，并跳过可选代理
argument-hint: "[--full] [--discuss]"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Task
  - AskUserQuestion
---
<objective>
在保留 GSD 保障（原子提交、`STATE.md` 跟踪）的前提下执行小型临时任务。

Quick 模式沿用同一套系统，但路径更短：
- Spawns gsd-planner (quick mode) + gsd-executor(s)
- Quick tasks live in `.planning/quick/` separate from planned phases
- Updates STATE.md "Quick Tasks Completed" table (NOT ROADMAP.md)

**默认：** 跳过研究、讨论、计划检查器和验证器。适合你已经清楚知道该做什么的场景。

**`--discuss` 标志：** 在规划前增加轻量讨论阶段，暴露假设、澄清灰区，并把决策记录到 `CONTEXT.md`。适合任务存在值得提前消解的歧义时使用。

**`--full` 标志：** 开启计划检查（最多 2 次迭代）与执行后验证。适合想要质量保障、但又不想走完整里程碑流程时使用。

标志可以组合：`--discuss --full` 表示讨论 + 计划检查 + 验证。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/quick.md
</execution_context>

<context>
$ARGUMENTS

上下文文件会在工作流内部通过 `init quick` 解析，并通过 `<files_to_read>` 区块传递。
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/quick.md` 中的 `quick` 工作流。
保留全部工作流关卡（校验、任务描述、规划、执行、状态更新、提交）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
