---
name: gsd:settings
description: 配置 GSD 工作流开关与模型档位
allowed-tools:
  - Read
  - Write
  - Bash
  - AskUserQuestion
---

<objective>
通过多轮提问交互式配置 GSD 工作流代理与模型档位。

转交给 `settings` 工作流处理，负责：
- Config existence ensuring
- Current settings reading and parsing
- Interactive 5-question prompt (model, research, plan_check, verifier, branching)
- Config merging and writing
- Confirmation display with quick command references
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/settings.md
</execution_context>

<process>
**按照** `@~/.claude/get-shit-done/workflows/settings.md` **中的 `settings` 工作流执行。**

The workflow handles all logic including:
1. Config file creation with defaults if missing
2. Current config reading
3. Interactive settings presentation with pre-selection
4. Answer parsing and config merging
5. File writing
6. Confirmation display

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
