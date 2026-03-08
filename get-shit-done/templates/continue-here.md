# 继续-此处模板

复制并填充 `.planning/phases/XX-name/.continue-here.md` 的结构：

```yaml
---
phase: XX-name
task: 3
total_tasks: 7
status: in_progress
last_updated: 2025-01-15T14:30:00Z
---
```

```markdown
<current_state>
[Where exactly are we? What's the immediate context?]
</current_state>

<completed_work>
[What got done this session - be specific]

- Task 1: [name] - Done
- Task 2: [name] - Done
- Task 3: [name] - In progress, [what's done on it]
</completed_work>

<remaining_work>
[What's left in this phase]

- Task 3: [name] - [what's left to do]
- Task 4: [name] - Not started
- Task 5: [name] - Not started
</remaining_work>

<decisions_made>
[Key decisions and why - so next session doesn't re-debate]

- Decided to use [X] because [reason]
- Chose [approach] over [alternative] because [reason]
</decisions_made>

<blockers>
[Anything stuck or waiting on external factors]

- [Blocker 1]: [status/workaround]
</blockers>

<context>
[Mental state, "vibe", anything that helps resume smoothly]

[What were you thinking about? What was the plan?
This is the "pick up exactly where you left off" context.]
</context>

<next_action>
[The very first thing to do when resuming]

Start with: [specific action]
</next_action>
```

<yaml_fields>
所需的 YAML frontmatter：

- `phase`：目录名称（e.g.、`02-authentication`）
- `task`：当前任务编号
- `total_tasks`：阶段中有多少任务
- `status`：`in_progress`、`blocked`、`almost_done`
- `last_updated`：ISO时间戳
</yaml_fields>

<guidelines>
- 足够具体，以便新的 Claude 实例立即理解
- 包括为什么做出决定，而不仅仅是做什么
- `<next_action>` 应该无需阅读任何其他内容即可操作
- 该文件在恢复后被删除 - 它不是永久存储
</guidelines>