---
phase: XX-name
plan: YY
subsystem: [primary category]
tags: [searchable tech]
requires:
  - phase: [prior phase]
    provides: [what that phase built]
provides:
  - [bullet list of what was built/delivered]
affects: [list of phase names or keywords]
tech-stack:
  added: [libraries/tools]
  patterns: [architectural/code patterns]
key-files:
  created: [important files created]
  modified: [important files modified]
key-decisions:
  - "Decision 1"
patterns-established:
  - "Pattern 1: description"
duration: Xmin
completed: YYYY-MM-DD
---

# [X] 阶段：[Name] 摘要（复杂）

**[用一句中文说明本次交付了什么，避免空泛表述]**

## 性能
- **持续时间：** [time]
- **任务：** [count completed]
- **修改文件：** [count]

## 成就
- [关键成果 1]
- [关键成果 2]

## 任务提交
1. **任务1：[task name]** - `hash`
2. **任务2：[task name]** - `hash`
3. **任务3：[task name]** - `hash`

## 创建/修改的文件
- `path/to/file.ts` - 它的作用
- `path/to/another.ts` - 它的作用

## 做出的决策
[关键决策及简短理由]

## 与计划的偏差（自动修复）
[按 GSD 偏差规则记录自动修复详情]

## 进度卡
```text
┌─ 本次更新 ───────────────────────────────┐
│ 文档: {phase}-{plan}-SUMMARY.md          │
│ 模块: ...                                │
│ 做了什么: ...                            │
│ 为什么: ...                              │
│ 下一步: ...                              │
│ 进度: ...                                │
└─────────────────────────────────────────┘
```

## 遇到的问题
[计划内问题及解决方式]

## 下一阶段准备情况
[下一阶段已准备好的内容]
[阻塞项或关注点]
