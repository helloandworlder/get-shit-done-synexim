<purpose>
Bootstrap GSD Synexim into an existing or new repository by preparing `.planning/config.json` and `AGENTS.md`.
</purpose>

<required_reading>
Read all files referenced by the invoking prompt's execution_context before starting.
</required_reading>

<process>

## 1. Gather bootstrap context

Run:

```bash
node "$HOME/.claude/get-shit-done/bin/gsd-tools.cjs" config-ensure-section
INIT=$(node "$HOME/.claude/get-shit-done/bin/gsd-tools.cjs" init new-project)
if [[ "$INIT" == @file:* ]]; then INIT=$(cat "${INIT#@file:}"); fi
```

Parse JSON for: `language`, `project_scale`, `recommended_scale`, `scale_reason`, `recommended_workflow`, `frontend_prototype_required`, `frontend_prototype_tool`, `code_file_count`, `code_directory_count`, `has_git`, `is_brownfield`.

## 2. Prepare AGENTS.md

Read `@~/.claude/get-shit-done/templates/project-agents.md`.

If `AGENTS.md` does not exist:
- Write a new root-level `AGENTS.md`
- Keep the template content intact

If `AGENTS.md` already exists:
- Apply the same merge logic as `/gsd:patch-agents`
- Preserve all user-authored content outside the managed block

## 3. Explain adaptive defaults in the file

Ensure the managed block communicates:
- default language is Chinese (`zh-CN`)
- scale is adaptive, with current recommendation set to `{recommended_scale}`
- implementation requests should move to code after at most one lightweight planning step
- front-end work must request a Gemini AI Studio prototype before phase planning

## 4. Report with progress card

Output a Chinese progress card in this style:

```text
┌─ GSD Synexim 初始化 ───────────────────────┐
│ 文档: AGENTS.md / .planning/config.json  │
│ 模块: governance / planning / frontend   │
│ 做了什么: 注入中文化、规模自适应规则       │
│ 为什么: 让 Agent 更主动地使用 GSD         │
│ 下一步: 运行 /gsd:new-project 或 /gsd:quick │
│ 推荐规模: {recommended_scale}            │
└──────────────────────────────────────────┘
```

Mention `code_file_count`, `code_directory_count`, and `recommended_workflow` in one short sentence after the card.

</process>
