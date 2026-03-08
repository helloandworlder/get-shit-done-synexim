# 里程碑条目模板

完成里程碑时将此条目添加到 `.planning/MILESTONES.md`：

```markdown
## v[X.Y] [Name] (Shipped: YYYY-MM-DD)

**Delivered:** [One sentence describing what shipped]

**Phases completed:** [X-Y] ([Z] plans total)

**Key accomplishments:**
- [Major achievement 1]
- [Major achievement 2]
- [Major achievement 3]
- [Major achievement 4]

**Stats:**
- [X] files created/modified
- [Y] lines of code (primary language)
- [Z] phases, [N] plans, [M] tasks
- [D] days from start to ship (or milestone to milestone)

**Git range:** `feat(XX-XX)` → `feat(YY-YY)`

**What's next:** [Brief description of next milestone goals, or "Project complete"]

---
```

<structure>
如果 MILESTONES.md 不存在，请使用标头创建它：

```markdown
# Project Milestones: [Project Name]

[Entries in reverse chronological order - newest first]
```
</structure>

<guidelines>
**何时创建里程碑：**
- 初始 v1.0 MVP 已发货
- 主要版本发布（v2.0、v3.0）
- 重要的功能里程碑（v1.1、v1.2）
- 归档计划之前（捕获已发货的内容）

**不要为以下目标创建里程碑：**
- 各个阶段的完成（正常工作流程）
- 正在进行中（等待发货）
- 不构成发布的小错误修复

**统计数据包括：**
- 统计修改的文件：`git diff --stat feat(XX-XX)..feat(YY-YY) | tail -1`
- 计数LOC：`find . -name "*.swift" -o -name "*.ts" | xargs wc -l`（或相关扩展）
- 路线图中的阶段/计划/任务计数
- 从第一阶段提交到最后阶段提交的时间线

**Git 范围格式：**
- 里程碑的第一次提交 → 里程碑的最后一次提交
- 示例：`feat(01-01)` → `feat(04-01)` 用于阶段 1-4
</guidelines>

<example>
```markdown
# Project Milestones: WeatherBar

## v1.1 Security & Polish (Shipped: 2025-12-10)

**Delivered:** Security hardening with Keychain integration and comprehensive error handling

**Phases completed:** 5-6 (3 plans total)

**Key accomplishments:**
- Migrated API key storage from plaintext to macOS Keychain
- Implemented comprehensive error handling for network failures
- Added Sentry crash reporting integration
- Fixed memory leak in auto-refresh timer

**Stats:**
- 23 files modified
- 650 lines of Swift added
- 2 phases, 3 plans, 12 tasks
- 8 days from v1.0 to v1.1

**Git range:** `feat(05-01)` → `feat(06-02)`

**What's next:** v2.0 SwiftUI redesign with widget support

---

## v1.0 MVP (Shipped: 2025-11-25)

**Delivered:** Menu bar weather app with current conditions and 3-day forecast

**Phases completed:** 1-4 (7 plans total)

**Key accomplishments:**
- Menu bar app with popover UI (AppKit)
- OpenWeather API integration with auto-refresh
- Current weather display with conditions icon
- 3-day forecast list with high/low temperatures
- Code signed and notarized for distribution

**Stats:**
- 47 files created
- 2,450 lines of Swift
- 4 phases, 7 plans, 28 tasks
- 12 days from start to ship

**Git range:** `feat(01-01)` → `feat(04-01)`

**What's next:** Security audit and hardening for v1.1
```
</example>