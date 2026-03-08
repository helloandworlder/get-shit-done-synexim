---
name: gsd:add-tests
description: Generate tests for a completed phase based on UAT criteria and implementation
argument-hint: "<phase> [additional instructions]"
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - Task
  - AskUserQuestion
argument-instructions: |
  Parse the argument as a phase number (integer, decimal, or letter-suffix), plus optional free-text instructions.
  Example: /gsd:add-tests 12
  Example: /gsd:add-tests 12 focus on edge cases in the pricing module
---
<objective>
基于已完成阶段的 `SUMMARY.md`、`CONTEXT.md` 与 `VERIFICATION.md` 作为规格，为其生成单元测试和 E2E 测试。

分析实现文件，将其归类为 TDD（单元）、E2E（浏览器）或 Skip，先向用户展示测试计划并获得确认，再按 RED-GREEN 约定生成测试。

输出：测试文件会以提交信息 `test(phase-{N}): add unit and E2E tests from add-tests command` 提交。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/add-tests.md
</execution_context>

<context>
阶段：`$ARGUMENTS`

@.planning/STATE.md
@.planning/ROADMAP.md
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/add-tests.md` 中的 `add-tests` 工作流。
保留全部工作流关卡（分类确认、测试计划确认、RED-GREEN 验证、缺口报告）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
