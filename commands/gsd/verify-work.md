---
name: gsd:verify-work
description: 通过对话式 UAT 验证已构建功能
argument-hint: "[phase number, e.g., '4']"
allowed-tools:
  - Read
  - Bash
  - Glob
  - Grep
  - Edit
  - Write
  - Task
---
<objective>
通过带持久状态的对话式测试来验证已构建功能。

目的：从用户视角确认 Claude 构建的内容是否真的可用。一次只测一个点，使用纯文本回复，不做审问式互动。发现问题时，会自动诊断、规划修复并为执行做好准备。

输出：使用 `{phase_num}-UAT.md` 跟踪全部测试结果。若发现问题：会产出已诊断缺口与可直接供 `/gsd:execute-phase` 使用的修复计划。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/verify-work.md
@~/.claude/get-shit-done/templates/UAT.md
</execution_context>

<context>
阶段：`$ARGUMENTS` (optional)
- 若提供：测试指定阶段（例如 `4`）
- 若未提供：先检查是否有活动会话，或继续询问阶段

上下文文件会在工作流内部通过 `init verify-work` 解析，并通过 `<files_to_read>` 区块传递。
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/verify-work.md` 中的 `verify-work` 工作流。
保留全部工作流关卡（会话管理、测试展示、诊断、修复规划、路由）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
