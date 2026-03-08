# 需求模板

`.planning/REQUIREMENTS.md` 模板 — 定义“完成”的可检查要求。

<template>

```markdown
# Requirements: [Project Name]

**Defined:** [date]
**Core Value:** [from PROJECT.md]

## v1 Requirements

Requirements for initial release. Each maps to roadmap phases.

### Authentication

- [ ] **AUTH-01**: User can sign up with email and password
- [ ] **AUTH-02**: User receives email verification after signup
- [ ] **AUTH-03**: User can reset password via email link
- [ ] **AUTH-04**: User session persists across browser refresh

### [Category 2]

- [ ] **[CAT]-01**: [Requirement description]
- [ ] **[CAT]-02**: [Requirement description]
- [ ] **[CAT]-03**: [Requirement description]

### [Category 3]

- [ ] **[CAT]-01**: [Requirement description]
- [ ] **[CAT]-02**: [Requirement description]

## v2 Requirements

Deferred to future release. Tracked but not in current roadmap.

### [Category]

- **[CAT]-01**: [Requirement description]
- **[CAT]-02**: [Requirement description]

## Out of Scope

Explicitly excluded. Documented to prevent scope creep.

| Feature | Reason |
|---------|--------|
| [Feature] | [Why excluded] |
| [Feature] | [Why excluded] |

## Traceability

Which phases cover which requirements. Updated during roadmap creation.

| Requirement | Phase | Status |
|-------------|-------|--------|
| AUTH-01 | Phase 1 | Pending |
| AUTH-02 | Phase 1 | Pending |
| AUTH-03 | Phase 1 | Pending |
| AUTH-04 | Phase 1 | Pending |
| [REQ-ID] | Phase [N] | Pending |

**Coverage:**
- v1 requirements: [X] total
- Mapped to phases: [Y]
- Unmapped: [Z] ⚠️

---
*Requirements defined: [date]*
*Last updated: [date] after [trigger]*
```

</template>

<guidelines>

**需求格式：**
- ID：`[CATEGORY]-[NUMBER]`（AUTH-01、内容-02、社交-03）
- 描述：以用户为中心、可测试、原子
- 复选框：仅适用于 v1 要求（v2 尚不可操作）

**类别：**
- 源自研究 FEATURES.md 类别
- 与领域约定保持一致
- 典型：身份验证、内容、社交、通知、审核、付款、管理

**v1 与 v2：**
- v1：承诺范围，将处于路线图阶段
- v2：已确认但已推迟，不在当前路线图中
- 移动 v2 → v1 需要更新路线图

**超出范围：**
- 带有推理的明确排除
- 防止“你为什么不包括 X？”后来
- 研究中的反特征属于此处并带有警告

**可追溯性：**
- 最初为空，在路线图创建期间填充
- 每个需求恰好对应一个阶段
- 未映射的需求=路线图差距

**状态值：**
- 待定：未开始
- 进行中：阶段已激活
- 完成：要求已验证
- 被阻止：等待外部因素

</guidelines>

<evolution>

**每个阶段完成后：**
1. 将涵盖的需求标记为“完成”
2.更新溯源状态
3. 注意任何改变范围的要求
4. 停下来启动项目，让用户验证本阶段新增功能，并记录用户反馈

**路线图更新后：**
1. 验证所有 v1 要求是否仍然映射
2. 如果范围扩大则添加新要求
3. 如果范围已解除，则将需求移至 v2/超出范围

**要求完成标准：**
- 在以下情况下，要求为“完整”：
  - 功能已实施
  - 功能已验证（测试通过，手动检查完成）
  - 功能已承诺
  - 用户已经收到明确的测试路径、登录方式与反馈入口

</evolution>

<example>

```markdown
# Requirements: CommunityApp

**Defined:** 2025-01-14
**Core Value:** Users can share and discuss content with people who share their interests

## v1 Requirements

### Authentication

- [ ] **AUTH-01**: User can sign up with email and password
- [ ] **AUTH-02**: User receives email verification after signup
- [ ] **AUTH-03**: User can reset password via email link
- [ ] **AUTH-04**: User session persists across browser refresh

### Profiles

- [ ] **PROF-01**: User can create profile with display name
- [ ] **PROF-02**: User can upload avatar image
- [ ] **PROF-03**: User can write bio (max 500 chars)
- [ ] **PROF-04**: User can view other users' profiles

### Content

- [ ] **CONT-01**: User can create text post
- [ ] **CONT-02**: User can upload image with post
- [ ] **CONT-03**: User can edit own posts
- [ ] **CONT-04**: User can delete own posts
- [ ] **CONT-05**: User can view feed of posts

### Social

- [ ] **SOCL-01**: User can follow other users
- [ ] **SOCL-02**: User can unfollow users
- [ ] **SOCL-03**: User can like posts
- [ ] **SOCL-04**: User can comment on posts
- [ ] **SOCL-05**: User can view activity feed (followed users' posts)

## v2 Requirements

### Notifications

- **NOTF-01**: User receives in-app notifications
- **NOTF-02**: User receives email for new followers
- **NOTF-03**: User receives email for comments on own posts
- **NOTF-04**: User can configure notification preferences

### Moderation

- **MODR-01**: User can report content
- **MODR-02**: User can block other users
- **MODR-03**: Admin can view reported content
- **MODR-04**: Admin can remove content
- **MODR-05**: Admin can ban users

## Out of Scope

| Feature | Reason |
|---------|--------|
| Real-time chat | High complexity, not core to community value |
| Video posts | Storage/bandwidth costs, defer to v2+ |
| OAuth login | Email/password sufficient for v1 |
| Mobile app | Web-first, mobile later |

## Traceability

| Requirement | Phase | Status |
|-------------|-------|--------|
| AUTH-01 | Phase 1 | Pending |
| AUTH-02 | Phase 1 | Pending |
| AUTH-03 | Phase 1 | Pending |
| AUTH-04 | Phase 1 | Pending |
| PROF-01 | Phase 2 | Pending |
| PROF-02 | Phase 2 | Pending |
| PROF-03 | Phase 2 | Pending |
| PROF-04 | Phase 2 | Pending |
| CONT-01 | Phase 3 | Pending |
| CONT-02 | Phase 3 | Pending |
| CONT-03 | Phase 3 | Pending |
| CONT-04 | Phase 3 | Pending |
| CONT-05 | Phase 3 | Pending |
| SOCL-01 | Phase 4 | Pending |
| SOCL-02 | Phase 4 | Pending |
| SOCL-03 | Phase 4 | Pending |
| SOCL-04 | Phase 4 | Pending |
| SOCL-05 | Phase 4 | Pending |

**Coverage:**
- v1 requirements: 18 total
- Mapped to phases: 18
- Unmapped: 0 ✓

---
*Requirements defined: 2025-01-14*
*Last updated: 2025-01-14 after initial definition*
```

</example>
