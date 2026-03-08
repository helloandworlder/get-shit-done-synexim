---
description: 在 GSD 更新后重新应用本地修改
allowed-tools: Read, Write, Edit, Bash, Glob, Grep, AskUserQuestion
---

<purpose>
当 GSD 更新清空并重装文件后，此命令会把用户之前保存的本地修改重新合并回新版本。它会使用智能比对处理上游文件同时发生变化的情况。
</purpose>

<process>

## 步骤 1：检测已备份的补丁

检查本地补丁目录：

```bash
# Global install — detect runtime config directory
if [ -d "$HOME/.config/opencode/gsd-local-patches" ]; then
  PATCHES_DIR="$HOME/.config/opencode/gsd-local-patches"
elif [ -d "$HOME/.opencode/gsd-local-patches" ]; then
  PATCHES_DIR="$HOME/.opencode/gsd-local-patches"
elif [ -d "$HOME/.gemini/gsd-local-patches" ]; then
  PATCHES_DIR="$HOME/.gemini/gsd-local-patches"
else
  PATCHES_DIR="$HOME/.claude/gsd-local-patches"
fi
# Local install fallback — check all runtime directories
if [ ! -d "$PATCHES_DIR" ]; then
  for dir in .config/opencode .opencode .gemini .claude; do
    if [ -d "./$dir/gsd-local-patches" ]; then
      PATCHES_DIR="./$dir/gsd-local-patches"
      break
    fi
  done
fi
```

Read `backup-meta.json` from the patches directory.

**If no patches found:**
```
未发现本地补丁，无需重新应用。

当你在修改过 GSD 工作流、命令或代理文件后运行 `/gsd:update` 时，本地补丁会被自动保存。
after modifying any GSD workflow, command, or agent files.
```
Exit.

## 步骤 2：显示补丁摘要

```
## 待重新应用的本地补丁

**备份来源版本：** v{from_version}
**当前版本：** {read VERSION file}
**修改文件数：** {count}

| # | File | Status |
|---|------|--------|
| 1 | {file_path} | Pending |
| 2 | {file_path} | Pending |
```

## 步骤 3：合并每个文件

For each file in `backup-meta.json`:

1. **Read the backed-up version** (user's modified copy from `gsd-local-patches/`)
2. **Read the newly installed version** (current file after update)
3. **Compare and merge:**

   - If the new file is identical to the backed-up file: skip (modification was incorporated upstream)
   - If the new file differs: identify the user's modifications and apply them to the new version

   **Merge strategy:**
   - Read both versions fully
   - Identify sections the user added or modified (look for additions, not just differences from path replacement)
   - Apply user's additions/modifications to the new version
   - If a section the user modified was also changed upstream: flag as conflict, show both versions, ask user which to keep

4. **Write merged result** to the installed location
5. **Report status:**
   - `Merged` — user modifications applied cleanly
   - `Skipped` — modification already in upstream
   - `Conflict` — user chose resolution

## 步骤 4：更新清单

After reapplying, regenerate the file manifest so future updates correctly detect these as user modifications:

```bash
# The manifest will be regenerated on next /gsd:update
# For now, just note which files were modified
```

## 步骤 5：清理选项

Ask user:
- "Keep patch backups for reference?" → preserve `gsd-local-patches/`
- "Clean up patch backups?" → remove `gsd-local-patches/` directory

## 步骤 6：结果报告

```
## 补丁已重新应用

| # | File | Status |
|---|------|--------|
| 1 | {file_path} | ✓ Merged |
| 2 | {file_path} | ○ Skipped (already upstream) |
| 3 | {file_path} | ⚠ Conflict resolved |

{count} file(s) updated. Your local modifications are active again.
```


完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>

<success_criteria>
- [ ] All backed-up patches processed
- [ ] User modifications merged into new version
- [ ] Conflicts resolved with user input
- [ ] Status reported for each file
</success_criteria>
