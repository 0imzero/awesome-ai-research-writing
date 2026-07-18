# GitHub 中文展示设计

## 背景

Fork 已在 `agent/add-research-writing-skill` 分支加入 `research-writing-prompts` Skill，并通过草稿 PR #1 提交。新增内容目前以英文界面元数据和英文 PR 说明为主，与仓库已有的中文 README 风格不一致。

## 目标

让 GitHub 上面向读者的新增内容以中文展示，同时保留 Skill 内部英文路由指令，避免影响自然语言意图识别与执行稳定性。

## 方案比较

1. 展示层中文、内部指令保留英文（采用）：中文化 README 介绍、Skill 界面元数据和 PR 信息；改动小，兼顾可读性与路由稳定性。
2. Skill 全量中文化：连 `SKILL.md` 内部路由指令一起翻译；展示统一，但改动面大，可能改变触发与约束语义。
3. 仅中文化 PR：改动最少，但仓库合并后缺少中文入口，读者难以发现和安装 Skill。

## 设计

### README

在 README 顶部加入“本 Fork 的增强内容”，让访客首先看到上游来源、Fork 维护者新增内容和 Skill 入口；同时在 Part II 的 Skills 内容中保留“科研写作 Prompt 路由 Skill”详细中文介绍，说明：

- Skill 目录与核心能力；
- 支持自然语言自动分配 17 类学术写作工作流；
- Codex 本地安装位置示例；
- 来源、Fork 关系和无许可证背景下的使用提醒。

不重写原作者已有 README 内容，仅增加 Fork 维护者的扩展说明。

### GitHub About

将仓库 About 描述设置为：“基于 awesome-ai-research-writing，新增支持自然语言路由的 Codex 科研写作 Skill。”让搜索结果和仓库侧栏直接展示本 Fork 的差异。

### Skill 界面元数据

将 `agents/openai.yaml` 中面向用户的 `display_name`、`short_description` 和 `default_prompt` 改为中文。Skill 标识 `$research-writing-prompts` 保持不变。

### 内部 Skill 指令

保持 `SKILL.md` 和 Prompt 参考文件的内部内容不变。它们属于执行层，不承担 GitHub 中文展示职责。

### PR 与合并

将 Fork 内 PR #1 的标题和正文改为中文，明确修改范围、使用价值、来源说明与验证结果。验证通过后将 PR 转为可审阅状态，并合并到 `0imzero/awesome-ai-research-writing` 的 `main`，不向上游仓库创建 PR。

## 验证

- 使用 `quick_validate.py` 在 UTF-8 模式下校验 Skill；
- 使用 `git diff --check` 检查补丁格式；
- 核对 PR 文件列表、提交数和目标仓库；
- 合并后确认 `main` 包含 README 中文入口和完整 Skill 目录。

## 边界与异常处理

所有远端写操作只作用于用户自己的 Fork。远端更新失败时停止合并，先核对分支、PR 和主分支状态，避免重复创建分支或 PR。
