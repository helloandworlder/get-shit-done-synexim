---
name: gsd:check-todos
description: 列出待处理 todo 并选择其中一项开始处理
argument-hint: [area filter]
allowed-tools:
  - Read
  - Write
  - Bash
  - AskUserQuestion
---

<objective>
列出所有待处理 todo，让用户选择其一，加载完整上下文，并路由到合适的下一步动作。

转交给 `check-todos` 工作流处理，负责：
- Todo counting and listing with area filtering
- Interactive selection with full context loading
- Roadmap correlation checking
- Action routing (work now, add to phase, brainstorm, create phase)
- STATE.md updates and git commits
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/check-todos.md
</execution_context>

<context>
参数：`$ARGUMENTS`（可选的领域过滤）

todo 状态与路线图关联会在工作流内部通过 `init todos` 和定向读取加载。
</context>

<process>
**按照** `@~/.claude/get-shit-done/workflows/check-todos.md` **中的 `check-todos` 工作流执行。**

The workflow handles all logic including:
1. Todo existence checking
2. Area filtering
3. Interactive listing and selection
4. Full context loading with file summaries
5. Roadmap correlation checking
6. Action offering and execution
7. STATE.md updates
8. Git commits

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
