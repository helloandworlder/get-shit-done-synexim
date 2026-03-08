---
name: gsd:health
description: 诊断规划目录健康状况，并可选修复问题
argument-hint: [--repair]
allowed-tools:
  - Read
  - Bash
  - Write
  - AskUserQuestion
---
<objective>
校验 `.planning/` 目录完整性，并报告可执行的问题项；检查缺失文件、无效配置、状态不一致以及孤立计划。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/health.md
</execution_context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/health.md` 中的 `health` 工作流。
从参数中解析 `--repair` 标志并传递给工作流。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
