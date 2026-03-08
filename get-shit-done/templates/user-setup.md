# 用户设置模板

`.planning/phases/XX-name/{phase}-USER-SETUP.md` 的模板 - Claude 无法自动化的人工所需配置。

**目的：** 实际上需要人工操作的文档设置任务 - 帐户创建、仪表板配置、秘密检索。 Claude 自动化一切可能；该文件仅捕获剩余的内容。

---

## 文件模板

```markdown
# Phase {X}: User Setup Required

**Generated:** [YYYY-MM-DD]
**Phase:** {phase-name}
**Status:** Incomplete

Complete these items for the integration to function. Claude automated everything possible; these items require human access to external dashboards/accounts.

## Environment Variables

| Status | Variable | Source | Add to |
|--------|----------|--------|--------|
| [ ] | `ENV_VAR_NAME` | [Service Dashboard → Path → To → Value] | `.env.local` |
| [ ] | `ANOTHER_VAR` | [Service Dashboard → Path → To → Value] | `.env.local` |

## Account Setup

[Only if new account creation is required]

- [ ] **Create [Service] account**
  - URL: [signup URL]
  - Skip if: Already have account

## Dashboard Configuration

[Only if dashboard configuration is required]

- [ ] **[Configuration task]**
  - Location: [Service Dashboard → Path → To → Setting]
  - Set to: [Required value or configuration]
  - Notes: [Any important details]

## Verification

After completing setup, verify with:

```bash
#[Verification commands]
```

Expected results:
- [What success looks like]

---

**Once all items complete:** Mark status as "Complete" at top of file.
```

---

## 何时生成

当计划 frontmatter 包含 `user_setup` 字段时生成 `{phase}-USER-SETUP.md`。

**触发器：** `user_setup` 存在于 PLAN.md frontmatter 中并且有项目。

**位置：** 与 PLAN.md 和 SUMMARY.md 相同的目录。

**时间：** 在任务完成后、SUMMARY.md 创建之前的 execute-plan.md 期间生成。

---

## Frontmatter 架构

在PLAN.md、`user_setup`中声明了人类所需的配置：

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
        details: "URL: https://[your-domain]/api/webhooks/stripe, Events: checkout.session.completed, customer.subscription.*"
    local_dev:
      - "Run: stripe listen --forward-to localhost:3000/api/webhooks/stripe"
      - "Use the webhook secret from CLI output for local testing"
```

---

## 自动化优先规则

**USER-SETUP.md 仅包含 Claude 字面上无法做到的事情。**

| Claude 可以（不在用户设置中） | Claude 无法执行（→ 用户设置）|
|------------------------------------------------|--------------------------------|
| `npm install stripe` |创建 Stripe 帐户 |
| Write webhook 处理程序代码 |从仪表板获取 API 密钥 |
|创建`.env.local`文件结构|复制实际的秘密值 |
|运行`stripe listen` |验证 Stripe CLI（浏览器 OAuth）|
|配置package.json |访问外部服务仪表板 |
| Write 任意码 |从第三方系统检索机密 |

**测试：**“这是否需要人在浏览器中访问 Claude 没有凭据的帐户？”
- 是 → USER-SETUP.md
- 否 → Claude 自动执行

---

## 特定于服务的示例

<stripe_example>
```markdown
# Phase 10: User Setup Required

**Generated:** 2025-01-14
**Phase:** 10-monetization
**Status:** Incomplete

Complete these items for Stripe integration to function.

## Environment Variables

| Status | Variable | Source | Add to |
|--------|----------|--------|--------|
| [ ] | `STRIPE_SECRET_KEY` | Stripe Dashboard → Developers → API keys → Secret key | `.env.local` |
| [ ] | `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY` | Stripe Dashboard → Developers → API keys → Publishable key | `.env.local` |
| [ ] | `STRIPE_WEBHOOK_SECRET` | Stripe Dashboard → Developers → Webhooks → [endpoint] → Signing secret | `.env.local` |

## Account Setup

- [ ] **Create Stripe account** (if needed)
  - URL: https://dashboard.stripe.com/register
  - Skip if: Already have Stripe account

## Dashboard Configuration

- [ ] **Create webhook endpoint**
  - Location: Stripe Dashboard → Developers → Webhooks → Add endpoint
  - Endpoint URL: `https://[your-domain]/api/webhooks/stripe`
  - Events to send:
    - `checkout.session.completed`
    - `customer.subscription.created`
    - `customer.subscription.updated`
    - `customer.subscription.deleted`

- [ ] **Create products and prices** (if using subscription tiers)
  - Location: Stripe Dashboard → Products → Add product
  - Create each subscription tier
  - Copy Price IDs to:
    - `STRIPE_STARTER_PRICE_ID`
    - `STRIPE_PRO_PRICE_ID`

## Local Development

For local webhook testing:
```bash
stripe 监听 --forward-to localhost:3000/api/webhooks/stripe
```
Use the webhook signing secret from CLI output (starts with `whsec_`).

## Verification

After completing setup:

```bash
# 检查环境变量是否设置
grep 条纹 .env.local

# 验证构建过程
npm 运行构建

# 测试 webhook 端点（应该返回 400 错误签名，而不是 500 崩溃）
卷曲 -X POST http://localhost:3000/api/webhooks/stripe \
  -H“内容类型：application/json”\
  -d '{}'
```

Expected: Build passes, webhook returns 400 (signature validation working).

---

**Once all items complete:** Mark status as "Complete" at top of file.
```
</stripe_example>

<supabase_example>
```markdown
# Phase 2: User Setup Required

**Generated:** 2025-01-14
**Phase:** 02-authentication
**Status:** Incomplete

Complete these items for Supabase Auth to function.

## Environment Variables

| Status | Variable | Source | Add to |
|--------|----------|--------|--------|
| [ ] | `NEXT_PUBLIC_SUPABASE_URL` | Supabase Dashboard → Settings → API → Project URL | `.env.local` |
| [ ] | `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase Dashboard → Settings → API → anon public | `.env.local` |
| [ ] | `SUPABASE_SERVICE_ROLE_KEY` | Supabase Dashboard → Settings → API → service_role | `.env.local` |

## Account Setup

- [ ] **Create Supabase project**
  - URL: https://supabase.com/dashboard/new
  - Skip if: Already have project for this app

## Dashboard Configuration

- [ ] **Enable Email Auth**
  - Location: Supabase Dashboard → Authentication → Providers
  - Enable: Email provider
  - Configure: Confirm email (on/off based on preference)

- [ ] **Configure OAuth providers** (if using social login)
  - Location: Supabase Dashboard → Authentication → Providers
  - For Google: Add Client ID and Secret from Google Cloud Console
  - For GitHub: Add Client ID and Secret from GitHub OAuth Apps

## Verification

After completing setup:

```bash
# 检查环境变量
grep SUPABASE .env.local

# 验证连接（在项目目录中运行）
npx supabase 状态
```

---

**Once all items complete:** Mark status as "Complete" at top of file.
```
</supabase_example>

<sendgrid_example>
```markdown
# Phase 5: User Setup Required

**Generated:** 2025-01-14
**Phase:** 05-notifications
**Status:** Incomplete

Complete these items for SendGrid email to function.

## Environment Variables

| Status | Variable | Source | Add to |
|--------|----------|--------|--------|
| [ ] | `SENDGRID_API_KEY` | SendGrid Dashboard → Settings → API Keys → Create API Key | `.env.local` |
| [ ] | `SENDGRID_FROM_EMAIL` | Your verified sender email address | `.env.local` |

## Account Setup

- [ ] **Create SendGrid account**
  - URL: https://signup.sendgrid.com/
  - Skip if: Already have account

## Dashboard Configuration

- [ ] **Verify sender identity**
  - Location: SendGrid Dashboard → Settings → Sender Authentication
  - Option 1: Single Sender Verification (quick, for dev)
  - Option 2: Domain Authentication (production)

- [ ] **Create API Key**
  - Location: SendGrid Dashboard → Settings → API Keys → Create API Key
  - Permission: Restricted Access → Mail Send (Full Access)
  - Copy key immediately (shown only once)

## Verification

After completing setup:

```bash
# 检查环境变量
grep SENDGRID .env.local

# 测试电子邮件发送（替换为您的测试电子邮件）
卷曲 -X POST http://localhost:3000/api/test-email \
  -H“内容类型：application/json”\
  -d '{"to": "your@email.com"}'
```

---

**Once all items complete:** Mark status as "Complete" at top of file.
```
</sendgrid_example>

---

## 指南

**绝不包括：** 实际秘密值。 Claude 可以自动化的步骤（软件包安装、代码更改）。

**命名：** `{phase}-USER-SETUP.md` 与相号模式匹配。
**状态跟踪：** 用户标记复选框并在完成后更新状态行。
**可搜索性：** `grep -r "USER-SETUP" .planning/` 查找具有用户需求的所有阶段。