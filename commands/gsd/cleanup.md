---
name: gsd:cleanup
description: 归档已完成里程碑累计留下的阶段目录
---
<objective>
将已完成里程碑的阶段目录归档到 `.planning/milestones/v{X.Y}-phases/`。

适用于 `.planning/phases/` 中已堆积多个历史里程碑阶段目录的情况。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/cleanup.md
</execution_context>

<process>
按照 `@~/.claude/get-shit-done/workflows/cleanup.md` 中的 `cleanup` 工作流执行。
识别已完成里程碑，先展示 dry-run 摘要，再在确认后执行归档。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
