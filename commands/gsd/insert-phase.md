---
name: gsd:insert-phase
description: 在现有阶段之间插入紧急小数阶段（如 72.1）
argument-hint: <after> <description>
allowed-tools:
  - Read
  - Write
  - Bash
---

<objective>
为里程碑执行过程中发现的紧急工作插入一个小数阶段，并要求它在现有整数阶段之间完成。

使用小数编号（如 72.1、72.2）在保留既有逻辑顺序的同时容纳紧急插入项。

目的：在不整体重排路线图编号的情况下处理执行中发现的紧急工作。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/insert-phase.md
</execution_context>

<context>
参数：`$ARGUMENTS`（格式：`<after-phase-number> <description>`）

路线图与状态会在工作流内部通过 `init phase-op` 和定向工具调用解析。
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/insert-phase.md` 中的 `insert-phase` 工作流。
保留全部校验关卡（参数解析、阶段验证、小数编号计算、路线图更新）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
