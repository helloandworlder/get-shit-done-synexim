<purpose>
切换 GSD 代理使用的模型配置档。在 Synexim 模式下，这控制 OpenAI GPT-5.4 的使用策略：规划使用 `xhigh/high`，实现使用 `high`。
</purpose>

<required_reading>
开始前读取调用提示的 execution_context 中引用的所有文件。
</required_reading>

<process>

<step name="validate">
校验参数：

```
if $ARGUMENTS.profile not in ["quality", "balanced", "budget"]:
  Error: Invalid profile "$ARGUMENTS.profile"
  Valid profiles: quality, balanced, budget
  EXIT
```
</step>

<step name="ensure_and_load_config">
确保配置存在并加载当前状态：

```bash
node "$HOME/.claude/get-shit-done/bin/gsd-tools.cjs" config-ensure-section
INIT=$(node "$HOME/.claude/get-shit-done/bin/gsd-tools.cjs" state load)
if [[ "$INIT" == @file:* ]]; then INIT=$(cat "${INIT#@file:}"); fi
```

如果缺失，会先以默认值创建 `.planning/config.json`，然后加载当前配置。
</step>

<step name="update_config">
从 `state load` 输出或配置文件中读取当前配置：

更新 `model_profile` 字段：
```json
{
  "model_profile": "$ARGUMENTS.profile"
}
```

将更新后的配置写回 `.planning/config.json`。
</step>

<step name="confirm">
显示确认信息、所选 profile 的模型表，以及对应的 effort 策略：

```
✓ Model profile set to: $ARGUMENTS.profile

代理后续将使用：

[Show table from MODEL_PROFILES in gsd-tools.cjs for selected profile]

Example:
| Agent | Model |
|-------|-------|
| gsd-planner | openai/gpt-5.4 |
| gsd-executor | openai/gpt-5.4 |
| gsd-verifier | openai/gpt-5.4 |
| ... | ... |

之后新启动的代理都会使用新的 profile。
```

配置档含义：
- quality: GPT-5.4 xhigh 用于路线图/阶段规划，GPT-5.4 high 用于实现
- balanced: GPT-5.4 high 用于规划与实现
- budget: GPT-5.4 high，但在合理情况下减少辅助代理/检查
</step>

</process>

<success_criteria>
- [ ] Argument validated
- [ ] Config file ensured
- [ ] Config updated with new model_profile
- [ ] Confirmation displayed with model table
</success_criteria>
