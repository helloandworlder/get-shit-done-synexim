<purpose>
修补或创建 `AGENTS.md`，让当前仓库主动采用 GSD Synexim。
</purpose>

<required_reading>
开始前，先读取调用提示的 `execution_context` 中引用的全部文件。
</required_reading>

<process>

## 1. 读取当前文件

如果存在 `AGENTS.md`，先读取它。

读取 `@~/.claude/get-shit-done/templates/project-agents.md`。

## 2. 维护稳定托管区块

在 `AGENTS.md` 中使用这对精确标记：

```text
<!-- GSD-SYNEXIM:START -->
<!-- GSD-SYNEXIM:END -->
```

规则：
- 如果缺少 `AGENTS.md`，则基于模板创建。
- 如果标记区块已存在，仅替换区块内部内容。
- 如果 `AGENTS.md` 已存在但没有标记区块，则在文件末尾追加托管区块，并保留一个空行分隔。
- 不要改写与此无关的用户自定义说明。

## 3. 校验内容

确保托管区块包含以下全部要求：
- 中文优先的输出与文档生成
- 面向 micro / standard / large 工作规模的自适应规则
- 在文档、规划、执行、进度更新场景下主动触发 GSD 的规则
- 在文档或实现工作之后输出进度卡
- 在规划前端阶段前，先通过 Gemini AI Studio 前端原型关卡
- 当原型覆盖不足时，要求启动本地前端演示

## 4. 报告

返回一张简洁的中文卡片，说明：
- `AGENTS.md` 是新建还是修补
- 注入了哪些模块/规则
- 下一条推荐执行的 GSD 命令是什么


在完成文档产出或实现步骤后，输出一个中文进度卡式总结，简要说明产物、状态、风险和下一步。
</process>
