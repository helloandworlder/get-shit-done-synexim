# Planner 子代理提示模板

用于生成 gsd-planner 代理的模板。该代理包含所有规划专业知识 - 此模板仅提供规划上下文。

---

## 模板

```markdown
<planning_context>

**Phase:** {phase_number}
**Mode:** {standard | gap_closure}

**Project State:**
@.planning/STATE.md

**Roadmap:**
@.planning/ROADMAP.md

**Model policy:**
- Planning/roadmapping must use OpenAI GPT-5.4 with `xhigh` or `high` effort
- Coding/execution later uses OpenAI GPT-5.4 with `high` effort
- Front-end design is blocked during project initialization; only prototype alignment is allowed

**Requirements (if exists):**
@.planning/REQUIREMENTS.md

**Phase Context (if exists):**
@.planning/phases/{phase_dir}/{phase_num}-CONTEXT.md

**Research (if exists):**
@.planning/phases/{phase_dir}/{phase_num}-RESEARCH.md

**Gap Closure (if --gaps mode):**
@.planning/phases/{phase_dir}/{phase_num}-VERIFICATION.md
@.planning/phases/{phase_dir}/{phase_num}-UAT.md

</planning_context>

<downstream_consumer>
Output consumed by /gsd:execute-phase
Plans must be executable prompts with:
- Frontmatter (wave, depends_on, files_modified, autonomous)
- Tasks in XML format
- Verification criteria
- must_haves for goal-backward verification
</downstream_consumer>

<quality_gate>
Before returning PLANNING COMPLETE:
- [ ] PLAN.md files created in phase directory
- [ ] Each plan has valid frontmatter
- [ ] Tasks are specific and actionable
- [ ] Dependencies correctly identified
- [ ] Waves assigned for parallel execution
- [ ] must_haves derived from phase goal
</quality_gate>
```

---

## 占位符

|占位符|来源|示例|
|-------------|--------|---------|
| `{phase_number}` |来自路线图/论点| `5` 或 `2.1` |
| `{phase_dir}` |阶段目录名称 | `05-user-profiles` |
| `{phase}` | 相出口 | `05` |
| `{standard \| gap_closure}` |模式标志| `standard` |

---

## 用法

**来自/gsd:plan-phase（标准模式）：**
```python
Task(
  prompt=filled_template,
  subagent_type="gsd-planner",
  description="Plan Phase {phase}"
)
```

**来自/gsd:plan-phase --gaps（间隙模式）：**
```python
Task(
  prompt=filled_template,  # with mode: gap_closure
  subagent_type="gsd-planner",
  description="Plan gaps for Phase {phase}"
)
```

---

## 继续

对于检查点，使用以下命令生成新代理：

```markdown
<objective>
Continue planning for Phase {phase_number}: {phase_name}
</objective>

<prior_state>
Phase directory: @.planning/phases/{phase_dir}/
Existing plans: @.planning/phases/{phase_dir}/*-PLAN.md
</prior_state>

<checkpoint_response>
**Type:** {checkpoint_type}
**Response:** {user_response}
</checkpoint_response>

<mode>
Continue: {standard | gap_closure}
</mode>
```

---

**注意：** 规划方法、任务拆分、依赖分析、波次分配、TDD 检测和目标后推规则都已内置在 `gsd-planner` 代理中。该模板只负责传递上下文。
