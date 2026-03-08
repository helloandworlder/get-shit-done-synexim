<purpose>
Switch the model profile used by GSD agents. In Synexim mode this controls how OpenAI GPT-5.4 is applied: planning uses `xhigh/high`, implementation uses `high`.
</purpose>

<required_reading>
Read all files referenced by the invoking prompt's execution_context before starting.
</required_reading>

<process>

<step name="validate">
Validate argument:

```
if $ARGUMENTS.profile not in ["quality", "balanced", "budget"]:
  Error: Invalid profile "$ARGUMENTS.profile"
  Valid profiles: quality, balanced, budget
  EXIT
```
</step>

<step name="ensure_and_load_config">
Ensure config exists and load current state:

```bash
node "$HOME/.claude/get-shit-done/bin/gsd-tools.cjs" config-ensure-section
INIT=$(node "$HOME/.claude/get-shit-done/bin/gsd-tools.cjs" state load)
if [[ "$INIT" == @file:* ]]; then INIT=$(cat "${INIT#@file:}"); fi
```

This creates `.planning/config.json` with defaults if missing and loads current config.
</step>

<step name="update_config">
Read current config from state load or directly:

Update `model_profile` field:
```json
{
  "model_profile": "$ARGUMENTS.profile"
}
```

Write updated config back to `.planning/config.json`.
</step>

<step name="confirm">
Display confirmation with model table for selected profile and explain the effort policy:

```
✓ Model profile set to: $ARGUMENTS.profile

Agents will now use:

[Show table from MODEL_PROFILES in gsd-tools.cjs for selected profile]

Example:
| Agent | Model |
|-------|-------|
| gsd-planner | openai/gpt-5.4 |
| gsd-executor | openai/gpt-5.4 |
| gsd-verifier | openai/gpt-5.4 |
| ... | ... |

Next spawned agents will use the new profile.
```

Map profile names:
- quality: GPT-5.4 xhigh for roadmap/phase planning, GPT-5.4 high for implementation
- balanced: GPT-5.4 high for planning and implementation
- budget: GPT-5.4 high, but with fewer auxiliary agents/checks when reasonable
</step>

</process>

<success_criteria>
- [ ] Argument validated
- [ ] Config file ensured
- [ ] Config updated with new model_profile
- [ ] Confirmation displayed with model table
</success_criteria>
