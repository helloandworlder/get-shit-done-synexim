# 调试模板

`.planning/debug/[slug].md` 模板 — 主动调试会话跟踪。

---

## 文件模板

```markdown
---
status: gathering | investigating | fixing | verifying | awaiting_human_verify | resolved
trigger: "[verbatim user input]"
created: [ISO timestamp]
updated: [ISO timestamp]
---

## Current Focus
<!-- OVERWRITE on each update - always reflects NOW -->

hypothesis: [current theory being tested]
test: [how testing it]
expecting: [what result means if true/false]
next_action: [immediate next step]

## Symptoms
<!-- Written during gathering, then immutable -->

expected: [what should happen]
actual: [what actually happens]
errors: [error messages if any]
reproduction: [how to trigger]
started: [when it broke / always broken]

## Eliminated
<!-- APPEND only - prevents re-investigating after /clear -->

- hypothesis: [theory that was wrong]
  evidence: [what disproved it]
  timestamp: [when eliminated]

## Evidence
<!-- APPEND only - facts discovered during investigation -->

- timestamp: [when found]
  checked: [what was examined]
  found: [what was observed]
  implication: [what this means]

## Resolution
<!-- OVERWRITE as understanding evolves -->

root_cause: [empty until found]
fix: [empty until applied]
verification: [empty until verified]
files_changed: []
```

---

<section_rules>

**Frontmatter（状态、触发器、时间戳）：**
- `status`：覆盖 - 反映当前阶段
- `trigger`：IMMUTABLE - 逐字用户输入，永远不会改变
- `created`：不可变 - 设置一次
- `updated`：覆盖 - 每次更改都会更新

**当前焦点：**
- 每次更新时完全覆盖
- 始终反映 Claude 现在正在做什么
- 如果 Claude 在 /clear 之后读取此内容，它确切地知道从哪里恢复
- 字段：假设、测试、期望、next_action

**症状：**
- 在初始收集阶段编写
- 收集完成后不可变
- 我们正在尝试解决的问题的参考点
- 字段：预期、实际、错误、复制、开始

**淘汰：**
- 仅附加 - 绝不删除条目
- 防止在上下文重置后重新调查死胡同
- 每个条目：假设、反驳它的证据、时间戳
- 对于跨越/清晰界限的效率至关重要

**证据：**
- 仅附加 - 绝不删除条目
- 调查中发现的事实
- 每个条目：时间戳、检查内容、发现内容、含义
- 建立根本原因的案例

**分辨率：**
- 随着理解的发展而覆盖
- 在尝试修复时可能会多次更新
- 最终状态显示已确认的根本原因和已验证的修复
- 字段：root_cause、修复、验证、files_changed

</section_rules>

<lifecycle>

**创建：**当/gsd:debug被调用时立即
- 根据用户输入创建带有触发器的文件
- 将状态设置为“正在收集”
- 当前焦点：next_action =“收集症状”
- 症状：空虚，待填充

**症状收集期间：**
- 当用户回答问题时更新症状部分
- 用每个问题更新当前焦点
- 完成后：状态→“调查”

**调查期间：**
- 用每个假设覆盖当前焦点
- 附加到每项发现的证据
- 当假设被推翻时附加到消除
- 更新 frontmatter 中的时间戳

**修复期间：**
- 状态→“修复”
- 确认后更新Resolution.root_cause
- 应用时更新Resolution.fix
- 更新Resolution.files_changed

**验证期间：**
- 状态→“正在验证”
- 更新 Resolution.verification 结果
- 如果验证失败：状态→“正在调查”，重试

**自我验证通过后：**
-状态->“等待人类验证”
- 在检查点请求明确的用户确认
- 请勿将文件移至已解决的位置

**关于分辨率：**
- 状态→“已解决”
- 将文件移至.planning/debug/resolved/（仅在用户确认修复后）

</lifecycle>

<resume_behavior>

当Claude在/clear之后读取该文件时：

1.解析frontmatter→了解状态
2. Read 当前焦点 → 准确了解发生了什么
3. Read 已消除 → 知道什么不应该重试
4. Read 证据 → 了解学到了什么
5. 从next_action继续

文件是调试大脑。 Claude应该能够从任何中断点完美恢复。

</resume_behavior>

<size_constraint>

保持调试文件集中：
- 证据条目：每行1-2行，仅是事实
- 消除：简要 - 假设 + 失败的原因
- 无叙事散文 - 仅结构化数据如果证据变得非常大（10 多个条目），请考虑您是否在原地踏步。检查“已消除”以确保您不会重蹈覆辙。

</size_constraint>