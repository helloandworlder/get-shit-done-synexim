# 编码约定模板

`.planning/codebase/CONVENTIONS.md` 模板 - 捕获编码风格和模式。

**目的：** 记录如何在此代码库中编写代码。 Claude 匹配现有风格的规范性指南。

---

## 文件模板

```markdown
# Coding Conventions

**Analysis Date:** [YYYY-MM-DD]

## Naming Patterns

**Files:**
- [Pattern: e.g., "kebab-case for all files"]
- [Test files: e.g., "*.test.ts alongside source"]
- [Components: e.g., "PascalCase.tsx for React components"]

**Functions:**
- [Pattern: e.g., "camelCase for all functions"]
- [Async: e.g., "no special prefix for async functions"]
- [Handlers: e.g., "handleEventName for event handlers"]

**Variables:**
- [Pattern: e.g., "camelCase for variables"]
- [Constants: e.g., "UPPER_SNAKE_CASE for constants"]
- [Private: e.g., "_prefix for private members" or "no prefix"]

**Types:**
- [Interfaces: e.g., "PascalCase, no I prefix"]
- [Types: e.g., "PascalCase for type aliases"]
- [Enums: e.g., "PascalCase for enum name, UPPER_CASE for values"]

## Code Style

**Formatting:**
- [Tool: e.g., "Prettier with config in .prettierrc"]
- [Line length: e.g., "100 characters max"]
- [Quotes: e.g., "single quotes for strings"]
- [Semicolons: e.g., "required" or "omitted"]

**Linting:**
- [Tool: e.g., "ESLint with eslint.config.js"]
- [Rules: e.g., "extends airbnb-base, no console in production"]
- [Run: e.g., "npm run lint"]

## Import Organization

**Order:**
1. [e.g., "External packages (react, express, etc.)"]
2. [e.g., "Internal modules (@/lib, @/components)"]
3. [e.g., "Relative imports (., ..)"]
4. [e.g., "Type imports (import type {})"]

**Grouping:**
- [Blank lines: e.g., "blank line between groups"]
- [Sorting: e.g., "alphabetical within each group"]

**Path Aliases:**
- [Aliases used: e.g., "@/ for src/, @components/ for src/components/"]

## Error Handling

**Patterns:**
- [Strategy: e.g., "throw errors, catch at boundaries"]
- [Custom errors: e.g., "extend Error class, named *Error"]
- [Async: e.g., "use try/catch, no .catch() chains"]

**Error Types:**
- [When to throw: e.g., "invalid input, missing dependencies"]
- [When to return: e.g., "expected failures return Result<T, E>"]
- [Logging: e.g., "log error with context before throwing"]

## Logging

**Framework:**
- [Tool: e.g., "console.log, pino, winston"]
- [Levels: e.g., "debug, info, warn, error"]

**Patterns:**
- [Format: e.g., "structured logging with context object"]
- [When: e.g., "log state transitions, external calls"]
- [Where: e.g., "log at service boundaries, not in utils"]

## Comments

**When to Comment:**
- [e.g., "explain why, not what"]
- [e.g., "document business logic, algorithms, edge cases"]
- [e.g., "avoid obvious comments like // increment counter"]

**JSDoc/TSDoc:**
- [Usage: e.g., "required for public APIs, optional for internal"]
- [Format: e.g., "use @param, @returns, @throws tags"]

**TODO Comments:**
- [Pattern: e.g., "// TODO(username): description"]
- [Tracking: e.g., "link to issue number if available"]

## Function Design

**Size:**
- [e.g., "keep under 50 lines, extract helpers"]

**Parameters:**
- [e.g., "max 3 parameters, use object for more"]
- [e.g., "destructure objects in parameter list"]

**Return Values:**
- [e.g., "explicit returns, no implicit undefined"]
- [e.g., "return early for guard clauses"]

## Module Design

**Exports:**
- [e.g., "named exports preferred, default exports for React components"]
- [e.g., "export from index.ts for public API"]

**Barrel Files:**
- [e.g., "use index.ts to re-export public API"]
- [e.g., "avoid circular dependencies"]

---

*Convention analysis: [date]*
*Update when patterns change*
```

<good_examples>
```markdown
# Coding Conventions

**Analysis Date:** 2025-01-20

## Naming Patterns

**Files:**
- kebab-case for all files (command-handler.ts, user-service.ts)
- *.test.ts alongside source files
- index.ts for barrel exports

**Functions:**
- camelCase for all functions
- No special prefix for async functions
- handleEventName for event handlers (handleClick, handleSubmit)

**Variables:**
- camelCase for variables
- UPPER_SNAKE_CASE for constants (MAX_RETRIES, API_BASE_URL)
- No underscore prefix (no private marker in TS)

**Types:**
- PascalCase for interfaces, no I prefix (User, not IUser)
- PascalCase for type aliases (UserConfig, ResponseData)
- PascalCase for enum names, UPPER_CASE for values (Status.PENDING)

## Code Style

**Formatting:**
- Prettier with .prettierrc
- 100 character line length
- Single quotes for strings
- Semicolons required
- 2 space indentation

**Linting:**
- ESLint with eslint.config.js
- Extends @typescript-eslint/recommended
- No console.log in production code (use logger)
- Run: npm run lint

## Import Organization

**Order:**
1. External packages (react, express, commander)
2. Internal modules (@/lib, @/services)
3. Relative imports (./utils, ../types)
4. Type imports (import type { User })

**Grouping:**
- Blank line between groups
- Alphabetical within each group
- Type imports last within each group

**Path Aliases:**
- @/ maps to src/
- No other aliases defined

## Error Handling

**Patterns:**
- Throw errors, catch at boundaries (route handlers, main functions)
- Extend Error class for custom errors (ValidationError, NotFoundError)
- Async functions use try/catch, no .catch() chains

**Error Types:**
- Throw on invalid input, missing dependencies, invariant violations
- Log error with context before throwing: logger.error({ err, userId }, 'Failed to process')
- Include cause in error message: new Error('Failed to X', { cause: originalError })

## Logging

**Framework:**
- pino logger instance exported from lib/logger.ts
- Levels: debug, info, warn, error (no trace)

**Patterns:**
- Structured logging with context: logger.info({ userId, action }, 'User action')
- Log at service boundaries, not in utility functions
- Log state transitions, external API calls, errors
- No console.log in committed code

## Comments

**When to Comment:**
- Explain why, not what: // Retry 3 times because API has transient failures
- Document business rules: // Users must verify email within 24 hours
- Explain non-obvious algorithms or workarounds
- Avoid obvious comments: // set count to 0

**JSDoc/TSDoc:**
- Required for public API functions
- Optional for internal functions if signature is self-explanatory
- Use @param, @returns, @throws tags

**TODO Comments:**
- Format: // TODO: description (no username, using git blame)
- Link to issue if exists: // TODO: Fix race condition (issue #123)

## Function Design

**Size:**
- Keep under 50 lines
- Extract helpers for complex logic
- One level of abstraction per function

**Parameters:**
- Max 3 parameters
- Use options object for 4+ parameters: function create(options: CreateOptions)
- Destructure in parameter list: function process({ id, name }: ProcessParams)

**Return Values:**
- Explicit return statements
- Return early for guard clauses
- Use Result<T, E> type for expected failures

## Module Design

**Exports:**
- Named exports preferred
- Default exports only for React components
- Export public API from index.ts barrel files

**Barrel Files:**
- index.ts re-exports public API
- Keep internal helpers private (don't export from index)
- Avoid circular dependencies (import from specific files if needed)

---

*Convention analysis: 2025-01-20*
*Update when patterns change*
```
</good_examples>

<guidelines>
**CONVENTIONS.md 属于什么：**
- 在代码库中观察到的命名模式
- 格式化规则（Prettier 配置、linting 规则）
- 导入组织模式
- 错误处理策略
- 记录方法
- 评论约定
- 功能和模块设计模式

**什么不属于这里：**
- 架构决策（即 ARCHITECTURE.md）
- 技术选择（即STACK.md）
- 测试模式（即TESTING.md）
- 文件组织（即STRUCTURE.md）

**填写此模板时：**
- 检查 .prettierrc、.eslintrc 或类似的配置文件
- 检查 5-10 个有代表性的源文件中的模式
- 寻找一致性：如果 80% 以上遵循某种模式，请将其记录下来
- 具有规定性：“使用 X”而不是“有时使用 Y”
- 注意偏差：“旧代码使用 Y，新代码应使用 X”
- 总共保持在约 150 行以内

**在以下情况下对于阶段规划很有用：**
- 编写新代码（匹配现有风格）
- 添加功能（遵循命名模式）
- 重构（应用一致的约定）
- 代码审查（对照记录的模式进行检查）
- 入职（了解风格期望）

**分析方法：**
- 扫描 src/ 目录中的文件命名模式
- 检查 package.json 脚本中的 lint/format 命令
- Read 5-10个文件识别函数命名、错误处理
- 查找配置文件（.prettierrc、eslint.config.js）
- 注意导入、注释、函数签名中的模式
</guidelines>