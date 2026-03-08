# Model Profiles

Model profiles control how Synexim applies `OpenAI GPT-5.4` across planning and implementation. The model stays the same; the effort level and amount of auxiliary work change by profile.

## Profile Definitions

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

## Profile Philosophy

**quality** - Maximum planning depth
- GPT-5.4 with `xhigh` effort for roadmap, research synthesis, and phase planning
- GPT-5.4 with `high` effort for execution and verification
- Use when: critical architecture work, complex milestone slicing, high-risk planning

**balanced** (default) - Practical default
- GPT-5.4 with `high` effort for planning, execution, and verification
- Use when: normal development, most milestones, everyday delivery

**budget** - Same model, less optional work
- GPT-5.4 with `high` effort, but reduce optional auxiliary agents/checks when appropriate
- Use when: conserving tokens by workflow shape rather than by downgrading the base model

## Front-end Design Rule

- GPT-5.4 must not perform front-end design during project initialization.
- If a project or milestone contains front-end implementation, first confirm a complete Gemini AI Studio MVP prototype exists.
- If the prototype and `.planning` disagree, list the differences and ask the user whether to补全 or移除 them before continuing.

## Resolution Logic

Orchestrators resolve model before spawning:

```
1. Read .planning/config.json
2. Check model_overrides for agent-specific override
3. If no override, look up agent in profile table
4. Pass model parameter to Task call
```

## Per-Agent Overrides

Override specific agents without changing the entire profile:

```json
{
  "model_profile": "balanced",
  "model_overrides": {
    "gsd-executor": "opus",
    "gsd-planner": "haiku"
  }
}
```

Overrides take precedence over the profile. Valid values are runtime-supported model identifiers such as `openai/gpt-5.4`.

## Switching Profiles

Runtime: `/gsd:set-profile <profile>`

Per-project default: Set in `.planning/config.json`:
```json
{
  "model_profile": "balanced"
}
```

## Design Rationale

**Why GPT-5.4 for planning?**
Planning sets the structure for the entire milestone. Stronger reasoning here reduces document drift and over-planning.

**Why GPT-5.4 high for execution?**
Execution still needs enough reasoning to adapt plans safely, but should avoid the slower exploratory depth reserved for roadmap/phase planning.

**Why block GPT-5.4 from front-end design during initialization?**
Initialization should align requirements and verify prototype readiness, not invent UI. Design should come from a human-reviewed Gemini AI Studio MVP prototype first.
