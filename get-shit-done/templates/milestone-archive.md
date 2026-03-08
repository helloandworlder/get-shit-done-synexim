# 里程碑存档模板

完整里程碑工作流程使用此模板在 `.planning/milestones/` 中创建存档文件。

---

## 文件模板

# 里程碑 v{{VERSION}}：{{MILESTONE_NAME}}

**状态：** ✅ 已发货 {{DATE}}
**阶段：** {{PHASE_START}}-{{PHASE_END}}
**总计划：** {{TOTAL_PLANS}}

## 概述

{{MILESTONE_DESCRIPTION}}

## 阶段

{{PHASES_SECTION}}

[For each phase in this milestone, include:]

### 阶段 {{PHASE_NUM}}：{{PHASE_NAME}}

**目标**：{{PHASE_GOAL}}
**取决于**：{{DEPENDS_ON}}
**计划**：{{PLAN_COUNT}}计划

计划：

- [x] {{PHASE}}-01：{{PLAN_DESCRIPTION}}
- [x] {{PHASE}}-02：{{PLAN_DESCRIPTION}}
      [... all plans ...]

**详情：**
{{PHASE_DETAILS_FROM_ROADMAP}}

**对于小数相位，包括（插入）标记：**

### 阶段 2.1：关键安全补丁（已插入）

**目标**：修复身份验证绕过漏洞
**取决于**：第 2 阶段
**计划**：1 个计划

计划：

- [x] 02.1-01：补丁身份验证漏洞

**详情：**
{{PHASE_DETAILS_FROM_ROADMAP}}

---

## 里程碑总结

**十进制相位：**

- 2.1 阶段：关键安全补丁（在第 2 阶段之后插入以进行紧急修复）
- 5.1 阶段：性能修补程序（针对生产问题在第 5 阶段之后插入）

**关键决策：**
{{DECISIONS_FROM_PROJECT_STATE}}
[Example:]

- 决定：使用 ROADMAP.md 分割（理由：上下文成本恒定）
- 决策：十进制相位编号（基本原理：清晰的插入语义）

**已解决的问题：**
{{ISSUES_RESOLVED_DURING_MILESTONE}}
[Example:]

- 修复了 100 多个阶段的上下文溢出
- 解决了相位插入混乱的问题

**推迟的问题：**
{{ISSUES_DEFERRED_TO_LATER}}
[Example:]

- PROJECT-STATE.md 分层（推迟到决策 > 300 为止）

**产生的技术债务：**
{{SHORTCUTS_NEEDING_FUTURE_WORK}}
[Example:]

- 某些工作流程仍然具有硬编码路径（在第 5 阶段修复）

---

_当前项目状态，请参见.planning/ROADMAP.md_

---

## 使用指南

<guidelines>
**何时创建里程碑档案：**
- 完成里程碑的所有阶段后（v1.0、v1.1、v2.0 等）
- 由完整的里程碑工作流程触发
- 在计划下一个里程碑工作之前

**如何填写模板：**

- 将 {{PLACEHOLDERS}} 替换为实际值
- 从 ROADMAP.md 中提取相位详细信息
- 使用（插入）标记记录小数相位
- 包括 PROJECT-STATE.md 或摘要文件中的关键决策
- 列出已解决和已推迟的问题
- 捕获技术债务以供将来参考

**存档位置：**

- 保存到`.planning/milestones/v{VERSION}-{NAME}.md`
- 示例：`.planning/milestones/v1.0-mvp.md`

**归档后：**

- 更新 ROADMAP.md 以折叠 `<details>` 标签中已完成的里程碑
- 将 PROJECT.md 更新为带有当前状态部分的棕地格式
- 在下一个里程碑中继续进行阶段编号（切勿从 01 重新开始）
  </guidelines>