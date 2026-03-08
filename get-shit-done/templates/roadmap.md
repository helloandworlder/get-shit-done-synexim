# 路线图模板

`.planning/ROADMAP.md` 的模板。

## 初始路线图（v1.0 Greenfield）

```markdown
# Roadmap: [Project Name]

## Overview

[One paragraph describing the journey from start to finish]

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: [Name]** - [One-line description]
- [ ] **Phase 2: [Name]** - [One-line description]
- [ ] **Phase 3: [Name]** - [One-line description]
- [ ] **Phase 4: [Name]** - [One-line description]

## Phase Details

### Phase 1: [Name]
**Goal**: [What this phase delivers]
**Depends on**: Nothing (first phase)
**Requirements**: [REQ-01, REQ-02, REQ-03]  <!-- brackets optional, parser handles both formats -->
**Success Criteria** (what must be TRUE):
  1. [Observable behavior from user perspective]
  2. [Observable behavior from user perspective]
  3. [Observable behavior from user perspective]
**Plans**: [Number of plans, e.g., "3 plans" or "TBD"]

Plans:
- [ ] 01-01: [Brief description of first plan]
- [ ] 01-02: [Brief description of second plan]
- [ ] 01-03: [Brief description of third plan]

### Phase 2: [Name]
**Goal**: [What this phase delivers]
**Depends on**: Phase 1
**Requirements**: [REQ-04, REQ-05]
**Success Criteria** (what must be TRUE):
  1. [Observable behavior from user perspective]
  2. [Observable behavior from user perspective]
**Plans**: [Number of plans]

Plans:
- [ ] 02-01: [Brief description]
- [ ] 02-02: [Brief description]

### Phase 2.1: Critical Fix (INSERTED)
**Goal**: [Urgent work inserted between phases]
**Depends on**: Phase 2
**Success Criteria** (what must be TRUE):
  1. [What the fix achieves]
**Plans**: 1 plan

Plans:
- [ ] 02.1-01: [Description]

### Phase 3: [Name]
**Goal**: [What this phase delivers]
**Depends on**: Phase 2
**Requirements**: [REQ-06, REQ-07, REQ-08]
**Success Criteria** (what must be TRUE):
  1. [Observable behavior from user perspective]
  2. [Observable behavior from user perspective]
  3. [Observable behavior from user perspective]
**Plans**: [Number of plans]

Plans:
- [ ] 03-01: [Brief description]
- [ ] 03-02: [Brief description]

### Phase 4: [Name]
**Goal**: [What this phase delivers]
**Depends on**: Phase 3
**Requirements**: [REQ-09, REQ-10]
**Success Criteria** (what must be TRUE):
  1. [Observable behavior from user perspective]
  2. [Observable behavior from user perspective]
**Plans**: [Number of plans]

Plans:
- [ ] 04-01: [Brief description]

## Progress

**Execution Order:**
Phases execute in numeric order: 2 → 2.1 → 2.2 → 3 → 3.1 → 4

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. [Name] | 0/3 | Not started | - |
| 2. [Name] | 0/2 | Not started | - |
| 3. [Name] | 0/2 | Not started | - |
| 4. [Name] | 0/1 | Not started | - |
```

<guidelines>
**初步规划（v1.0）：**
- 相位数取决于粒度设置（粗略：3-5，standard：5-8，精细：8-12）
- 每个阶段都必须交付一个或多个“完整可用”的基础功能，而不是单纯的技术分层成果
- 阶段可以有 1+ 个计划（如果超过 3 个任务或多个子系统则拆分）
- 计划统一命名：`{phase}-{plan}-PLAN.md`（例如 `01-02-PLAN.md`）
- 没有时间估计（这不是企业 PM）
- 通过执行工作流程更新进度表
- 计划计数最初可以是“待定”，在计划过程中进行细化
- 对后台/管理系统类项目，禁止把数据库、ORM、API、前端拆成独立阶段；正确做法是每个阶段都覆盖前后端与数据层，至少让一个模块真正可用
- 如果阶段涉及前端，实现前必须先确认 Gemini AI Studio MVP 原型已与需求和当前里程碑对齐

**成功标准：**
- 每个阶段 2-5 个可观察的行为（从用户的角度）
- 在创建路线图期间根据要求进行交叉检查
- 计划阶段向下游流动至 `must_haves`
- 执行后通过verify-phase进行验证
- 格式：“用户可以 [action]”或“[Thing] 有效/存在”
- 阶段完成后，用户应能实际启动项目并测试这些行为，而不只是看到底层代码已存在

**里程碑发布后：**
- 折叠 `<details>` 标签中已完成的里程碑
- 为即将开展的工作添加新的里程碑部分
- 保持连续的阶段编号（永远不要从01重新开始）
</guidelines>

<status_values>
- `Not started` - 还没有开始
- `In progress` - 目前正在工作
- `Complete` - 完成（添加完成日期）
- `Deferred` - 推到稍后（有原因）
</status_values>

## 里程碑分组路线图（v1.0 发布后）

完成第一个里程碑后，重新组织里程碑分组：

```markdown
# Roadmap: [Project Name]

## Milestones

- ✅ **v1.0 MVP** - Phases 1-4 (shipped YYYY-MM-DD)
- 🚧 **v1.1 [Name]** - Phases 5-6 (in progress)
- 📋 **v2.0 [Name]** - Phases 7-10 (planned)

## Phases

<details>
<summary>✅ v1.0 MVP (Phases 1-4) - SHIPPED YYYY-MM-DD</summary>

### Phase 1: [Name]
**Goal**: [What this phase delivers]
**Plans**: 3 plans

Plans:
- [x] 01-01: [Brief description]
- [x] 01-02: [Brief description]
- [x] 01-03: [Brief description]

[... remaining v1.0 phases ...]

</details>

### 🚧 v1.1 [Name] (In Progress)

**Milestone Goal:** [What v1.1 delivers]

#### Phase 5: [Name]
**Goal**: [What this phase delivers]
**Depends on**: Phase 4
**Plans**: 2 plans

Plans:
- [ ] 05-01: [Brief description]
- [ ] 05-02: [Brief description]

[... remaining v1.1 phases ...]

### 📋 v2.0 [Name] (Planned)

**Milestone Goal:** [What v2.0 delivers]

[... v2.0 phases ...]

## Progress

| Phase | Milestone | Plans Complete | Status | Completed |
|-------|-----------|----------------|--------|-----------|
| 1. Foundation | v1.0 | 3/3 | Complete | YYYY-MM-DD |
| 2. Features | v1.0 | 2/2 | Complete | YYYY-MM-DD |
| 5. Security | v1.1 | 0/2 | Not started | - |
```

**注释：**
- 里程碑表情符号：✅ 已发货、🚧 正在进行、📋 计划中
- 已完成的里程碑在 `<details>` 中折叠以提高可读性
- 扩大当前/未来的里程碑
- 连续相编号（01-99）
- 进度表包括里程碑列
