<purpose>
Patch or create `AGENTS.md` so the current repository proactively uses GSD Synexim.
</purpose>

<required_reading>
Read all files referenced by the invoking prompt's execution_context before starting.
</required_reading>

<process>

## 1. Read current files

Read `AGENTS.md` if it exists.

Read `@~/.claude/get-shit-done/templates/project-agents.md`.

## 2. Manage a stable block

Use this exact marker pair inside `AGENTS.md`:

```text
<!-- GSD-SYNEXIM:START -->
<!-- GSD-SYNEXIM:END -->
```

Rules:
- If `AGENTS.md` is missing, create it from the template.
- If the marker block already exists, replace only the content inside the block.
- If `AGENTS.md` exists without the marker block, append the managed block to the end of the file with one blank line separator.
- Do not rewrite unrelated user-authored instructions.

## 3. Validate content

Ensure the managed block includes all of these requirements:
- Chinese-first output and document generation
- adaptive scale rules for micro / standard / large work
- proactive GSD triggers for documentation, planning, execution, and progress updates
- progress-card output after docs or implementation work
- front-end prototype gate using Gemini AI Studio before planning front-end phases
- instruction to launch a local front-end demo when prototype coverage is missing

## 4. Report

Return a concise Chinese card that names:
- whether `AGENTS.md` was created or patched
- which modules/rules were injected
- what the next recommended GSD command is

</process>
