# UAT 模板

`.planning/phases/XX-name/{phase_num}-UAT.md` 模板 — 持久 UAT 会话跟踪。

---

## 文件模板

```markdown
---
status: testing | complete | diagnosed
phase: XX-name
source: [list of SUMMARY.md files tested]
started: [ISO timestamp]
updated: [ISO timestamp]
---

## Current Test
<!-- OVERWRITE each test - shows where we are -->

number: [N]
name: [test name]
expected: |
  [what user should observe]
awaiting: user response

## Tests

### 1. [Test Name]
expected: [observable behavior - what user should see]
result: [pending]

### 2. [Test Name]
expected: [observable behavior]
result: pass

### 3. [Test Name]
expected: [observable behavior]
result: issue
reported: "[verbatim user response]"
severity: major

### 4. [Test Name]
expected: [observable behavior]
result: skipped
reason: [why skipped]

...

## Summary

total: [N]
passed: [N]
issues: [N]
pending: [N]
skipped: [N]

## Gaps

<!-- YAML format for plan-phase --gaps consumption -->
- truth: "[expected behavior from test]"
  status: failed
  reason: "User reported: [verbatim response]"
  severity: blocker | major | minor | cosmetic
  test: [N]
  root_cause: ""     # Filled by diagnosis
  artifacts: []      # Filled by diagnosis
  missing: []        # Filled by diagnosis
  debug_session: ""  # Filled by diagnosis
```

---

<section_rules>

**前线：**
- `status`：覆盖 - “测试”或“完成”
- `phase`：不可变 - 创建时设置
- `source`：不可变 - 正在测试摘要文件
- `started`：不可变 - 创建时设置
- `updated`：覆盖 - 每次更改都会更新

**当前测试：**
- 在每次测试转换时完全覆盖
- 显示哪个测试处于活动状态以及正在等待什么
- 完成后：“[testing complete]”

**测试：**
- 每个测试：当用户响应时覆盖结果字段
- `result` 值：[pending]、通过、发出、跳过
- 如果出现问题：添加 `reported`（逐字）和 `severity`（推断）
- 如果跳过：添加 `reason`（如果提供）

**总结：**
- 每次响应后覆盖计数
- 曲目：总计、通过、问题、待定、跳过

**差距：**
- 仅在发现问题时追加（YAML 格式）
- 诊断后：填写`root_cause`、`artifacts`、`missing`、`debug_session`
- 此部分直接输入 /gsd:plan-phase --gaps

</section_rules>

<diagnosis_lifecycle>

**测试完成后（状态：完成），如果存在差距：**

1. 用户运行诊断（从验证工作报价或手动）
2. 诊断问题工作流程产生并行调试代理
3. 每个代理调查一个差距，返回根本原因
4. UAT.md 间隙部分更新了诊断：
   - 每个缺口都被 `root_cause`、`artifacts`、`missing`、`debug_session` 填充
5.状态→“确诊”
6. 为/gsd:plan-phase做好准备——根本原因的差距

**诊断后：**
```yaml
## Gaps

- truth: "Comment appears immediately after submission"
  status: failed
  reason: "User reported: works but doesn't show until I refresh the page"
  severity: major
  test: 2
  root_cause: "useEffect in CommentList.tsx missing commentCount dependency"
  artifacts:
    - path: "src/components/CommentList.tsx"
      issue: "useEffect missing dependency"
  missing:
    - "Add commentCount to useEffect dependency array"
  debug_session: ".planning/debug/comment-not-refreshing.md"
```

</diagnosis_lifecycle>

<lifecycle>

**创建：**当/gsd:verify-work开始新会话时
- 从 SUMMARY.md 文件中提取测试
- 将状态设置为“测试”
- 当前要测试 1 的测试点
- 所有测试都有结果：[pending]

**测试期间：**
- 当前测试部分的当前测试
- 用户回复通过确认或问题描述
- 更新测试结果（通过/发出/跳过）
- 更新摘要计数
- 如果出现问题：附加到差距部分（YAML 格式），推断严重性
- 将当前测试移至下一个待处理测试

**完成后：**
- 状态→“完成”
- 当前测试→“[testing complete]”
- 提交文件
- 提出总结以及后续步骤

**/clear 之后恢复：**
1. Read前置→了解相位和状态
2. Read电流测试→知道我们在哪里
3. 找到第一个 [pending] 结果 → 从那里继续
4. 总结显示迄今为止的进展

</lifecycle>

<severity_guide>

严重性是根据用户的自然语言推断出来的，从未被询问过。

|用户描述 |推断|
|----------------|--------------------|
|崩溃、错误、异常、完全失败、无法使用 |拦截器|
|不起作用、没有任何反应、行为错误、失踪 |专业|
|可以工作，但是......，缓慢，奇怪，小问题|次要|
|颜色、字体、间距、对齐、视觉、外观 |化妆品 |

默认值：**major**（安全默认值，如果错误用户可以澄清）

</severity_guide>

<good_example>
```markdown
---
status: diagnosed
phase: 04-comments
source: 04-01-SUMMARY.md, 04-02-SUMMARY.md
started: 2025-01-15T10:30:00Z
updated: 2025-01-15T10:45:00Z
---

## Current Test

[testing complete]

## Tests

### 1. View Comments on Post
expected: Comments section expands, shows count and comment list
result: pass

### 2. Create Top-Level Comment
expected: Submit comment via rich text editor, appears in list with author info
result: issue
reported: "works but doesn't show until I refresh the page"
severity: major

### 3. Reply to a Comment
expected: Click Reply, inline composer appears, submit shows nested reply
result: pass

### 4. Visual Nesting
expected: 3+ level thread shows indentation, left borders, caps at reasonable depth
result: pass

### 5. Delete Own Comment
expected: Click delete on own comment, removed or shows [deleted] if has replies
result: pass

### 6. Comment Count
expected: Post shows accurate count, increments when adding comment
result: pass

## Summary

total: 6
passed: 5
issues: 1
pending: 0
skipped: 0

## Gaps

- truth: "Comment appears immediately after submission in list"
  status: failed
  reason: "User reported: works but doesn't show until I refresh the page"
  severity: major
  test: 2
  root_cause: "useEffect in CommentList.tsx missing commentCount dependency"
  artifacts:
    - path: "src/components/CommentList.tsx"
      issue: "useEffect missing dependency"
  missing:
    - "Add commentCount to useEffect dependency array"
  debug_session: ".planning/debug/comment-not-refreshing.md"
```
</good_example>