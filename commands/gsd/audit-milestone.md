---
name: gsd:audit-milestone
description: 在归档前审计里程碑是否符合原始目标
argument-hint: "[version]"
allowed-tools:
  - Read
  - Glob
  - Grep
  - Bash
  - Task
  - Write
---
<objective>
验证里程碑是否真正达到完成定义，检查需求覆盖、跨阶段集成与端到端流程。

**该命令本身就是编排器。** 它会读取已有的 `VERIFICATION.md` 文件（这些阶段已在 `execute-phase` 时完成验证），汇总技术债与延期缺口，再启动集成检查器验证跨阶段串联。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/audit-milestone.md
</execution_context>

<context>
版本：`$ARGUMENTS`（可选，默认当前里程碑）

核心规划文件会在工作流内部通过 `init milestone-op` 解析，并按需加载。

**Completed Work:**
Glob: .planning/phases/*/*-SUMMARY.md
Glob: .planning/phases/*/*-VERIFICATION.md
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/audit-milestone.md` 中的 `audit-milestone` 工作流。
保留全部工作流关卡（范围判定、验证读取、集成检查、需求覆盖、路由）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
