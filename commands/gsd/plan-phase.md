---
name: gsd:plan-phase
description: 创建带校验循环的详细阶段计划（`PLAN.md`）
argument-hint: "[phase] [--auto] [--research] [--skip-research] [--gaps] [--skip-verify] [--prd <file>]"
agent: gsd-planner
allowed-tools:
  - Read
  - Write
  - Bash
  - Glob
  - Grep
  - Task
  - WebFetch
  - mcp__context7__*
---
<objective>
为路线图阶段生成可执行的阶段提示（`PLAN.md` 文件），并内置研究与验证闭环。

**默认流程：** 研究（如有需要）→ 规划 → 校验 → 完成

**编排器职责：** 解析参数、验证阶段、研究领域（除非跳过）、拉起 `gsd-planner`、使用 `gsd-plan-checker` 校验，并在通过或达到最大迭代次数前持续迭代，最后展示结果。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/plan-phase.md
@~/.claude/get-shit-done/references/ui-brand.md
</execution_context>

<context>
阶段编号：`$ARGUMENTS`（可选；若省略则自动检测下一个未规划阶段）

**标志：**
- `--research` — 即使 `RESEARCH.md` 已存在，也强制重新研究
- `--skip-research` — 跳过研究，直接进入规划
- `--gaps` — 补缺模式（读取 `VERIFICATION.md`，跳过研究）
- `--skip-verify` — 跳过校验循环
- `--prd <file>` — 使用 PRD/验收标准文件替代 `discuss-phase`，并自动把需求解析到 `CONTEXT.md` 中，完全跳过 `discuss-phase`。

在执行任何目录查找前，先在步骤 2 规范化阶段输入。
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/plan-phase.md` 中的 `plan-phase` 工作流。
保留全部工作流关卡（校验、研究、规划、校验循环、路由）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
