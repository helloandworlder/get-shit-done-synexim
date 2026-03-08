---
name: gsd:patch-agents
description: Inject or refresh the GSD Synexim block in AGENTS.md
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
---
<objective>
Patch the current project's `AGENTS.md` so future agents proactively use GSD Synexim.

Preserve existing project instructions outside the managed block.
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/patch-agents.md
@~/.claude/get-shit-done/templates/project-agents.md
</execution_context>

<process>
Execute the patch-agents workflow from @~/.claude/get-shit-done/workflows/patch-agents.md end-to-end.
</process>
