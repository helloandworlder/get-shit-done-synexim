---
name: gsd:validate-phase
description: 对已完成阶段补做 Nyquist 验证审计并填补缺口
argument-hint: "[phase number]"
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - Task
  - AskUserQuestion
---
<objective>
审计已完成阶段的 Nyquist 验证覆盖情况。共有三种状态：
- (A) 已存在 `VALIDATION.md` —— 审计并补齐缺口
- (B) 没有 `VALIDATION.md`，但存在 `SUMMARY.md` —— 从产物中重建
- (C) 阶段尚未执行 —— 给出引导后退出

输出：更新后的 `VALIDATION.md` 与生成的测试文件。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/validate-phase.md
</execution_context>

<context>
阶段：`$ARGUMENTS` — optional, defaults to last completed phase.
</context>

<process>
执行 `@~/.claude/get-shit-done/workflows/validate-phase.md`。
保留全部工作流关卡。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
