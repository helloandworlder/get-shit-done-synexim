---
phase: {N}
slug: {phase-slug}
status: draft
nyquist_compliant: false
wave_0_complete: false
created: {date}
---

# 阶段 {N} — 验证策略

> 执行期间反馈采样的每阶段验证合同。

---

## 测试基础设施

|物业 |价值|
|----------|--------|
| **框架** | {pytest 7.x / jest 29.x / vitest / go test / other} |
| **配置文件** | {path or "none — Wave 0 installs"} |
| **快速运行命令** | `{quick command}` |
| **全套命令** | `{full command}` |
| **预计运行时间** | ~{N} 秒 |

---

## 采样率

- **每次任务提交后：** 运行 `{quick run command}`
- **每次计划波后：** 运行 `{full suite command}`
- **`/gsd:verify-work`之前：**全套必须是绿色的
- **最大反馈延迟：** {N} 秒

---

## 每任务验证图

|任务 ID |计划|波|要求|测试类型|自动化命令|文件存在 |状态 |
|--------|------|------|-------------|------------|--------------------|-------------|--------|
| {N}-01-01 | 01 | 1 |请求-{XX} |单位| `{command}` | ✅ / ❌ W0 | ⬜ 待定 |

*状态：⬜待处理·✅绿色·❌红色·⚠️片状*

---

## 第 0 波要求

- [ ] `{tests/test_file.py}` — REQ-{XX} 的存根
- [ ] `{tests/conftest.py}` — 共享灯具
- [ ] `{framework install}` — 如果未检测到框架

*如果没有：“现有基础设施满足所有阶段要求。”*

---

## 仅手动验证

|行为 |要求 |为什么手动 |测试说明|
|----------|-------------|------------|--------------------|
| {behavior} |请求-{XX} | {reason} | {steps} |

*如果没有：“所有阶段行为都有自动验证。”*

---

## 验证签核

- [ ] 所有任务都有 `<automated>` 验证或 Wave 0 依赖项
- [ ] 采样连续性：没有自动验证的连续 3 个任务
- [ ] Wave 0 涵盖所有缺失的参考文献
- [ ] 无监视模式标志
- [ ] 反馈延迟 < {N}s
- [ ] `nyquist_compliant: true` 设置在 frontmatter 中

**批准：** {pending / approved YYYY-MM-DD}