# 测试模式模板

`.planning/codebase/TESTING.md` 模板 - 捕获测试框架和模式。

**目的：** 记录测试是如何编写和运行的。添加与现有模式匹配的测试的指南。

---

## 文件模板

```markdown
# Testing Patterns

**Analysis Date:** [YYYY-MM-DD]

## Test Framework

**Runner:**
- [Framework: e.g., "Jest 29.x", "Vitest 1.x"]
- [Config: e.g., "jest.config.js in project root"]

**Assertion Library:**
- [Library: e.g., "built-in expect", "chai"]
- [Matchers: e.g., "toBe, toEqual, toThrow"]

**Run Commands:**
```bash
[e.g., "npm test" or "npm run test"] # 运行所有测试
[e.g., "npm test -- --watch"] # 观看模式
[e.g., "npm test -- path/to/file.test.ts"] # 单文件
[e.g., "npm run test:coverage"] # 覆盖率报告
```

## Test File Organization

**Location:**
- [Pattern: e.g., "*.test.ts alongside source files"]
- [Alternative: e.g., "__tests__/ directory" or "separate tests/ tree"]

**Naming:**
- [Unit tests: e.g., "module-name.test.ts"]
- [Integration: e.g., "feature-name.integration.test.ts"]
- [E2E: e.g., "user-flow.e2e.test.ts"]

**Structure:**
```
[Show actual directory pattern, e.g.:
src/
  lib/
    utils.ts
    utils.test.ts
  services/
    user-service.ts
    user-service.test.ts
]
```

## Test Structure

**Suite Organization:**
```打字稿
[Show actual pattern used, e.g.:

describe('ModuleName', () => {
  describe('functionName', () => {
    it('should handle success case', () => { expect(result).toEqual(expected); });

    it('should handle error case', () => { expect(() => runWithInvalidInput()).toThrow(); });
  });
});
]
```

**Patterns:**
- [Setup: e.g., "beforeEach for shared setup, avoid beforeAll"]
- [Teardown: e.g., "afterEach to clean up, restore mocks"]
- [Structure: e.g., "arrange/act/assert pattern required"]

## Mocking

**Framework:**
- [Tool: e.g., "Jest built-in mocking", "Vitest vi", "Sinon"]
- [Import mocking: e.g., "vi.mock() at top of file"]

**Patterns:**
```打字稿
[Show actual mocking pattern, e.g.:

// Mock external dependency
vi.mock('./external-service', () => ({ fetchData: vi.fn() }));

// Mock in test
const mockFetch = vi.mocked(fetchData);
mockFetch.mockResolvedValue({ data: 'ok' });
]
```

**What to Mock:**
- [e.g., "External APIs, file system, database"]
- [e.g., "Time/dates (use vi.useFakeTimers)"]
- [e.g., "Network calls (use mock fetch)"]

**What NOT to Mock:**
- [e.g., "Pure functions, utilities"]
- [e.g., "Internal business logic"]

## Fixtures and Factories

**Test Data:**
```打字稿
[显示创建测试数据的模式，e.g.：

// 工厂模式
函数createTestUser（覆盖？：Partial<User>）：用户{
  返回{
    id: 'test-id',
    name: 'Test User',
    email: 'test@example.com',
    ...overrides
  }；
}

// 夹具文件
// tests/fixtures/users.ts
导出常量模拟用户= [/* ... */];
]
```

**Location:**
- [e.g., "tests/fixtures/ for shared fixtures"]
- [e.g., "factory functions in test file or tests/factories/"]

## Coverage

**Requirements:**
- [Target: e.g., "80% line coverage", "no specific target"]
- [Enforcement: e.g., "CI blocks <80%", "coverage for awareness only"]

**Configuration:**
- [Tool: e.g., "built-in coverage via --coverage flag"]
- [Exclusions: e.g., "exclude *.test.ts, config files"]

**View Coverage:**
```bash
[e.g., "npm run test:coverage"]
[e.g., "open coverage/index.html"]
```

## Test Types

**Unit Tests:**
- [Scope: e.g., "test single function/class in isolation"]
- [Mocking: e.g., "mock all external dependencies"]
- [Speed: e.g., "must run in <1s per test"]

**Integration Tests:**
- [Scope: e.g., "test multiple modules together"]
- [Mocking: e.g., "mock external services, use real internal modules"]
- [Setup: e.g., "use test database, seed data"]

**E2E Tests:**
- [Framework: e.g., "Playwright for E2E"]
- [Scope: e.g., "test full user flows"]
- [Location: e.g., "e2e/ directory separate from unit tests"]

## Common Patterns

**Async Testing:**
```打字稿
[Show pattern, e.g.:

it('should handle async operation', async () => { await expect(runTask()).resolves.toEqual(expected); });
]
```

**Error Testing:**
```打字稿
[Show pattern, e.g.:

it('should throw on invalid input', () => { expect(() => parseInput(null)).toThrow(); });

// Async error
it('should reject on failure', async () => { await expect(runTask()).rejects.toThrow('failure'); });
]
```

**Snapshot Testing:**
- [Usage: e.g., "for React components only" or "not used"]
- [Location: e.g., "__snapshots__/ directory"]

---

*Testing analysis: [date]*
*Update when test patterns change*
```

<good_examples>
```markdown
# Testing Patterns

**Analysis Date:** 2025-01-20

## Test Framework

**Runner:**
- Vitest 1.0.4
- Config: vitest.config.ts in project root

**Assertion Library:**
- Vitest built-in expect
- Matchers: toBe, toEqual, toThrow, toMatchObject

**Run Commands:**
```bash
npm test # 运行所有测试
npm测试 -- --watch # 观看模式
npm 测试 -- path/to/file.test.ts # 单文件
npm run test:coverage # 覆盖率报告
```

## Test File Organization

**Location:**
- *.test.ts alongside source files
- No separate tests/ directory

**Naming:**
- unit-name.test.ts for all tests
- No distinction between unit/integration in filename

**Structure:**
```
源代码/
  库/
    parser.ts
    parser.test.ts
  服务/
    install-service.ts
    install-service.test.ts
  垃圾箱/
    install.ts
    （无测试 - 通过 CLI 进行集成测试）
```

## Test Structure

**Suite Organization:**
```打字稿
从 'vitest' 导入 { describe, it, expect, beforeEach, afterEach, vi }；

描述('模块名称', () => {
  描述('函数名', () => {
    beforeEach(() => {
      // reset state
    });

    it('应该处理有效的输入', () => {
      // arrange
      const input = createTestInput();

      // act
      const result = functionName(input);

      // assert
      expect(result).toEqual(expectedOutput);
    });

    it('应该抛出无效输入', () => {
      expect(() => functionName(null)).toThrow('Invalid input');
    });
  });
});
```

**Patterns:**
- Use beforeEach for per-test setup, avoid beforeAll
- Use afterEach to restore mocks: vi.restoreAllMocks()
- Explicit arrange/act/assert comments in complex tests
- One assertion focus per test (but multiple expects OK)

## Mocking

**Framework:**
- Vitest built-in mocking (vi)
- Module mocking via vi.mock() at top of test file

**Patterns:**
```打字稿
从 'vitest' 导入 { vi }；
从'./external'导入{ externalFunction }；

// 模拟模块
vi.mock('./外部', () => ({
  externalFunction: vi.fn()
}));

描述（'测试套件'，（）=> {
  it('模拟函数', () => {
    const mockFn = vi.mocked(externalFunction);
    mockFn.mockReturnValue('mocked result');

    // test code using mocked function

    expect(mockFn).toHaveBeenCalledWith('expected arg');
  });
});
```

**What to Mock:**
- File system operations (fs-extra)
- Child process execution (child_process.exec)
- External API calls
- Environment variables (process.env)

**What NOT to Mock:**
- Internal pure functions
- Simple utilities (string manipulation, array helpers)
- TypeScript types

## Fixtures and Factories

**Test Data:**
```打字稿
// 测试文件中的工厂函数
函数createTestConfig（覆盖？：Partial<Config>）：配置{
  返回{
    targetDir: '/tmp/test',
    global: false,
    ...overrides
  }；
}

// 在tests/fixtures/中共享fixtures
// tests/fixtures/sample-command.md
导出常量样本命令 = `---
description: Test command
---
Content here`;
```

**Location:**
- Factory functions: define in test file near usage
- Shared fixtures: tests/fixtures/ (for multi-file test data)
- Mock data: inline in test when simple, factory when complex

## Coverage

**Requirements:**
- No enforced coverage target
- Coverage tracked for awareness
- Focus on critical paths (parsers, service logic)

**Configuration:**
- Vitest coverage via c8 (built-in)
- Excludes: *.test.ts, bin/install.ts, config files

**View Coverage:**
```bash
npm运行测试：覆盖率
打开coverage/index.html
```

## Test Types

**Unit Tests:**
- Test single function in isolation
- Mock all external dependencies (fs, child_process)
- Fast: each test <100ms
- Examples: parser.test.ts, validator.test.ts

**Integration Tests:**
- Test multiple modules together
- Mock only external boundaries (file system, process)
- Examples: install-service.test.ts (tests service + parser)

**E2E Tests:**
- Not currently used
- CLI integration tested manually

## Common Patterns

**Async Testing:**
```打字稿
it('应该处理异步操作', async () => {
  const result = await asyncFunction();
  expect(result).toBe('expected');
});
```

**Error Testing:**
```打字稿
it('应该抛出无效输入', () => {
  expect(() => parse(null)).toThrow('Cannot parse null');
});

// 异步错误
it('应该拒绝找不到文件', async () => {
  await expect(readConfig('invalid.txt')).rejects.toThrow('ENOENT');
});
```

**File System Mocking:**
```打字稿
从 'vitest' 导入 { vi }；
从“fs-extra”导入*作为fs；

vi.mock('fs-extra');

it('模拟文件系统', () => {
  vi.mocked(fs.readFile).mockResolvedValue('file content');
  // test code
});
```

**Snapshot Testing:**
- Not used in this codebase
- Prefer explicit assertions for clarity

---

*Testing analysis: 2025-01-20*
*Update when test patterns change*
```
</good_examples>

<guidelines>
**TESTING.md 属于什么：**
- 测试框架和运行器配置
- 测试文件位置和命名模式
- 测试结构（describe/it、beforeEach 模式）
- 模拟方法和示例
- 固定装置/工厂模式
- 覆盖范围要求
- 如何运行测试（命令）
- 实际代码中的常见测试模式

**什么不属于这里：**
- 具体测试用例（以实际测试文件为准）
- 技术选择（即STACK.md）
- CI/CD 设置（即部署文档）

**填写此模板时：**
- 检查 package.json 脚本的测试命令
- 查找测试配置文件（jest.config.js、vitest.config.ts）
- Read 3-5个现有测试文件来识别模式
- 在tests/或test-utils/中查找测试实用程序
- 检查覆盖配置
- 记录实际使用的模式，而不是理想的模式

**在以下情况下对于阶段规划很有用：**- 添加新功能（编写匹配测试）
- 重构（维护测试模式）
- 修复错误（添加回归测试）
- 了解验证方法
- 建立测试基础设施

**分析方法：**
- 检查 package.json 的测试框架和脚本
- Read 测试覆盖范围、设置的配置文件
- 检查测试文件组织（并置与单独）
- 查看 5 个测试文件的模式（模拟、结构、断言）
- 寻找测试设施、固定装置、工厂
- 记下任何测试类型（单元、集成、e2e）
- 记录运行测试的命令
</guidelines>
