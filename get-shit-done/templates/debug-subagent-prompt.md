# 调试子代理提示模板

用于生成 gsd 调试器代理的模板。该代理包含所有调试专业知识 - 该模板仅提供问题上下文。

---

## 模板

```markdown
<objective>
Investigate issue: {issue_id}

**Summary:** {issue_summary}
</objective>

<symptoms>
expected: {expected}
actual: {actual}
errors: {errors}
reproduction: {reproduction}
timeline: {timeline}
</symptoms>

<mode>
symptoms_prefilled: {true_or_false}
goal: {find_root_cause_only | find_and_fix}
</mode>

<debug_file>
Create: .planning/debug/{slug}.md
</debug_file>
```

---

## 占位符

|占位符 |来源 |示例|
|-------------|--------|---------|
| `{issue_id}` |协调员分配 | `auth-screen-dark` |
| `{issue_summary}` |用户描述 | `Auth screen is too dark` |
| `{expected}` |从症状来看| `See logo clearly` |
| `{actual}` |从症状来看| `Screen is dark` |
| `{errors}` |从症状来看| `None in console` |
| `{reproduction}` |从症状来看| `Open /auth page` |
| `{timeline}` |从症状来看| `After recent deploy` |
| `{goal}` |编排器套装 | `find_and_fix` |
| `{slug}` |生成 | `auth-screen-dark` |

---

## 用法

**来自/gsd:debug:**
```python
Task(
  prompt=filled_template,
  subagent_type="gsd-debugger",
  description="Debug {slug}"
)
```

**来自诊断问题 (UAT)：**
```python
Task(prompt=template, subagent_type="gsd-debugger", description="Debug UAT-001")
```

---

## 继续

对于检查点，使用以下命令生成新代理：

```markdown
<objective>
Continue debugging {slug}. Evidence is in the debug file.
</objective>

<prior_state>
Debug file: @.planning/debug/{slug}.md
</prior_state>

<checkpoint_response>
**Type:** {checkpoint_type}
**Response:** {user_response}
</checkpoint_response>

<mode>
goal: {goal}
</mode>
```