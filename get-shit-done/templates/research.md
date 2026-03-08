# 研究模板

`.planning/phases/XX-name/{phase_num}-RESEARCH.md` 模板 - 规划前的全面生态系统研究。

**目的：** 记录 Claude 需要了解什么才能很好地实现一个阶段 - 不仅仅是“哪个库”，而是“专家如何构建这个库”。

---

## 文件模板

```markdown
# Phase [X]: [Name] - Research

**Researched:** [date]
**Domain:** [primary technology/problem domain]
**Confidence:** [HIGH/MEDIUM/LOW]

<user_constraints>
## User Constraints (from CONTEXT.md)

**CRITICAL:** If CONTEXT.md exists from /gsd:discuss-phase, copy locked decisions here verbatim. These MUST be honored by the planner.

### Locked Decisions
[Copy from CONTEXT.md `## Decisions` section - these are NON-NEGOTIABLE]
- [Decision 1]
- [Decision 2]

### Claude's Discretion
[Copy from CONTEXT.md - areas where researcher/planner can choose]
- [Area 1]
- [Area 2]

### Deferred Ideas (OUT OF SCOPE)
[Copy from CONTEXT.md - do NOT research or plan these]
- [Deferred 1]
- [Deferred 2]

**If no CONTEXT.md exists:** Write "No user constraints - all decisions at Claude's discretion"
</user_constraints>

<research_summary>
## Summary

[2-3 paragraph executive summary]
- What was researched
- What the standard approach is
- Key recommendations

**Primary recommendation:** [one-liner actionable guidance]
</research_summary>

<standard_stack>
## Standard Stack

The established libraries/tools for this domain:

### Core
| Library | Version | Purpose | Why Standard |
|---------|---------|---------|--------------|
| [name] | [ver] | [what it does] | [why experts use it] |
| [name] | [ver] | [what it does] | [why experts use it] |

### Supporting
| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| [name] | [ver] | [what it does] | [use case] |
| [name] | [ver] | [what it does] | [use case] |

### Alternatives Considered
| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| [standard] | [alternative] | [when alternative makes sense] |

**Installation:**
```bash
npm 安装 [packages]
# 或
纱线添加[packages]
```
</standard_stack>

<architecture_patterns>
## Architecture Patterns

### Recommended Project Structure
```
源代码/
├── [folder]/#[purpose]
├── [folder]/#[purpose]
└── [folder]/#[purpose]
```

### Pattern 1: [Pattern Name]
**What:** [description]
**When to use:** [conditions]
**Example:**
```打字稿
// [code example from Context7/official docs]
```

### Pattern 2: [Pattern Name]
**What:** [description]
**When to use:** [conditions]
**Example:**
```打字稿
// [code example]
```

### Anti-Patterns to Avoid
- **[Anti-pattern]:** [why it's bad, what to do instead]
- **[Anti-pattern]:** [why it's bad, what to do instead]
</architecture_patterns>

<dont_hand_roll>
## Don't Hand-Roll

Problems that look simple but have existing solutions:

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| [problem] | [what you'd build] | [library] | [edge cases, complexity] |
| [problem] | [what you'd build] | [library] | [edge cases, complexity] |
| [problem] | [what you'd build] | [library] | [edge cases, complexity] |

**Key insight:** [why custom solutions are worse in this domain]
</dont_hand_roll>

<common_pitfalls>
## Common Pitfalls

### Pitfall 1: [Name]
**What goes wrong:** [description]
**Why it happens:** [root cause]
**How to avoid:** [prevention strategy]
**Warning signs:** [how to detect early]

### Pitfall 2: [Name]
**What goes wrong:** [description]
**Why it happens:** [root cause]
**How to avoid:** [prevention strategy]
**Warning signs:** [how to detect early]

### Pitfall 3: [Name]
**What goes wrong:** [description]
**Why it happens:** [root cause]
**How to avoid:** [prevention strategy]
**Warning signs:** [how to detect early]
</common_pitfalls>

<code_examples>
## Code Examples

Verified patterns from official sources:

### [Common Operation 1]
```打字稿
// 来源：[Context7/official docs URL]
[code]
```

### [Common Operation 2]
```打字稿
// 来源：[Context7/official docs URL]
[code]
```

### [Common Operation 3]
```打字稿
// 来源：[Context7/official docs URL]
[code]
```
</code_examples>

<sota_updates>
## State of the Art (2024-2025)

What's changed recently:

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| [old] | [new] | [date/version] | [what it means for implementation] |

**New tools/patterns to consider:**
- [Tool/Pattern]: [what it enables, when to use]
- [Tool/Pattern]: [what it enables, when to use]

**Deprecated/outdated:**
- [Thing]: [why it's outdated, what replaced it]
</sota_updates>

<open_questions>
## Open Questions

Things that couldn't be fully resolved:

1. **[Question]**
   - What we know: [partial info]
   - What's unclear: [the gap]
   - Recommendation: [how to handle during planning/execution]

2. **[Question]**
   - What we know: [partial info]
   - What's unclear: [the gap]
   - Recommendation: [how to handle]
</open_questions>

<sources>
## Sources

### Primary (HIGH confidence)
- [Context7 library ID] - [topics fetched]
- [Official docs URL] - [what was checked]

### Secondary (MEDIUM confidence)
- [WebSearch verified with official source] - [finding + verification]

### Tertiary (LOW confidence - needs validation)
- [WebSearch only] - [finding, marked for validation during implementation]
</sources>

<metadata>
## Metadata

**Research scope:**
- Core technology: [what]
- Ecosystem: [libraries explored]
- Patterns: [patterns researched]
- Pitfalls: [areas checked]

**Confidence breakdown:**
- Standard stack: [HIGH/MEDIUM/LOW] - [reason]
- Architecture: [HIGH/MEDIUM/LOW] - [reason]
- Pitfalls: [HIGH/MEDIUM/LOW] - [reason]
- Code examples: [HIGH/MEDIUM/LOW] - [reason]

**Research date:** [date]
**Valid until:** [estimate - 30 days for stable tech, 7 days for fast-moving]
</metadata>

---

*Phase: XX-name*
*Research completed: [date]*
*Ready for planning: [yes/no]*
```

---

## 好例子

```markdown
# Phase 3: 3D City Driving - Research

**Researched:** 2025-01-20
**Domain:** Three.js 3D web game with driving mechanics
**Confidence:** HIGH

<research_summary>
## Summary

Researched the Three.js ecosystem for building a 3D city driving game. The standard approach uses Three.js with React Three Fiber for component architecture, Rapier for physics, and drei for common helpers.

Key finding: Don't hand-roll physics or collision detection. Rapier (via @react-three/rapier) handles vehicle physics, terrain collision, and city object interactions efficiently. Custom physics code leads to bugs and performance issues.

**Primary recommendation:** Use R3F + Rapier + drei stack. Start with vehicle controller from drei, add Rapier vehicle physics, build city with instanced meshes for performance.
</research_summary>

<standard_stack>
## Standard Stack

### Core
| Library | Version | Purpose | Why Standard |
|---------|---------|---------|--------------|
| three | 0.160.0 | 3D rendering | The standard for web 3D |
| @react-three/fiber | 8.15.0 | React renderer for Three.js | Declarative 3D, better DX |
| @react-three/drei | 9.92.0 | Helpers and abstractions | Solves common problems |
| @react-three/rapier | 1.2.1 | Physics engine bindings | Best physics for R3F |

### Supporting
| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| @react-three/postprocessing | 2.16.0 | Visual effects | Bloom, DOF, motion blur |
| leva | 0.9.35 | Debug UI | Tweaking parameters |
| zustand | 4.4.7 | State management | Game state, UI state |
| use-sound | 4.0.1 | Audio | Engine sounds, ambient |

### Alternatives Considered
| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| Rapier | Cannon.js | Cannon simpler but less performant for vehicles |
| R3F | Vanilla Three | Vanilla if no React, but R3F DX is much better |
| drei | Custom helpers | drei is battle-tested, don't reinvent |

**Installation:**
```bash
npm 安装三个 @react-三/fibre @react-三/drei @react-三/rapier zustand
```
</standard_stack>

<architecture_patterns>
## Architecture Patterns

### Recommended Project Structure
```
源代码/
├── 组件/
│ ├── 车辆/ # 具有物理功能的玩家汽车
│ ├── 城市/ # 城市生成与建筑
│ ├── 道路/ # 道路网络
│ └── 环境/ # 天空、灯光、雾
├── 挂钩/
│ ├── useVehicleControls.ts
│ └── useGameState.ts
├── 店铺/
│ └── gameStore.ts # Zustand状态
└── 实用程序/
    └── cityGenerator.ts # 程序生成助手
```

### Pattern 1: Vehicle with Rapier Physics
**What:** Use RigidBody with vehicle-specific settings, not custom physics
**When to use:** Any ground vehicle
**Example:**
```打字稿
// 来源：@react- Three/rapier 文档
从“@react-三/剑杆”导入 { RigidBody, useRapier }

函数车辆（）{
  const 刚体 = useRef()

  返回（
    <RigidBody
      ref={body}
      type="dynamic"
      colliders="hull"
      mass={1200}
      linearDamping={0.4}
      angularDamping={0.8}
    >
      <mesh>
        <boxGeometry args={[2, 1, 4]} />
        <meshStandardMaterial />
      </mesh>
    </RigidBody>
  ）
}
```

### Pattern 2: Instanced Meshes for City
**What:** Use InstancedMesh for repeated objects (buildings, trees, props)
**When to use:** >100 similar objects
**Example:**
```打字稿
// 来源：drei 文档
从“@react-三/drei”导入 { Instances, Instance }

功能建筑物({ positions }) {
  返回（
    <Instances limit={1000}>
      <boxGeometry />
      <meshStandardMaterial />
      {positions.map((pos, i) => (
        <Instance key={i} position={pos} scale={[1, 1, 1]} />
      ))}
    </Instances>
  ）
}
```

### Anti-Patterns to Avoid
- **Creating meshes in render loop:** Create once, update transforms only
- **Not using InstancedMesh:** Individual meshes for buildings kills performance
- **Custom physics math:** Rapier handles it better, every time
</architecture_patterns>

<dont_hand_roll>
## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Vehicle physics | Custom velocity/acceleration | Rapier RigidBody | Wheel friction, suspension, collisions are complex |
| Collision detection | Raycasting everything | Rapier colliders | Performance, edge cases, tunneling |
| Camera follow | Manual lerp | drei CameraControls or custom with useFrame | Smooth interpolation, bounds |
| City generation | Pure random placement | Grid-based with noise for variation | Random looks wrong, grid is predictable |
| LOD | Manual distance checks | drei <Detailed> | Handles transitions, hysteresis |

**Key insight:** 3D game development has 40+ years of solved problems. Rapier implements proper physics simulation. drei implements proper 3D helpers. Fighting these leads to bugs that look like "game feel" issues but are actually physics edge cases.
</dont_hand_roll>

<common_pitfalls>
## Common Pitfalls

### Pitfall 1: Physics Tunneling
**What goes wrong:** Fast objects pass through walls
**Why it happens:** Default physics step too large for velocity
**How to avoid:** Use CCD (Continuous Collision Detection) in Rapier
**Warning signs:** Objects randomly appearing outside buildings

### Pitfall 2: Performance Death by Draw Calls
**What goes wrong:** Game stutters with many buildings
**Why it happens:** Each mesh = 1 draw call, hundreds of buildings = hundreds of calls
**How to avoid:** InstancedMesh for similar objects, merge static geometry
**Warning signs:** GPU bound, low FPS despite simple scene

### Pitfall 3: Vehicle "Floaty" Feel
**What goes wrong:** Car doesn't feel grounded
**Why it happens:** Missing proper wheel/suspension simulation
**How to avoid:** Use Rapier vehicle controller or tune mass/damping carefully
**Warning signs:** Car bounces oddly, doesn't grip corners
</common_pitfalls>

<code_examples>
## Code Examples

### Basic R3F + Rapier Setup
```打字稿
// 来源：@react- Three/rapier 入门
从“@react-三/纤维”导入 { Canvas }
从“@react-三/剑杆”导入 { Physics }

函数游戏（）{
  返回（
    <Canvas>
      <Physics gravity={[0, -9.81, 0]}>
        <Vehicle />
        <City />
        <Ground />
      </Physics>
    </Canvas>
  ）
}
```

### Vehicle Controls Hook
```打字稿
// 来源：社区模式，经 drei 文档验证
从“@react-三/纤维”导入 { useFrame }
从“@react-三/drei”导入 { useKeyboardControls }

函数 useVehicleControls(rigidBodyRef) {
  const [, getKeys] = useKeyboardControls()

  useFrame(() => {
    常量 { forward, back, left, right } = getKeys()
    常量主体 = rigidBodyRef.current
    if (!body) 返回

    常量脉冲 = { x: 0, y: 0, z: 0 }
    如果（转发）impulse.z -= 10
    如果（返回）impulse.z += 5

    body.applyImpulse(脉冲、真实)

    如果（左）body.applyTorqueImpulse（{ x: 0, y: 2, z: 0 }，真）
    如果（右）body.applyTorqueImpulse（{ x: 0, y: -2, z: 0 }，真）
  })
}
```
</code_examples>

<sota_updates>
## State of the Art (2024-2025)

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| cannon-es | Rapier | 2023 | Rapier is faster, better maintained |
| vanilla Three.js | React Three Fiber | 2020+ | R3F is now standard for React apps |
| Manual InstancedMesh | drei <Instances> | 2022 | Simpler API, handles updates |

**New tools/patterns to consider:**
- **WebGPU:** Coming but not production-ready for games yet (2025)
- **drei Gltf helpers:** <useGLTF.preload> for loading screens

**Deprecated/outdated:**
- **cannon.js (original):** Use cannon-es fork or better, Rapier
- **Manual raycasting for physics:** Just use Rapier colliders
</sota_updates>

<sources>
## Sources

### Primary (HIGH confidence)
- /pmndrs/react-three-fiber - getting started, hooks, performance
- /pmndrs/drei - instances, controls, helpers
- /dimforge/rapier-js - physics setup, vehicle physics

### Secondary (MEDIUM confidence)
- Three.js discourse "city driving game" threads - verified patterns against docs
- R3F examples repository - verified code works

### Tertiary (LOW confidence - needs validation)
- None - all findings verified
</sources>

<metadata>
## Metadata

**Research scope:**
- Core technology: Three.js + React Three Fiber
- Ecosystem: Rapier, drei, zustand
- Patterns: Vehicle physics, instancing, city generation
- Pitfalls: Performance, physics, feel

**Confidence breakdown:**
- Standard stack: HIGH - verified with Context7, widely used
- Architecture: HIGH - from official examples
- Pitfalls: HIGH - documented in discourse, verified in docs
- Code examples: HIGH - from Context7/official sources

**Research date:** 2025-01-20
**Valid until:** 2025-02-20 (30 days - R3F ecosystem stable)
</metadata>

---

*Phase: 03-city-driving*
*Research completed: 2025-01-20*
*Ready for planning: yes*
```

---

## 指南

**何时创建：**
- 在利基/复杂领域的规划阶段之前
- 当 Claude 的训练数据可能陈旧或稀疏时
- 当“专家如何做到这一点”比“哪个图书馆”更重要时

**结构：**
- 使用 XML 标签作为部分标记（与 GSD 模板匹配）
- 七个核心部分：summary、standard_stack、architecture_patterns、dont_hand_roll、common_pitfalls、code_examples、sources
- 所需的所有部分（推动全面研究）

**内容quality：**
- 标准堆栈：特定版本，而不仅仅是名称
- 架构：包括来自权威来源的实际代码示例
- 不要手卷：明确哪些问题不能自己解决- 陷阱：包括警告标志，而不仅仅是“不要这样做”
- 来源：诚实地标记置信水平

**与规划整合：**
- RESEARCH.md 在 PLAN.md 中作为 @context 引用加载
- 标准堆栈告知库选择
- 不要手卷防止定制解决方案
- 陷阱告知验证标准
- 任务操作中可以引用代码示例

**创建后：**
- 文件位于阶段目录：`.planning/phases/XX-name/{phase_num}-RESEARCH.md`
- 在规划工作流程期间参考
- 计划阶段在存在时自动加载它
