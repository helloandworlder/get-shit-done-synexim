# 代码库问题模板

`.planning/codebase/CONCERNS.md` 模板 - 捕获已知问题和需要注意的区域。

**目的：** 关于代码库的可操作警告。重点是“做出改变时要注意什么”。

---

## 文件模板

```markdown
# Codebase Concerns

**Analysis Date:** [YYYY-MM-DD]

## Tech Debt

**[Area/Component]:**
- Issue: [What's the shortcut/workaround]
- Why: [Why it was done this way]
- Impact: [What breaks or degrades because of it]
- Fix approach: [How to properly address it]

**[Area/Component]:**
- Issue: [What's the shortcut/workaround]
- Why: [Why it was done this way]
- Impact: [What breaks or degrades because of it]
- Fix approach: [How to properly address it]

## Known Bugs

**[Bug description]:**
- Symptoms: [What happens]
- Trigger: [How to reproduce]
- Workaround: [Temporary mitigation if any]
- Root cause: [If known]
- Blocked by: [If waiting on something]

**[Bug description]:**
- Symptoms: [What happens]
- Trigger: [How to reproduce]
- Workaround: [Temporary mitigation if any]
- Root cause: [If known]

## Security Considerations

**[Area requiring security care]:**
- Risk: [What could go wrong]
- Current mitigation: [What's in place now]
- Recommendations: [What should be added]

**[Area requiring security care]:**
- Risk: [What could go wrong]
- Current mitigation: [What's in place now]
- Recommendations: [What should be added]

## Performance Bottlenecks

**[Slow operation/endpoint]:**
- Problem: [What's slow]
- Measurement: [Actual numbers: "500ms p95", "2s load time"]
- Cause: [Why it's slow]
- Improvement path: [How to speed it up]

**[Slow operation/endpoint]:**
- Problem: [What's slow]
- Measurement: [Actual numbers]
- Cause: [Why it's slow]
- Improvement path: [How to speed it up]

## Fragile Areas

**[Component/Module]:**
- Why fragile: [What makes it break easily]
- Common failures: [What typically goes wrong]
- Safe modification: [How to change it without breaking]
- Test coverage: [Is it tested? Gaps?]

**[Component/Module]:**
- Why fragile: [What makes it break easily]
- Common failures: [What typically goes wrong]
- Safe modification: [How to change it without breaking]
- Test coverage: [Is it tested? Gaps?]

## Scaling Limits

**[Resource/System]:**
- Current capacity: [Numbers: "100 req/sec", "10k users"]
- Limit: [Where it breaks]
- Symptoms at limit: [What happens]
- Scaling path: [How to increase capacity]

## Dependencies at Risk

**[Package/Service]:**
- Risk: [e.g., "deprecated", "unmaintained", "breaking changes coming"]
- Impact: [What breaks if it fails]
- Migration plan: [Alternative or upgrade path]

## Missing Critical Features

**[Feature gap]:**
- Problem: [What's missing]
- Current workaround: [How users cope]
- Blocks: [What can't be done without it]
- Implementation complexity: [Rough effort estimate]

## Test Coverage Gaps

**[Untested area]:**
- What's not tested: [Specific functionality]
- Risk: [What could break unnoticed]
- Priority: [High/Medium/Low]
- Difficulty to test: [Why it's not tested yet]

---

*Concerns audit: [date]*
*Update as issues are fixed or new ones discovered*
```

<good_examples>
```markdown
# Codebase Concerns

**Analysis Date:** 2025-01-20

## Tech Debt

**Database queries in React components:**
- Issue: Direct Supabase queries in 15+ page components instead of server actions
- Files: `app/dashboard/page.tsx`, `app/profile/page.tsx`, `app/courses/[id]/page.tsx`, `app/settings/page.tsx` (and 11 more in `app/`)
- Why: Rapid prototyping during MVP phase
- Impact: Can't implement RLS properly, exposes DB structure to client
- Fix approach: Move all queries to server actions in `app/actions/`, add proper RLS policies

**Manual webhook signature validation:**
- Issue: Copy-pasted Stripe webhook verification code in 3 different endpoints
- Files: `app/api/webhooks/stripe/route.ts`, `app/api/webhooks/checkout/route.ts`, `app/api/webhooks/subscription/route.ts`
- Why: Each webhook added ad-hoc without abstraction
- Impact: Easy to miss verification in new webhooks (security risk)
- Fix approach: Create shared `lib/stripe/validate-webhook.ts` middleware

## Known Bugs

**Race condition in subscription updates:**
- Symptoms: User shows as "free" tier for 5-10 seconds after successful payment
- Trigger: Fast navigation after Stripe checkout redirect, before webhook processes
- Files: `app/checkout/success/page.tsx` (redirect handler), `app/api/webhooks/stripe/route.ts` (webhook)
- Workaround: Stripe webhook eventually updates status (self-heals)
- Root cause: Webhook processing slower than user navigation, no optimistic UI update
- Fix: Add polling in `app/checkout/success/page.tsx` after redirect

**Inconsistent session state after logout:**
- Symptoms: User redirected to /dashboard after logout instead of /login
- Trigger: Logout via button in mobile nav (desktop works fine)
- File: `components/MobileNav.tsx` (line ~45, logout handler)
- Workaround: Manual URL navigation to /login works
- Root cause: Mobile nav component not awaiting supabase.auth.signOut()
- Fix: Add await to logout handler in `components/MobileNav.tsx`

## Security Considerations

**Admin role check client-side only:**
- Risk: Admin dashboard pages check isAdmin from Supabase client, no server verification
- Files: `app/admin/page.tsx`, `app/admin/users/page.tsx`, `components/AdminGuard.tsx`
- Current mitigation: None (relying on UI hiding)
- Recommendations: Add middleware to admin routes in `middleware.ts`, verify role server-side

**Unvalidated file uploads:**
- Risk: Users can upload any file type to avatar bucket (no size/type validation)
- File: `components/AvatarUpload.tsx` (upload handler)
- Current mitigation: Supabase bucket limits to 2MB (configured in dashboard)
- Recommendations: Add file type validation (image/* only) in `lib/storage/validate.ts`

## Performance Bottlenecks

**/api/courses endpoint:**
- Problem: Fetching all courses with nested lessons and authors
- File: `app/api/courses/route.ts`
- Measurement: 1.2s p95 response time with 50+ courses
- Cause: N+1 query pattern (separate query per course for lessons)
- Improvement path: Use Prisma include to eager-load lessons in `lib/db/courses.ts`, add Redis caching

**Dashboard initial load:**
- Problem: Waterfall of 5 serial API calls on mount
- File: `app/dashboard/page.tsx`
- Measurement: 3.5s until interactive on slow 3G
- Cause: Each component fetches own data independently
- Improvement path: Convert to Server Component with single parallel fetch

## Fragile Areas

**Authentication middleware chain:**
- File: `middleware.ts`
- Why fragile: 4 different middleware functions run in specific order (auth -> role -> subscription -> logging)
- Common failures: Middleware order change breaks everything, hard to debug
- Safe modification: Add tests before changing order, document dependencies in comments
- Test coverage: No integration tests for middleware chain (only unit tests)

**Stripe webhook event handling:**
- File: `app/api/webhooks/stripe/route.ts`
- Why fragile: Giant switch statement with 12 event types, shared transaction logic
- Common failures: New event type added without handling, partial DB updates on error
- Safe modification: Extract each event handler to `lib/stripe/handlers/*.ts`
- Test coverage: Only 3 of 12 event types have tests

## Scaling Limits

**Supabase Free Tier:**
- Current capacity: 500MB database, 1GB file storage, 2GB bandwidth/month
- Limit: ~5000 users estimated before hitting limits
- Symptoms at limit: 429 rate limit errors, DB writes fail
- Scaling path: Upgrade to Pro ($25/mo) extends to 8GB DB, 100GB storage

**Server-side render blocking:**
- Current capacity: ~50 concurrent users before slowdown
- Limit: Vercel Hobby plan (10s function timeout, 100GB-hrs/mo)
- Symptoms at limit: 504 gateway timeouts on course pages
- Scaling path: Upgrade to Vercel Pro ($20/mo), add edge caching

## Dependencies at Risk

**react-hot-toast:**
- Risk: Unmaintained (last update 18 months ago), React 19 compatibility unknown
- Impact: Toast notifications break, no graceful degradation
- Migration plan: Switch to sonner (actively maintained, similar API)

## Missing Critical Features

**Payment failure handling:**
- Problem: No retry mechanism or user notification when subscription payment fails
- Current workaround: Users manually re-enter payment info (if they notice)
- Blocks: Can't retain users with expired cards, no dunning process
- Implementation complexity: Medium (Stripe webhooks + email flow + UI)

**Course progress tracking:**
- Problem: No persistent state for which lessons completed
- Current workaround: Users manually track progress
- Blocks: Can't show completion percentage, can't recommend next lesson
- Implementation complexity: Low (add completed_lessons junction table)

## Test Coverage Gaps

**Payment flow end-to-end:**
- What's not tested: Full Stripe checkout -> webhook -> subscription activation flow
- Risk: Payment processing could break silently (has happened twice)
- Priority: High
- Difficulty to test: Need Stripe test fixtures and webhook simulation setup

**Error boundary behavior:**
- What's not tested: How app behaves when components throw errors
- Risk: White screen of death for users, no error reporting
- Priority: Medium
- Difficulty to test: Need to intentionally trigger errors in test environment

---

*Concerns audit: 2025-01-20*
*Update as issues are fixed or new ones discovered*
```
</good_examples>

<guidelines>
**CONCERNS.md 属于什么：**
- 具有明显影响和修复方法的技术债务
- 已知错误及重现步骤
- 安全漏洞和缓解建议
- 测量的性能瓶颈
- 脆弱的代码很容易被破坏
- 用数字缩放限制
- 需要注意的依赖关系
- 缺少阻碍工作流程的功能
- 测试覆盖率差距

**什么不属于这里：**
- 没有证据的意见（“代码很乱”）
- 没有解决方案的投诉（“auth 很糟糕”）
- 未来的功能想法（用于产品规划）
- 普通 TODO（位于代码注释中）
- 运行良好的架构决策
- 代码风格的小问题

**填写此模板时：**
- **始终包含文件路径** - 没有位置的问题是不可操作的。使用反引号：`src/file.ts`
- 测量具体（“500ms p95”而不是“慢”）
- 包括错误的重现步骤
- 建议修复方法，而不仅仅是问题
- 专注于可操作的项目
- 按风险/影响确定优先级
- 问题解决后更新
- 添加新发现的 concerns

**语气指南：**
- 专业，不情绪化（“N+1 查询模式”而不是“糟糕的查询”）
- 面向解决方案（“修复：添加索引”而不是“需要修复”）
- 以风险为中心（“可能暴露用户数据”而不是“安全性不好”）
- 事实（“3.5s 加载时间”不是“真的很慢”）

**在以下情况下对于阶段规划很有用：**
- 决定下一步做什么
- 估计变更风险
- 了解哪里要小心
- 优先改进
- 加入新的 Claude 上下文
- 规划重构工作

**如何填充：**
探索代理在代码库映射期间检测这些。对于人类发现的问题，欢迎手动添加。这是活的文件，而不是投诉清单。
</guidelines>