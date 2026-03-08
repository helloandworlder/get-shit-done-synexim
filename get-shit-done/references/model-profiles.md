# 模型配置档

模型配置档用于控制 Synexim 如何在规划与实现阶段使用 `OpenAI GPT-5.4`。基础模型保持一致，变化的是 effort 强度与辅助工作量。

## 配置档定义

| Agent | `quality` | `balanced` | `budget` |
|-------|-----------|------------|----------|
| gsd-planner | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-roadmapper | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-executor | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-phase-researcher | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-project-researcher | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-research-synthesizer | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-debugger | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-codebase-mapper | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-verifier | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-plan-checker | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-integration-checker | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |
| gsd-nyquist-auditor | openai/gpt-5.4 | openai/gpt-5.4 | openai/gpt-5.4 |

## 配置档策略

**quality** - 最大化规划深度
- GPT-5.4 `xhigh` 用于路线图、研究汇总与阶段规划
- GPT-5.4 `high` 用于执行与验证
- 适用场景：关键架构工作、复杂里程碑拆分、高风险规划

**balanced**（默认）- 实用默认档
- GPT-5.4 `high` 用于规划、执行与验证
- 适用场景：常规开发、多数里程碑、日常交付

**budget** - 同一模型，减少可选工作
- GPT-5.4 `high` 保持不变，但在合适时减少可选辅助代理/检查
- 适用场景：通过工作流收缩来节省 token，而不是降低基础模型

## 前端设计规则

- GPT-5.4 在项目初始化阶段不得直接承担前端设计工作。
- 若项目或里程碑涉及前端实现，必须先确认存在完整的 Gemini AI Studio MVP 原型。
- 若原型与 `.planning` 不一致，必须先列出差异，并询问用户要“补全”还是“移除”，再继续推进。

## 解析逻辑

编排器在启动代理前应先解析模型：

```
1. Read .planning/config.json
2. Check model_overrides for agent-specific override
3. If no override, look up agent in profile table
4. Pass model parameter to Task call
```

## 单代理覆盖

如果不想改整个 profile，可单独覆盖某些代理：

```json
{
  "model_profile": "balanced",
  "model_overrides": {
    "gsd-executor": "opus",
    "gsd-planner": "haiku"
  }
}
```

单代理覆盖优先级高于 profile。有效值应为运行时支持的模型标识，例如 `openai/gpt-5.4`。

## 切换配置档

运行时命令：`/gsd:set-profile <profile>`

项目级默认值：在 `.planning/config.json` 中设置：
```json
{
  "model_profile": "balanced"
}
```

## 设计理由

**为什么规划默认用 GPT-5.4？**
规划决定整个里程碑的结构。这里的推理更强，能减少文档漂移与过度规划。

**为什么执行阶段用 GPT-5.4 high？**
执行仍然需要足够的推理能力来安全适配计划，但不应该进入路线图/阶段规划那种更慢、更发散的探索深度。

**为什么要禁止 GPT-5.4 在初始化阶段直接做前端设计？**
初始化阶段的目标是对齐需求和验证原型是否就绪，而不是临时发明 UI。设计应优先来自经过人工确认的 Gemini AI Studio MVP 原型。
