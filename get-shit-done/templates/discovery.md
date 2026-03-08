# 发现模板

`.planning/phases/XX-name/DISCOVERY.md` 模板 - 库/选项决策的浅层研究。

**目的：** 在计划阶段的强制发现过程中回答“我们应该使用哪个库/选项”的问题。

对于深入的生态系统研究（“专家如何构建这个”），请使用生成 RESEARCH.md 的 `/gsd:research-phase`。

---

## 文件模板

```markdown
---
phase: XX-name
type: discovery
topic: [discovery-topic]
---

<session_initialization>
Before beginning discovery, verify today's date:
!`date +%Y-%m-%d`

Use this date when searching for "current" or "latest" information.
Example: If today is 2025-11-22, search for "2025" not "2024".
</session_initialization>

<discovery_objective>
Discover [topic] to inform [phase name] implementation.

Purpose: [What decision/implementation this enables]
Scope: [Boundaries]
Output: DISCOVERY.md with recommendation
</discovery_objective>

<discovery_scope>
<include>
- [Question to answer]
- [Area to investigate]
- [Specific comparison if needed]
</include>

<exclude>
- [Out of scope for this discovery]
- [Defer to implementation phase]
</exclude>
</discovery_scope>

<discovery_protocol>

**Source Priority:**
1. **Context7 MCP** - For library/framework documentation (current, authoritative)
2. **Official Docs** - For platform-specific or non-indexed libraries
3. **WebSearch** - For comparisons, trends, community patterns (verify all findings)

**Quality Checklist:**
Before completing discovery, verify:
- [ ] All claims have authoritative sources (Context7 or official docs)
- [ ] Negative claims ("X is not possible") verified with official documentation
- [ ] API syntax/configuration from Context7 or official docs (never WebSearch alone)
- [ ] WebSearch findings cross-checked with authoritative sources
- [ ] Recent updates/changelogs checked for breaking changes
- [ ] Alternative approaches considered (not just first solution found)

**Confidence Levels:**
- HIGH: Context7 or official docs confirm
- MEDIUM: WebSearch + Context7/official docs confirm
- LOW: WebSearch only or training knowledge only (mark for validation)

</discovery_protocol>


<output_structure>
Create `.planning/phases/XX-name/DISCOVERY.md`:

```降价
# [Topic] 发现

## 总结
[2-3 paragraph executive summary - what was researched, what was found, what's recommended]

## 主要推荐
[What to do and why - be specific and actionable]

## 考虑的替代方案
[What else was evaluated and why not chosen]

## 主要发现

### [Category 1]
- [Finding with source URL and relevance to our case]

### [Category 2]
- [Finding with source URL and relevance]

## 代码示例
[Relevant implementation patterns, if applicable]

## 元数据

<metadata>
<confidence level="high|medium|low">
[Why this confidence level - based on source quality and verification]
</confidence>

<sources>
- [Primary authoritative sources used]
</sources>

<open_questions>
[What couldn't be determined or needs validation during implementation]
</open_questions>

<validation_checkpoints>
[If confidence is LOW or MEDIUM, list specific things to verify during implementation]
</validation_checkpoints>
</metadata>
```
</output_structure>

<success_criteria>
- All scope questions answered with authoritative sources
- Quality checklist items completed
- Clear primary recommendation
- Low-confidence findings marked with validation checkpoints
- Ready to inform PLAN.md creation
</success_criteria>

<guidelines>
**When to use discovery:**
- Technology choice unclear (library A vs B)
- Best practices needed for unfamiliar integration
- API/library investigation required
- Single decision pending

**When NOT to use:**
- Established patterns (CRUD, auth with known library)
- Implementation details (defer to execution)
- Questions answerable from existing project context

**When to use RESEARCH.md instead:**
- Niche/complex domains (3D, games, audio, shaders)
- Need ecosystem knowledge, not just library choice
- "How do experts build this" questions
- Use `/gsd:research-phase` 对于这些
</guidelines>