---
name: gsd:patch-agents
description: 注入或刷新 `AGENTS.md` 中的 GSD Synexim 托管区块
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
---
<objective>
修补当前项目的 `AGENTS.md`，让后续代理主动使用 GSD Synexim。

保留托管区块之外现有的项目指令。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/patch-agents.md
@~/.claude/get-shit-done/templates/project-agents.md
</execution_context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/patch-agents.md` 中的 `patch-agents` 工作流。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
