---
name: gsd:remove-phase
description: 从路线图中移除未来阶段，并重编号后续阶段
argument-hint: <phase-number>
allowed-tools:
  - Read
  - Write
  - Bash
  - Glob
---
<objective>
从路线图中移除一个尚未开始的未来阶段，并为后续阶段重新编号，以保持序列整洁线性。

目的：干净地移除你决定不再执行的工作，而不是用取消/延期标记污染上下文。
输出：删除该阶段，后续阶段全部重新编号，并通过 git 提交保留历史记录。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/remove-phase.md
</execution_context>

<context>
阶段：`$ARGUMENTS`

Roadmap and state are resolved in-workflow via `init phase-op` and targeted reads.
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/remove-phase.md` 中的 `remove-phase` 工作流。
保留全部校验关卡（未来阶段检查、工作状态检查）、重编号逻辑与提交步骤。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
