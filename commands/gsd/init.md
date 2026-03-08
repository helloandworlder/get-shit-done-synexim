---
name: gsd:init
description: Bootstrap GSD Synexim into the current project
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
---
<objective>
Initialize GSD Synexim in the current repository.

This command should:
- ensure `.planning/config.json` exists
- create or patch `AGENTS.md` with Synexim's Chinese-first GSD rules
- prepare the repository so agents proactively use GSD on future work
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/init.md
@~/.claude/get-shit-done/templates/project-agents.md
</execution_context>

<process>
Execute the init workflow from @~/.claude/get-shit-done/workflows/init.md end-to-end.
</process>
