# 阶段提示模板

> **注：** 规划方法见 `agents/gsd-planner.md`。
> 此模板定义代理生成的 PLAN.md 输出格式。

`.planning/phases/XX-name/{phase}-{plan}-PLAN.md` 模板 - 针对并行执行优化的可执行阶段计划。

- 面向用户的说明、决策标签、检查点文案和最终总结默认使用中文。
- 计划规模要自适应：`micro` 保持轻量，`standard` 使用正常 Phase/Plan 粒度，`large` 明确分波次和依赖。
- 如果计划包含检查点或阶段交付，请在执行结果中要求输出进度卡，说明已完成内容、原因、下一步和当前进度。
- 规划与 Phase 设计默认由 `OpenAI GPT-5.4` 完成；优先 `xhigh / Extreme High`，其次 `high`。进入代码实现后统一使用 `GPT-5.4 high`。
- 任何前端实现计划都必须先确认已存在完整且对齐需求的 MVP 原型；若原型与 `.planning` 或当前里程碑存在差异，先请求用户决定补全还是移除。
- 每个 Phase 都必须交付一个或多个完整可用功能，便于用户在阶段结束时实际启动项目并测试。

**命名：** 使用 `{phase}-{plan}-PLAN.md` 格式（e.g.、`01-02-PLAN.md` 用于阶段 1、计划 2）

---

## 文件模板

```markdown
---
phase: XX-name
plan: NN
type: execute
wave: N                     # Execution wave (1, 2, 3...). Pre-computed at plan time.
depends_on: []              # Plan IDs this plan requires (e.g., ["01-01"]).
files_modified: []          # Files this plan modifies.
autonomous: true            # false if plan has checkpoints requiring user interaction
requirements: []            # REQUIRED — Requirement IDs from ROADMAP this plan addresses. MUST NOT be empty.
user_setup: []              # Human-required setup Claude cannot automate (see below)

# Goal-backward verification (derived during planning, verified after execution)
must_haves:
  truths: []                # Observable behaviors that must be true for goal achievement
  artifacts: []             # Files that must exist with real implementation
  key_links: []             # Critical connections between artifacts
---

<objective>
[What this plan accomplishes]

Purpose: [Why this matters for the project]
Output: [What artifacts will be created]
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/execute-plan.md
@~/.claude/get-shit-done/templates/summary.md
[If plan contains checkpoint tasks (type="checkpoint:*"), add:]
@~/.claude/get-shit-done/references/checkpoints.md
</execution_context>

<context>
@.planning/PROJECT.md
@.planning/ROADMAP.md
@.planning/STATE.md

# Only reference prior plan SUMMARYs if genuinely needed:
# - This plan uses types/exports from prior plan
# - Prior plan made decision that affects this plan
# Do NOT reflexively chain: Plan 02 refs 01, Plan 03 refs 02...

[Relevant source files:]
@src/path/to/relevant.ts
</context>

<tasks>

<task type="auto">
  <name>Task 1: [Action-oriented name]</name>
  <files>path/to/file.ext, another/file.ext</files>
  <action>[Specific implementation - what to do, how to do it, what to avoid and WHY]</action>
  <verify>[Command or check to prove it worked]</verify>
  <done>[Measurable acceptance criteria]</done>
</task>

<task type="auto">
  <name>Task 2: [Action-oriented name]</name>
  <files>path/to/file.ext</files>
  <action>[Specific implementation]</action>
  <verify>[Command or check]</verify>
  <done>[Acceptance criteria]</done>
</task>

<!-- For checkpoint task examples and patterns, see @~/.claude/get-shit-done/references/checkpoints.md -->
<!-- Key rule: Claude starts dev server BEFORE human-verify checkpoints. User only visits URLs. -->

<task type="checkpoint:decision" gate="blocking">
  <decision>[What needs deciding]</decision>
  <context>[Why this decision matters]</context>
  <options>
    <option id="option-a"><name>[Name]</name><pros>[Benefits]</pros><cons>[Tradeoffs]</cons></option>
    <option id="option-b"><name>[Name]</name><pros>[Benefits]</pros><cons>[Tradeoffs]</cons></option>
  </options>
  <resume-signal>Select: option-a or option-b</resume-signal>
</task>

<task type="checkpoint:human-verify" gate="blocking">
  <what-built>[What Claude built] - server running at [URL]</what-built>
  <how-to-verify>Visit [URL] and verify: [visual checks only, NO CLI commands]</how-to-verify>
  <resume-signal>Type "approved" or describe issues</resume-signal>
</task>

</tasks>

<verification>
Before declaring plan complete:
- [ ] [Specific test command]
- [ ] [Build/type check passes]
- [ ] [Behavior verification]
</verification>

<success_criteria>

- All tasks completed
- All verification checks pass
- No errors or warnings introduced
- [Plan-specific criteria]
  </success_criteria>

<output>
After completion, create `.planning/phases/XX-name/{phase}-{plan}-SUMMARY.md`
</output>
```

---

## Frontmatter 字段

|领域 |必填 |目的|
|--------|----------|---------|
| `phase` |是的 |相标识符（e.g.、`01-foundation`）|
| `plan` |是的 |阶段内计划编号（e.g.、`01`、`02`）|
| `type` |是的 | standard 计划始终为 `execute`，TDD 计划始终为 `tdd` |
| `wave` |是的 |执行波数（1、2、3...）。在计划时预先计算。 |
| `depends_on` |是的 |该计划所需的计划 ID 数组。 |
| `files_modified` |是的 |该计划涉及的文件。 |
| `autonomous` |是的 |如果没有检查点则为 `true`，如果有检查点则为 `false` |
| `requirements` |是的 | **必须** 列出路线图中的要求 ID。每项路线图要求必须出现在至少一个计划中。 |
| `user_setup` |没有 |一系列人工所需的设置项（外部服务）|
| `must_haves` |是的 |目标向后验证标准（见下文）|

**波是预先计算的：**波数是在 `/gsd:plan-phase` 期间分配的。执行阶段直接从 frontmatter 读取 `wave` 并按波数对计划进行分组。无需运行时依赖性分析。

**必须具备的启用验证功能：** `must_haves` 字段承载着从计划到执行的目标后向要求。所有计划完成后，执行阶段会生成一个验证子代理，根据实际代码库检查这些标准。

---

## 并行与顺序

<parallel_examples>

**第一波候选者（并行）：**

```yaml
# Plan 01 - User feature
wave: 1
depends_on: []
files_modified: [src/models/user.ts, src/api/users.ts]
autonomous: true

# Plan 02 - Product feature (no overlap with Plan 01)
wave: 1
depends_on: []
files_modified: [src/models/product.ts, src/api/products.ts]
autonomous: true

# Plan 03 - Order feature (no overlap)
wave: 1
depends_on: []
files_modified: [src/models/order.ts, src/api/orders.ts]
autonomous: true
```

所有三个并行运行（第 1 波）- 没有依赖性，没有文件冲突。

**顺序（真正的依赖）：**

```yaml
# Plan 01 - Auth foundation
wave: 1
depends_on: []
files_modified: [src/lib/auth.ts, src/middleware/auth.ts]
autonomous: true

# Plan 02 - Protected features (needs auth)
wave: 2
depends_on: ["01"]
files_modified: [src/features/dashboard.ts]
autonomous: true
```

第 2 波中的计划 02 等待第 1 波中的计划 01 - 对身份验证类型/中间件的真正依赖。

**检查点计划：**

```yaml
# Plan 03 - UI with verification
wave: 3
depends_on: ["01", "02"]
files_modified: [src/components/Dashboard.tsx]
autonomous: false  # Has checkpoint:human-verify
```

第 3 波在第 1 波和第 2 波之后运行。在检查点暂停，编排器向用户呈现，在批准后恢复。

</parallel_examples>

---

## 上下文部分

**并行感知上下文：**

```markdown
<context>
@.planning/PROJECT.md
@.planning/ROADMAP.md
@.planning/STATE.md

# Only include SUMMARY refs if genuinely needed:
# - This plan imports types from prior plan
# - Prior plan made decision affecting this plan
# - Prior plan's output is input to this plan
#
# Independent plans need NO prior SUMMARY references.
# Do NOT reflexively chain: 02 refs 01, 03 refs 02...

@src/relevant/source.ts
</context>
```

**错误的模式（创建错误的依赖关系）：**
```markdown
<context>
@.planning/phases/03-features/03-01-SUMMARY.md  # Just because it's earlier
@.planning/phases/03-features/03-02-SUMMARY.md  # Reflexive chaining
</context>
```

---

## 范围指南

**计划尺寸：**

- 每个计划 2-3 个任务
- ~50% 上下文使用最大值
- 复杂的阶段：多个重点计划，而不是一个大型计划

**何时拆分：**

- 不同的子系统（auth vs API vs UI）
- >3个任务
- 上下文溢出的风险
- TDD 候选者 - 单独的计划

**首选垂直切片：**

```
PREFER: Plan 01 = User (model + API + UI)
        Plan 02 = Product (model + API + UI)

AVOID:  Plan 01 = All models
        Plan 02 = All APIs
        Plan 03 = All UIs
```

---

## TDD 计划

TDD 功能与 `type: tdd` 一起获得专用计划。

**启发式：** 你能在写`fn`之前先写`expect(fn(input)).toBe(output)`吗？
→ 是：创建 TDD 计划
→ 否：standard 计划中的标准任务

有关 TDD 计划结构，请参阅 `~/.claude/get-shit-done/references/tdd.md`。

---

## 任务类型

|类型 |用于 |自治|
|------|---------|----------|
| `auto` | Claude 可以独立完成所有事情 |完全自主|
| `checkpoint:human-verify` |视觉/功能验证|暂停，返回orchestrator |
| `checkpoint:decision` |实施选择|暂停，返回orchestrator |
| `checkpoint:human-action` |真正不可避免的手动步骤（罕见）|暂停，返回orchestrator |**并行执行中的检查点行为：**
- 计划运行直到检查点
- 代理返回检查点详细信息 + agent_id
- Orchestrator 呈现给用户
- 用户回应
- Orchestrator 使用 `resume: agent_id` 恢复代理

---

## 示例

**自主并行计划：**

```markdown
---
phase: 03-features
plan: 01
type: execute
wave: 1
depends_on: []
files_modified: [src/features/user/model.ts, src/features/user/api.ts, src/features/user/UserList.tsx]
autonomous: true
---

<objective>
Implement complete User feature as vertical slice.

Purpose: Self-contained user management that can run parallel to other features.
Output: User model, API endpoints, and UI components.
</objective>

<context>
@.planning/PROJECT.md
@.planning/ROADMAP.md
@.planning/STATE.md
</context>

<tasks>
<task type="auto">
  <name>Task 1: Create User model</name>
  <files>src/features/user/model.ts</files>
  <action>Define User type with id, email, name, createdAt. Export TypeScript interface.</action>
  <verify>tsc --noEmit passes</verify>
  <done>User type exported and usable</done>
</task>

<task type="auto">
  <name>Task 2: Create User API endpoints</name>
  <files>src/features/user/api.ts</files>
  <action>GET /users (list), GET /users/:id (single), POST /users (create). Use User type from model.</action>
  <verify>curl tests pass for all endpoints</verify>
  <done>All CRUD operations work</done>
</task>
</tasks>

<verification>
- [ ] npm run build succeeds
- [ ] API endpoints respond correctly
</verification>

<success_criteria>
- All tasks completed
- User feature works end-to-end
</success_criteria>

<output>
After completion, create `.planning/phases/03-features/03-01-SUMMARY.md`
</output>
```

**带检查点的计划（非自治）：**

```markdown
---
phase: 03-features
plan: 03
type: execute
wave: 2
depends_on: ["03-01", "03-02"]
files_modified: [src/components/Dashboard.tsx]
autonomous: false
---

<objective>
Build dashboard with visual verification.

Purpose: Integrate user and product features into unified view.
Output: Working dashboard component.
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/execute-plan.md
@~/.claude/get-shit-done/templates/summary.md
@~/.claude/get-shit-done/references/checkpoints.md
</execution_context>

<context>
@.planning/PROJECT.md
@.planning/ROADMAP.md
@.planning/phases/03-features/03-01-SUMMARY.md
@.planning/phases/03-features/03-02-SUMMARY.md
</context>

<tasks>
<task type="auto">
  <name>Task 1: Build Dashboard layout</name>
  <files>src/components/Dashboard.tsx</files>
  <action>Create responsive grid with UserList and ProductList components. Use Tailwind for styling.</action>
  <verify>npm run build succeeds</verify>
  <done>Dashboard renders without errors</done>
</task>

<!-- Checkpoint pattern: Claude starts server, user visits URL. See checkpoints.md for full patterns. -->
<task type="auto">
  <name>Start dev server</name>
  <action>Run `npm run dev` in background, wait for ready</action>
  <verify>curl localhost:3000 returns 200</verify>
</task>

<task type="checkpoint:human-verify" gate="blocking">
  <what-built>Dashboard - server at http://localhost:3000</what-built>
  <how-to-verify>Visit localhost:3000/dashboard. Check: desktop grid, mobile stack, no scroll issues.</how-to-verify>
  <resume-signal>Type "approved" or describe issues</resume-signal>
</task>
</tasks>

<verification>
- [ ] npm run build succeeds
- [ ] Visual verification passed
</verification>

<success_criteria>
- All tasks completed
- User approved visual layout
</success_criteria>

<output>
After completion, create `.planning/phases/03-features/03-03-SUMMARY.md`
</output>
```

---

## 反模式

**不好：自反依赖链**
```yaml
depends_on: ["03-01"]  # Just because 01 comes before 02
```

**不好：水平图层分组**
```
Plan 01: All models
Plan 02: All APIs (depends on 01)
Plan 03: All UIs (depends on 02)
```

**不好：缺少自治标志**
```yaml
# Has checkpoint but no autonomous: false
depends_on: []
files_modified: [...]
# autonomous: ???  <- Missing!
```

**不好：任务模糊**
```xml
<task type="auto">
  <name>Set up authentication</name>
  <action>Add auth to the app</action>
</task>
```

---

## 指南

- 始终使用 XML 结构进行 Claude 解析
- 每个计划均包含 `wave`、`depends_on`、`files_modified`、`autonomous`
- 更喜欢垂直切片而不是水平层
- 仅在真正需要时参考之前的摘要
- 将检查点与同一计划中的相关 auto 任务分组
- 每个计划 2-3 个任务，最大上下文 50%

---

## 用户设置（外部服务）

当计划引入需要人工配置的外部服务时，请在 frontmatter 中声明：

```yaml
user_setup:
  - service: stripe
    why: "Payment processing requires API keys"
    env_vars:
      - name: STRIPE_SECRET_KEY
        source: "Stripe Dashboard → Developers → API keys → Secret key"
      - name: STRIPE_WEBHOOK_SECRET
        source: "Stripe Dashboard → Developers → Webhooks → Signing secret"
    dashboard_config:
      - task: "Create webhook endpoint"
        location: "Stripe Dashboard → Developers → Webhooks → Add endpoint"
        details: "URL: https://[your-domain]/api/webhooks/stripe"
    local_dev:
      - "stripe listen --forward-to localhost:3000/api/webhooks/stripe"
```

**自动化优先规则：** `user_setup` 仅包含 Claude 字面上无法做到的事情：
- 帐户创建（需要人工注册）
- 秘密检索（需要仪表板访问）
- 仪表板配置（需要人在浏览器中）

**不包括：** 软件包安装、代码更改、文件创建、CLI 命令 Claude 可以运行。

**结果：** 执行计划为用户生成带有清单的 `{phase}-USER-SETUP.md`。

有关完整架构和示例，请参阅 `~/.claude/get-shit-done/templates/user-setup.md`

---

## 必备条件（目标向后验证）

`must_haves` 字段定义要实现阶段目标必须为 TRUE 的内容。在计划中产生，在执行后验证。

**结构：**

```yaml
must_haves:
  truths:
    - "User can see existing messages"
    - "User can send a message"
    - "Messages persist across refresh"
  artifacts:
    - path: "src/components/Chat.tsx"
      provides: "Message list rendering"
      min_lines: 30
    - path: "src/app/api/chat/route.ts"
      provides: "Message CRUD operations"
      exports: ["GET", "POST"]
    - path: "prisma/schema.prisma"
      provides: "Message model"
      contains: "model Message"
  key_links:
    - from: "src/components/Chat.tsx"
      to: "/api/chat"
      via: "fetch in useEffect"
      pattern: "fetch.*api/chat"
    - from: "src/app/api/chat/route.ts"
      to: "prisma.message"
      via: "database query"
      pattern: "prisma\\.message\\.(find|create)"
```

**字段说明：**

|领域 |目的|
|--------|---------|
| `truths` |从用户角度观察的行为。每个都必须是可测试的。 |
| `artifacts` |实际实施时必须存在的文件。 |
| `artifacts[].path` |相对于项目根目录的文件路径。 |
| `artifacts[].provides` |这个神器提供了什么。 |
| `artifacts[].min_lines` |选修的。被视为实质性的最低限度。 |
| `artifacts[].exports` |选修的。预计出口量需核实。 |
| `artifacts[].contains` |选修的。文件中必须存在的模式。 |
| `key_links` |工件之间的关键联系。 |
| `key_links[].from` |源神器。 |
| `key_links[].to` |目标工件或端点。 |
| `key_links[].via` |它们如何连接（描述）。 |
| `key_links[].pattern` |选修的。用于验证连接是否存在的正则表达式。 |

**为什么这很重要：**

任务完成≠目标实现。任务“创建聊天组件”可以通过创建占位符来完成。 `must_haves` 字段捕获必须实际工作的内容，从而使验证能够在差距复合之前捕获差距。

**验证流程：**

1. 计划阶段从阶段目标导出must_haves（目标向后）
2. Must_haves写入PLAN.md frontmatter
3.执行阶段运行所有计划
4. 验证子代理根据代码库检查 Must_haves
5. 发现差距→制定修复计划→执行→重新验证
6. 所有必备条件均已通过 → 阶段完成

验证逻辑参见`~/.claude/get-shit-done/workflows/verify-phase.md`。
