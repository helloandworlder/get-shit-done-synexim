# 模型配置档解析

在编排开始时解析一次模型配置档，然后将结果复用于所有 Task 派发。

## 解析模式

```bash
MODEL_PROFILE=$(cat .planning/config.json 2>/dev/null | grep -o '"model_profile"[[:space:]]*:[[:space:]]*"[^"]*"' | grep -o '"[^"]*"$' | tr -d '"' || echo "balanced")
```

默认值：若未设置或配置缺失，则使用 `balanced`。

## 查询表

@~/.claude/get-shit-done/references/model-profiles.md

根据解析出的 profile 在表中查找对应代理，并在 Task 调用中传入 `model` 参数：

```
Task(
  prompt="...",
  subagent_type="gsd-planner",
  model="{resolved_model}"  # typically "openai/gpt-5.4" in Synexim mode
)
```

**说明：** 在 Synexim 模式下，基础代理模型是 `openai/gpt-5.4`。不同 profile 的差异主要体现在规划 effort（`xhigh` 与 `high`）以及是否开启更多可选辅助工作。

## 使用方式

1. 在编排开始时解析一次
2. 保存解析出的 profile 值
3. 为每个待启动代理从表中查模型
4. 在每次 Task 调用中传入 `model` 参数（通常是 `"openai/gpt-5.4"`）
