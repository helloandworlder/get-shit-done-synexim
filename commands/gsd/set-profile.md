---
name: gsd:set-profile
description: 切换 GSD 代理模型档位（quality/balanced/budget）
argument-hint: <profile>
allowed-tools:
  - Read
  - Write
  - Bash
---

<objective>
切换 GSD 代理使用的模型配置档，控制 Synexim 模式下 `OpenAI GPT-5.4` 的使用策略：规划默认 `xhigh/high`，实现统一 `high`。

转交给 `set-profile` 工作流处理，负责：
- Argument validation (quality/balanced/budget)
- Config file creation if missing
- Profile update in config.json
- Confirmation with model table display
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/set-profile.md
</execution_context>

<process>
**按照** `@~/.claude/get-shit-done/workflows/set-profile.md` **中的 `set-profile` 工作流执行。**

The workflow handles all logic including:
1. Profile argument validation
2. Config file ensuring
3. Config reading and updating
4. Model table generation from MODEL_PROFILES
5. Confirmation display

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
