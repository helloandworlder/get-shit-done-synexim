---
name: gsd:list-phase-assumptions
description: 在规划前展示 Claude 对阶段方案的假设
argument-hint: "[phase]"
allowed-tools:
  - Read
  - Bash
  - Grep
  - Glob
---

<objective>
分析某个阶段，并展示 Claude 对技术路线、实现顺序、范围边界、风险区域与依赖关系的假设。

目的：让用户在正式规划前看到 Claude 的预设判断，从而在假设错误时尽早校正方向。
输出：仅对话式输出（不创建文件），并以“你怎么看？”作为结尾提示。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/list-phase-assumptions.md
</execution_context>

<context>
阶段编号：`$ARGUMENTS`（必填）

项目状态与路线图会在工作流内部通过定向读取加载。
</context>

<process>
1. Validate phase number argument (error if missing or invalid)
2. Check if phase exists in roadmap
3. Follow list-phase-assumptions.md workflow:
   - Analyze roadmap description
   - Surface assumptions about: technical approach, implementation order, scope, risks, dependencies
   - Present assumptions clearly
   - Prompt "What do you think?"
4. 收集反馈并给出下一步建议

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>

<success_criteria>

- Phase validated against roadmap
- Assumptions surfaced across five areas
- User prompted for feedback
- User knows next steps (discuss context, plan phase, or correct assumptions)
  </success_criteria>
