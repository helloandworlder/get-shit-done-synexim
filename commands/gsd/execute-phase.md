---
name: gsd:execute-phase
description: 在单个阶段内按波次并行执行全部计划
argument-hint: "<phase-number> [--gaps-only]"
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Task
  - TodoWrite
  - AskUserQuestion
---
<objective>
通过基于波次的并行执行来完成某个阶段中的全部计划。

编排器保持轻量：发现计划、分析依赖、按波次分组、拉起子代理并汇总结果。每个子代理都会加载完整的 `execute-plan` 上下文并独立处理自己的计划。

上下文预算：编排器约占 15%，每个子代理使用全新上下文。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/execute-phase.md
@~/.claude/get-shit-done/references/ui-brand.md
</execution_context>

<context>
阶段：`$ARGUMENTS`

**标志：**
- `--gaps-only` — 仅执行补缺计划（frontmatter 中 `gap_closure: true` 的计划）。通常在 `verify-work` 生成修复计划后使用。

上下文文件会在工作流内部通过 `gsd-tools init execute-phase` 和每个子代理的 `<files_to_read>` 区块解析。
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/execute-phase.md` 中的 `execute-phase` 工作流。
保留全部工作流关卡（波次执行、检查点处理、验证、状态更新、路由）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
