<purpose>
显示完整的 GSD 命令参考。只输出参考内容本身；不要添加项目分析、git 状态、下一步建议或任何额外评论。
</purpose>

<reference>
# GSD 命令参考

**GSD**（Get Shit Done）会创建适合使用 Claude Code 进行单人代理式开发的分层项目计划。

## 快速开始

1. `/gsd:new-project` - Initialize project (includes research, requirements, roadmap)
2. `/gsd:plan-phase 1` - Create detailed plan for first phase
3. `/gsd:execute-phase 1` - Execute the phase

## 保持更新

GSD 演进很快，建议定期更新：

```bash
npx get-shit-done-synexim@latest
```

## 核心工作流

```
/gsd:new-project → /gsd:plan-phase → /gsd:execute-phase → repeat
```

### 项目初始化

**`/gsd:init`**
将 GSD Synexim 引导接入当前仓库。

- Creates `.planning/config.json` if missing
- Creates or patches `AGENTS.md` with Chinese-first Synexim rules
- Enables adaptive project scale defaults for micro / standard / large work
- Adds the front-end prototype gate for Gemini AI Studio driven flows

Usage: `/gsd:init`

**`/gsd:new-project`**
通过统一流程初始化新项目。

一条命令即可让你从想法进入可规划状态：
- Deep questioning to understand what you're building
- Optional domain research (spawns 4 parallel researcher agents)
- Requirements definition with v1/v2/out-of-scope scoping
- Roadmap creation with phase breakdown and success criteria

会创建全部 `.planning/` 产物：
- `PROJECT.md` — vision and requirements
- `config.json` — workflow mode (interactive/yolo)
- `research/` — domain research (if selected)
- `REQUIREMENTS.md` — scoped requirements with REQ-IDs
- `ROADMAP.md` — phases mapped to requirements
- `STATE.md` — project memory

Usage: `/gsd:new-project`

**`/gsd:map-codebase`**
为存量项目映射现有代码库。

- Analyzes codebase with parallel Explore agents
- Creates `.planning/codebase/` with 7 focused documents
- Covers stack, architecture, structure, conventions, testing, integrations, concerns
- Use before `/gsd:new-project` on existing codebases

Usage: `/gsd:map-codebase`

### 阶段规划

**`/gsd:discuss-phase <number>`**
在规划前帮助你明确某个阶段的愿景。

- Captures how you imagine this phase working
- Creates CONTEXT.md with your vision, essentials, and boundaries
- Use when you have ideas about how something should look/feel

Usage: `/gsd:discuss-phase 2`

**`/gsd:research-phase <number>`**
为小众/复杂领域执行全面生态研究。

- Discovers standard stack, architecture patterns, pitfalls
- Creates RESEARCH.md with "how experts build this" knowledge
- Use for 3D, games, audio, shaders, ML, and other specialized domains
- Goes beyond "which library" to ecosystem knowledge

Usage: `/gsd:research-phase 3`

**`/gsd:list-phase-assumptions <number>`**
在 Claude 开始前查看它准备怎么做。

- Shows Claude's intended approach for a phase
- Lets you course-correct if Claude misunderstood your vision
- No files created - conversational output only

Usage: `/gsd:list-phase-assumptions 3`

**`/gsd:plan-phase <number>`**
为特定阶段创建详细执行计划。

- Generates `.planning/phases/XX-phase-name/XX-YY-PLAN.md`
- Breaks phase into concrete, actionable tasks
- Includes verification criteria and success measures
- Multiple plans per phase supported (XX-01, XX-02, etc.)

Usage: `/gsd:plan-phase 1`
Result: Creates `.planning/phases/01-foundation/01-01-PLAN.md`

**PRD Express Path:** Pass `--prd path/to/requirements.md` to skip discuss-phase entirely. Your PRD becomes locked decisions in CONTEXT.md. Useful when you already have clear acceptance criteria.

### 执行

**`/gsd:execute-phase <phase-number>`**
执行某个阶段中的全部计划。

- Groups plans by wave (from frontmatter), executes waves sequentially
- Plans within each wave run in parallel via Task tool
- Verifies phase goal after all plans complete
- Updates REQUIREMENTS.md, ROADMAP.md, STATE.md

Usage: `/gsd:execute-phase 5`

### 快速模式

**`/gsd:quick`**
执行小型临时任务，同时保留 GSD 保障并跳过可选代理。

Quick mode uses the same system with a shorter path:
- Spawns planner + executor (skips researcher, checker, verifier)
- Quick tasks live in `.planning/quick/` separate from planned phases
- Updates STATE.md tracking (not ROADMAP.md)

Use when you know exactly what to do and the task is small enough to not need research or verification.

Usage: `/gsd:quick`
Result: Creates `.planning/quick/NNN-slug/PLAN.md`, `.planning/quick/NNN-slug/SUMMARY.md`

### 路线图管理

**`/gsd:add-phase <description>`**
在当前里程碑末尾新增阶段。

- Appends to ROADMAP.md
- Uses next sequential number
- Updates phase directory structure

Usage: `/gsd:add-phase "Add admin dashboard"`

**`/gsd:insert-phase <after> <description>`**
在现有阶段之间插入紧急的小数阶段。

- Creates intermediate phase (e.g., 7.1 between 7 and 8)
- Useful for discovered work that must happen mid-milestone
- Maintains phase ordering

Usage: `/gsd:insert-phase 7 "Fix critical auth bug"`
Result: Creates Phase 7.1

**`/gsd:remove-phase <number>`**
移除未来阶段，并对后续阶段重新编号。

- Deletes phase directory and all references
- Renumbers all subsequent phases to close the gap
- Only works on future (unstarted) phases
- Git commit preserves historical record

Usage: `/gsd:remove-phase 17`
Result: Phase 17 deleted, phases 18-20 become 17-19

### 里程碑管理

**`/gsd:new-milestone <name>`**
通过统一流程启动新的里程碑。

- Deep questioning to understand what you're building next
- Optional domain research (spawns 4 parallel researcher agents)
- Requirements definition with scoping
- Roadmap creation with phase breakdown

Mirrors `/gsd:new-project` flow for brownfield projects (existing PROJECT.md).

Usage: `/gsd:new-milestone "v2.0 Features"`

**`/gsd:complete-milestone <version>`**
归档已完成里程碑，并为下一个版本做准备。

- Creates MILESTONES.md entry with stats
- Archives full details to milestones/ directory
- Creates git tag for the release
- Prepares workspace for next version

Usage: `/gsd:complete-milestone 1.0.0`

### 进度跟踪

**`/gsd:progress`**
检查项目状态，并智能路由到下一步动作。

- Shows visual progress bar and completion percentage
- Summarizes recent work from SUMMARY files
- Displays current position and what's next
- Lists key decisions and open issues
- Offers to execute next plan or create it if missing
- Detects 100% milestone completion

Usage: `/gsd:progress`

### 会话管理

**`/gsd:resume-work`**
恢复上一次会话的工作，并完整还原上下文。

- Reads STATE.md for project context
- Shows current position and recent progress
- Offers next actions based on project state

Usage: `/gsd:resume-work`

**`/gsd:pause-work`**
在阶段中途暂停时创建上下文交接。

- Creates .continue-here file with current state
- Updates STATE.md session continuity section
- Captures in-progress work context

Usage: `/gsd:pause-work`

### 调试

**`/gsd:debug [issue description]`**
通过持久状态进行系统化调试，支持跨上下文重置继续。

- Gathers symptoms through adaptive questioning
- Creates `.planning/debug/[slug].md` to track investigation
- Investigates using scientific method (evidence → hypothesis → test)
- Survives `/clear` — run `/gsd:debug` with no args to resume
- Archives resolved issues to `.planning/debug/resolved/`

Usage: `/gsd:debug "login button doesn't work"`
Usage: `/gsd:debug` (resume active session)

### Todo 管理

**`/gsd:add-todo [description]`**
从当前对话中捕获想法或任务并记录为 todo。

- Extracts context from conversation (or uses provided description)
- Creates structured todo file in `.planning/todos/pending/`
- Infers area from file paths for grouping
- Checks for duplicates before creating
- Updates STATE.md todo count

Usage: `/gsd:add-todo` (infers from conversation)
Usage: `/gsd:add-todo Add auth token refresh`

**`/gsd:check-todos [area]`**
列出待处理 todo，并选择其中一项开始处理。

- Lists all pending todos with title, area, age
- Optional area filter (e.g., `/gsd:check-todos api`)
- Loads full context for selected todo
- Routes to appropriate action (work now, add to phase, brainstorm)
- Moves todo to done/ when work begins

Usage: `/gsd:check-todos`
Usage: `/gsd:check-todos api`

### 用户验收测试

**`/gsd:verify-work [phase]`**
通过对话式 UAT 验证已构建功能。

- Extracts testable deliverables from SUMMARY.md files
- Presents tests one at a time (yes/no responses)
- Automatically diagnoses failures and creates fix plans
- Ready for re-execution if issues found

Usage: `/gsd:verify-work 3`

### 里程碑审计

**`/gsd:audit-milestone [version]`**
根据原始目标审计里程碑完成情况。

- Reads all phase VERIFICATION.md files
- Checks requirements coverage
- Spawns integration checker for cross-phase wiring
- Creates MILESTONE-AUDIT.md with gaps and tech debt

Usage: `/gsd:audit-milestone`

**`/gsd:plan-milestone-gaps`**
为审计发现的缺口创建修复阶段。

- Reads MILESTONE-AUDIT.md and groups gaps into phases
- Prioritizes by requirement priority (must/should/nice)
- Adds gap closure phases to ROADMAP.md
- Ready for `/gsd:plan-phase` on new phases

Usage: `/gsd:plan-milestone-gaps`

### 配置

**`/gsd:settings`**
以交互方式配置工作流开关与模型档位。

- Toggle researcher, plan checker, verifier agents
- Select model profile (quality/balanced/budget) with GPT-5.4 effort policy
- Updates `.planning/config.json`

Usage: `/gsd:settings`

**`/gsd:set-profile <profile>`**
快速切换 GSD 代理的模型档位。

- `quality` — OpenAI GPT-5.4 with `xhigh` for roadmap/phase planning, `high` for execution
- `balanced` — OpenAI GPT-5.4 with `high` for planning and execution (default)
- `budget` — OpenAI GPT-5.4 with `high`, but fewer auxiliary checks/research

**前端规则：** 项目初始化阶段不得使用 GPT-5.4 直接做前端设计；若要做前端实现，必须先确认 Gemini AI Studio MVP 原型已完整覆盖当前里程碑与一级功能。

Usage: `/gsd:set-profile budget`

### 实用命令

**`/gsd:cleanup`**
归档已完成里程碑累计下来的阶段目录。

- Identifies phases from completed milestones still in `.planning/phases/`
- Shows dry-run summary before moving anything
- Moves phase dirs to `.planning/milestones/v{X.Y}-phases/`
- Use after multiple milestones to reduce `.planning/phases/` clutter

Usage: `/gsd:cleanup`

**`/gsd:help`**
显示这份命令参考。

**`/gsd:patch-agents`**
注入或刷新 `AGENTS.md` 中的 GSD Synexim 托管区块。

- Preserves user-authored project rules outside the managed block
- Reapplies Chinese-first, adaptive-scale, and front-end prototype requirements
- Safe to run after manual AGENTS edits or after updating GSD

Usage: `/gsd:patch-agents`

**`/gsd:update`**
将 GSD 更新到最新版本，并预览更新日志。

- Shows installed vs latest version comparison
- Displays changelog entries for versions you've missed
- Highlights breaking changes
- Confirms before running install
- Better than raw `npx get-shit-done-synexim`

Usage: `/gsd:update`

**`/gsd:join-discord`**
加入 GSD Discord 社区。

- Get help, share what you're building, stay updated
- Connect with other GSD users

Usage: `/gsd:join-discord`

## 文件与结构

```
.planning/
├── PROJECT.md            # Project vision
├── ROADMAP.md            # Current phase breakdown
├── STATE.md              # Project memory & context
├── RETROSPECTIVE.md      # Living retrospective (updated per milestone)
├── config.json           # Workflow mode & gates
├── todos/                # Captured ideas and tasks
│   ├── pending/          # Todos waiting to be worked on
│   └── done/             # Completed todos
├── debug/                # Active debug sessions
│   └── resolved/         # Archived resolved issues
├── milestones/
│   ├── v1.0-ROADMAP.md       # Archived roadmap snapshot
│   ├── v1.0-REQUIREMENTS.md  # Archived requirements
│   └── v1.0-phases/          # Archived phase dirs (via /gsd:cleanup or --archive-phases)
│       ├── 01-foundation/
│       └── 02-core-features/
├── codebase/             # Codebase map (brownfield projects)
│   ├── STACK.md          # Languages, frameworks, dependencies
│   ├── ARCHITECTURE.md   # Patterns, layers, data flow
│   ├── STRUCTURE.md      # Directory layout, key files
│   ├── CONVENTIONS.md    # Coding standards, naming
│   ├── TESTING.md        # Test setup, patterns
│   ├── INTEGRATIONS.md   # External services, APIs
│   └── CONCERNS.md       # Tech debt, known issues
└── phases/
    ├── 01-foundation/
    │   ├── 01-01-PLAN.md
    │   └── 01-01-SUMMARY.md
    └── 02-core-features/
        ├── 02-01-PLAN.md
        └── 02-01-SUMMARY.md
```

## 工作流模式

在 `/gsd:new-project` 期间设置：

**交互模式**

- Confirms each major decision
- Pauses at checkpoints for approval
- More guidance throughout

**YOLO 模式**

- Auto-approves most decisions
- Executes plans without confirmation
- Only stops for critical checkpoints

随时可通过编辑 `.planning/config.json` 修改

## 规划配置

Configure how planning artifacts are managed in `.planning/config.json`:

**`planning.commit_docs`** (default: `true`)
- `true`: Planning artifacts committed to git (standard workflow)
- `false`: Planning artifacts kept local-only, not committed

When `commit_docs: false`:
- Add `.planning/` to your `.gitignore`
- Useful for OSS contributions, client projects, or keeping planning private
- All planning files still work normally, just not tracked in git

**`planning.search_gitignored`** (default: `false`)
- `true`: Add `--no-ignore` to broad ripgrep searches
- Only needed when `.planning/` is gitignored and you want project-wide searches to include it

Example config:
```json
{
  "planning": {
    "commit_docs": false,
    "search_gitignored": true
  }
}
```

## 常见工作流

**启动新项目：**

```
/gsd:new-project        # Unified flow: questioning → research → requirements → roadmap
/clear
/gsd:plan-phase 1       # Create plans for first phase
/clear
/gsd:execute-phase 1    # Execute all plans in phase
```

**中断后恢复工作：**

```
/gsd:progress  # See where you left off and continue
```

**在里程碑中途插入紧急工作：**

```
/gsd:insert-phase 5 "Critical security fix"
/gsd:plan-phase 5.1
/gsd:execute-phase 5.1
```

**完成一个里程碑：**

```
/gsd:complete-milestone 1.0.0
/clear
/gsd:new-milestone  # Start next milestone (questioning → research → requirements → roadmap)
```

**在工作中记录想法：**

```
/gsd:add-todo                    # Capture from conversation context
/gsd:add-todo Fix modal z-index  # Capture with explicit description
/gsd:check-todos                 # Review and work on todos
/gsd:check-todos api             # Filter by area
```

**调试问题：**

```
/gsd:debug "form submission fails silently"  # Start debug session
# ... investigation happens, context fills up ...
/clear
/gsd:debug                                    # Resume from where you left off
```

## 获取帮助

- 阅读 `.planning/PROJECT.md` 了解项目愿景
- 阅读 `.planning/STATE.md` 了解当前上下文
- 查看 `.planning/ROADMAP.md` 了解阶段状态
- 运行 `/gsd:progress` 查看当前推进到哪里
</reference>
