# 技术栈模板

`.planning/codebase/STACK.md` 模板 - 掌握技术基础。

**目的：** 记录运行此代码库的技术。重点关注“运行代码时执行的内容”。

---

## 文件模板

```markdown
# Technology Stack

**Analysis Date:** [YYYY-MM-DD]

## Languages

**Primary:**
- [Language] [Version] - [Where used: e.g., "all application code"]

**Secondary:**
- [Language] [Version] - [Where used: e.g., "build scripts, tooling"]

## Runtime

**Environment:**
- [Runtime] [Version] - [e.g., "Node.js 20.x"]
- [Additional requirements if any]

**Package Manager:**
- [Manager] [Version] - [e.g., "npm 10.x"]
- Lockfile: [e.g., "package-lock.json present"]

## Frameworks

**Core:**
- [Framework] [Version] - [Purpose: e.g., "web server", "UI framework"]

**Testing:**
- [Framework] [Version] - [e.g., "Jest for unit tests"]
- [Framework] [Version] - [e.g., "Playwright for E2E"]

**Build/Dev:**
- [Tool] [Version] - [e.g., "Vite for bundling"]
- [Tool] [Version] - [e.g., "TypeScript compiler"]

## Key Dependencies

[Only include dependencies critical to understanding the stack - limit to 5-10 most important]

**Critical:**
- [Package] [Version] - [Why it matters: e.g., "authentication", "database access"]
- [Package] [Version] - [Why it matters]

**Infrastructure:**
- [Package] [Version] - [e.g., "Express for HTTP routing"]
- [Package] [Version] - [e.g., "PostgreSQL client"]

## Configuration

**Environment:**
- [How configured: e.g., ".env files", "environment variables"]
- [Key configs: e.g., "DATABASE_URL, API_KEY required"]

**Build:**
- [Build config files: e.g., "vite.config.ts, tsconfig.json"]

## Platform Requirements

**Development:**
- [OS requirements or "any platform"]
- [Additional tooling: e.g., "Docker for local DB"]

**Production:**
- [Deployment target: e.g., "Vercel", "AWS Lambda", "Docker container"]
- [Version requirements]

---

*Stack analysis: [date]*
*Update after major dependency changes*
```

<good_examples>
```markdown
# Technology Stack

**Analysis Date:** 2025-01-20

## Languages

**Primary:**
- TypeScript 5.3 - All application code

**Secondary:**
- JavaScript - Build scripts, config files

## Runtime

**Environment:**
- Node.js 20.x (LTS)
- No browser runtime (CLI tool only)

**Package Manager:**
- npm 10.x
- Lockfile: `package-lock.json` present

## Frameworks

**Core:**
- None (vanilla Node.js CLI)

**Testing:**
- Vitest 1.0 - Unit tests
- tsx - TypeScript execution without build step

**Build/Dev:**
- TypeScript 5.3 - Compilation to JavaScript
- esbuild - Used by Vitest for fast transforms

## Key Dependencies

**Critical:**
- commander 11.x - CLI argument parsing and command structure
- chalk 5.x - Terminal output styling
- fs-extra 11.x - Extended file system operations

**Infrastructure:**
- Node.js built-ins - fs, path, child_process for file operations

## Configuration

**Environment:**
- No environment variables required
- Configuration via CLI flags only

**Build:**
- `tsconfig.json` - TypeScript compiler options
- `vitest.config.ts` - Test runner configuration

## Platform Requirements

**Development:**
- macOS/Linux/Windows (any platform with Node.js)
- No external dependencies

**Production:**
- Distributed as npm package
- Installed globally via npm install -g
- Runs on user's Node.js installation

---

*Stack analysis: 2025-01-20*
*Update after major dependency changes*
```
</good_examples>

<guidelines>
**STACK.md 属于什么：**
- 语言和版本
- 运行时要求（Node、Bun、Deno、浏览器）
- 包管理器和锁定文件
- 框架选择
- 关键依赖项（限制为 5-10 个最重要的依赖项）
- 构建工具
- 平台/部署要求

**什么不属于这里：**
- 文件结构（即STRUCTURE.md）
- 架构模式（即ARCHITECTURE.md）
- package.json 中的每个依赖项（仅关键依赖项）
- 实现细节（参考代码）

**填写此模板时：**
- 检查 package.json 的依赖关系
- 注意 .nvmrc 或 package.json 引擎的运行时版本
- 仅包含影响理解的依赖项（不是每个实用程序）
- 仅在版本重要时指定版本（重大更改、兼容性）

**在以下情况下对于阶段规划很有用：**
- 添加新的依赖项（检查兼容性）
- 升级框架（知道正在使用什么）
- 选择实施方法（必须与现有堆栈一起使用）
- 了解构建要求
</guidelines>