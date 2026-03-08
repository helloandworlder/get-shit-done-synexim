---
name: gsd:help
description: 显示可用的 GSD 命令与使用说明
---
<objective>
显示完整的 GSD 命令参考。

只输出下方参考内容。不要额外加入：
- 与项目相关的分析
- Git 状态或文件上下文
- 下一步建议
- 参考内容以外的任何评论
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/help.md
</execution_context>

<process>
输出 `@~/.claude/get-shit-done/workflows/help.md` 中的完整 GSD 命令参考。
直接显示参考内容，不做额外补充或改写。
</process>
