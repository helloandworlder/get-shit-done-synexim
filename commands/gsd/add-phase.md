---
name: gsd:add-phase
description: 在路线图中向当前里程碑末尾添加阶段
argument-hint: <description>
allowed-tools:
  - Read
  - Write
  - Bash
---

<objective>
在路线图中为当前里程碑末尾新增一个整数阶段。

转交给 `add-phase` 工作流处理，负责：
- Phase number calculation (next sequential integer)
- Directory creation with slug generation
- Roadmap structure updates
- STATE.md roadmap evolution tracking
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/add-phase.md
</execution_context>

<context>
Arguments: $ARGUMENTS (phase description)

路线图与状态会在工作流内部通过 `init phase-op` 和定向工具调用解析。
</context>

<process>
**按照** `@~/.claude/get-shit-done/workflows/add-phase.md` **中的 `add-phase` 工作流执行。**

The workflow handles all logic including:
1. Argument parsing and validation
2. Roadmap existence checking
3. Current milestone identification
4. Next phase number calculation (ignoring decimals)
5. Slug generation from description
6. Phase directory creation
7. Roadmap entry insertion
8. STATE.md updates

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
