---
name: gsd:pause-work
description: 在阶段中途暂停工作时创建上下文交接
allowed-tools:
  - Read
  - Write
  - Bash
---

<objective>
创建 `.continue-here.md` 交接文件，以在跨会话时保留完整工作状态。

转交给 `pause-work` 工作流处理，负责：
- Current phase detection from recent files
- Complete state gathering (position, completed work, remaining work, decisions, blockers)
- Handoff file creation with all context sections
- Git commit as WIP
- Resume instructions
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/pause-work.md
</execution_context>

<context>
状态与阶段进度会在工作流内部通过定向读取收集。
</context>

<process>
**按照** `@~/.claude/get-shit-done/workflows/pause-work.md` **中的 `pause-work` 工作流执行。**

The workflow handles all logic including:
1. Phase directory detection
2. State gathering with user clarifications
3. Handoff file writing with timestamp
4. Git commit
5. Confirmation with resume instructions

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
