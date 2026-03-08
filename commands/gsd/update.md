---
name: gsd:update
description: 将 GSD 更新到最新版本并显示更新日志
allowed-tools:
  - Bash
  - AskUserQuestion
---

<objective>
检查 GSD 更新；若有可用版本则安装，并展示变化内容。

转交给 `update` 工作流处理，负责：
- Version detection (local vs global installation)
- npm version checking
- Changelog fetching and display
- User confirmation with clean install warning
- Update execution and cache clearing
- Restart reminder
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/update.md
</execution_context>

<process>
**按照** `@~/.claude/get-shit-done/workflows/update.md` **中的 `update` 工作流执行。**

The workflow handles all logic including:
1. Installed version detection (local/global)
2. Latest version checking via npm
3. Version comparison
4. Changelog fetching and extraction
5. Clean install warning display
6. User confirmation
7. Update execution
8. Cache clearing

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
