# 架构模板

`.planning/codebase/ARCHITECTURE.md` 模板 - 捕获概念性代码组织。

**目的：** 记录代码如何在概念层面上组织。补充 STRUCTURE.md（显示物理文件位置）。

---

## 文件模板

```markdown
# Architecture

**Analysis Date:** [YYYY-MM-DD]

## Pattern Overview

**Overall:** [Pattern name: e.g., "Monolithic CLI", "Serverless API", "Full-stack MVC"]

**Key Characteristics:**
- [Characteristic 1: e.g., "Single executable"]
- [Characteristic 2: e.g., "Stateless request handling"]
- [Characteristic 3: e.g., "Event-driven"]

## Layers

[Describe the conceptual layers and their responsibilities]

**[Layer Name]:**
- Purpose: [What this layer does]
- Contains: [Types of code: e.g., "route handlers", "business logic"]
- Depends on: [What it uses: e.g., "data layer only"]
- Used by: [What uses it: e.g., "API routes"]

**[Layer Name]:**
- Purpose: [What this layer does]
- Contains: [Types of code]
- Depends on: [What it uses]
- Used by: [What uses it]

## Data Flow

[Describe the typical request/execution lifecycle]

**[Flow Name] (e.g., "HTTP Request", "CLI Command", "Event Processing"):**

1. [Entry point: e.g., "User runs command"]
2. [Processing step: e.g., "Router matches path"]
3. [Processing step: e.g., "Controller validates input"]
4. [Processing step: e.g., "Service executes logic"]
5. [Output: e.g., "Response returned"]

**State Management:**
- [How state is handled: e.g., "Stateless - no persistent state", "Database per request", "In-memory cache"]

## Key Abstractions

[Core concepts/patterns used throughout the codebase]

**[Abstraction Name]:**
- Purpose: [What it represents]
- Examples: [e.g., "UserService, ProjectService"]
- Pattern: [e.g., "Singleton", "Factory", "Repository"]

**[Abstraction Name]:**
- Purpose: [What it represents]
- Examples: [Concrete examples]
- Pattern: [Pattern used]

## Entry Points

[Where execution begins]

**[Entry Point]:**
- Location: [Brief: e.g., "src/index.ts", "API Gateway triggers"]
- Triggers: [What invokes it: e.g., "CLI invocation", "HTTP request"]
- Responsibilities: [What it does: e.g., "Parse args, route to command"]

## Error Handling

**Strategy:** [How errors are handled: e.g., "Exception bubbling to top-level handler", "Per-route error middleware"]

**Patterns:**
- [Pattern: e.g., "try/catch at controller level"]
- [Pattern: e.g., "Error codes returned to user"]

## Cross-Cutting Concerns

[Aspects that affect multiple layers]

**Logging:**
- [Approach: e.g., "Winston logger, injected per-request"]

**Validation:**
- [Approach: e.g., "Zod schemas at API boundary"]

**Authentication:**
- [Approach: e.g., "JWT middleware on protected routes"]

---

*Architecture analysis: [date]*
*Update when major patterns change*
```

<good_examples>
```markdown
# Architecture

**Analysis Date:** 2025-01-20

## Pattern Overview

**Overall:** CLI Application with Plugin System

**Key Characteristics:**
- Single executable with subcommands
- Plugin-based extensibility
- File-based state (no database)
- Synchronous execution model

## Layers

**Command Layer:**
- Purpose: Parse user input and route to appropriate handler
- Contains: Command definitions, argument parsing, help text
- Location: `src/commands/*.ts`
- Depends on: Service layer for business logic
- Used by: CLI entry point (`src/index.ts`)

**Service Layer:**
- Purpose: Core business logic
- Contains: FileService, TemplateService, InstallService
- Location: `src/services/*.ts`
- Depends on: File system utilities, external tools
- Used by: Command handlers

**Utility Layer:**
- Purpose: Shared helpers and abstractions
- Contains: File I/O wrappers, path resolution, string formatting
- Location: `src/utils/*.ts`
- Depends on: Node.js built-ins only
- Used by: Service layer

## Data Flow

**CLI Command Execution:**

1. User runs: `gsd new-project`
2. Commander parses args and flags
3. Command handler invoked (`src/commands/new-project.ts`)
4. Handler calls service methods (`src/services/project.ts` → `create()`)
5. Service reads templates, processes files, writes output
6. Results logged to console
7. Process exits with status code

**State Management:**
- File-based: All state lives in `.planning/` directory
- No persistent in-memory state
- Each command execution is independent

## Key Abstractions

**Service:**
- Purpose: Encapsulate business logic for a domain
- Examples: `src/services/file.ts`, `src/services/template.ts`, `src/services/project.ts`
- Pattern: Singleton-like (imported as modules, not instantiated)

**Command:**
- Purpose: CLI command definition
- Examples: `src/commands/new-project.ts`, `src/commands/plan-phase.ts`
- Pattern: Commander.js command registration

**Template:**
- Purpose: Reusable document structures
- Examples: PROJECT.md, PLAN.md templates
- Pattern: Markdown files with substitution variables

## Entry Points

**CLI Entry:**
- Location: `src/index.ts`
- Triggers: User runs `gsd <command>`
- Responsibilities: Register commands, parse args, display help

**Commands:**
- Location: `src/commands/*.ts`
- Triggers: Matched command from CLI
- Responsibilities: Validate input, call services, format output

## Error Handling

**Strategy:** Throw exceptions, catch at command level, log and exit

**Patterns:**
- Services throw Error with descriptive messages
- Command handlers catch, log error to stderr, exit(1)
- Validation errors shown before execution (fail fast)

## Cross-Cutting Concerns

**Logging:**
- Console.log for normal output
- Console.error for errors
- Chalk for colored output

**Validation:**
- Zod schemas for config file parsing
- Manual validation in command handlers
- Fail fast on invalid input

**File Operations:**
- FileService abstraction over fs-extra
- All paths validated before operations
- Atomic writes (temp file + rename)

---

*Architecture analysis: 2025-01-20*
*Update when major patterns change*
```
</good_examples>

<guidelines>
**ARCHITECTURE.md 属于什么：**
- 整体架构模式（单体、微服务、分层等）
- 概念层及其关系
- 数据流/请求生命周期
- 关键抽象和模式
- 切入点
- 错误处理策略
- 横切 concerns（日志记录、身份验证、验证）

**什么不属于这里：**
- 详尽的文件列表（即 STRUCTURE.md）
- 技术选择（即STACK.md）
- 逐行代码演练（参考代码阅读）
- 具体功能的实现细节

**欢迎使用文件路径：**
包括文件路径作为抽象的具体示例。使用反引号格式：`src/services/user.ts`。这使得架构文档在规划时可用于 Claude。

**填写此模板时：**
- Read 主要入口点（索引、服务器、主）
- 通过读取导入/依赖关系来识别层
- 跟踪典型的请求/命令执行
- 注意重复出现的模式（服务、控制器、存储库）
- 保持描述的概念性，而不是机械性

**在以下情况下对于阶段规划很有用：**
- 添加新功能（它适合在层中的什么位置？）
- 重构（了解当前模式）
- 确定在哪里添加代码（哪一层处理 X？）
- 了解组件之间的依赖关系
</guidelines>