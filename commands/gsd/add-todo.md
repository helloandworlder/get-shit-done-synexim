---
name: gsd:add-todo
description: 从当前对话上下文中捕获想法或任务并记为 todo
argument-hint: [optional description]
allowed-tools:
  - Read
  - Write
  - Bash
  - AskUserQuestion
---

<objective>
把 GSD 会话中出现的想法、任务或问题记录成结构化 todo，供后续处理。

转交给 `add-todo` 工作流处理，负责：
- Directory structure creation
- Content extraction from arguments or conversation
- Area inference from file paths
- Duplicate detection and resolution
- Todo file creation with frontmatter
- STATE.md updates
- Git commits
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/add-todo.md
</execution_context>

<context>
参数：`$ARGUMENTS`（可选的 todo 描述）

状态会在工作流内部通过 `init todos` 和定向读取解析。
</context>

<process>
**按照** `@~/.claude/get-shit-done/workflows/add-todo.md` **中的 `add-todo` 工作流执行。**

The workflow handles all logic including:
1. Directory ensuring
2. Existing area checking
3. Content extraction (arguments or conversation)
4. Area inference
5. Duplicate checking
6. File creation with slug generation
7. STATE.md updates
8. Git commits

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
