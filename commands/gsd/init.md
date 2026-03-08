---
name: gsd:init
description: 将 GSD Synexim 引导接入当前项目
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
---
<objective>
在当前仓库中初始化 GSD Synexim。

该命令应当：
- 确保 `.planning/config.json` 存在
- 创建或修补 `AGENTS.md`，写入 Synexim 的中文优先 GSD 规则
- 让仓库在后续工作中使代理主动采用 GSD
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/init.md
@~/.claude/get-shit-done/templates/project-agents.md
</execution_context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/init.md` 中的 `init` 工作流。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
