# 科研写作 Prompt 路由 Skill

`research-writing-prompts` 把本仓库 Part I 中的科研写作 Prompt 整理成一个可由 Codex 加载的 Skill。使用时不必查找模板名称，直接描述任务即可。例如：

- “把这段中文翻译成论文英文，保留 LaTeX。”
- “这段实验分析太长，缩短一点，但不要删掉数据。”
- “从 ICML 审稿人的角度检查这篇论文。”

Skill 会结合任务含义、输入语言和文档格式选择对应工作流。除非用户另有要求，输出仍遵循原 Prompt 的格式。

## 适合哪些任务

这个 Skill 面向已有材料的处理：论文草稿、LaTeX 片段、实验数据、图表说明或待审阅的论文文件。它不负责从零撰写整篇论文，也不代替引用核验、会议模板配置或 camera-ready 检查。

目前收录 17 个工作流：

| 类别 | 工作流 | 常见说法 |
|---|---|---|
| 翻译与改写 | 中转英-latex、中转英-word | “翻译成论文英文并润色”“保留 LaTeX” |
| 翻译与改写 | 英转中-latex | “把这段英文 LaTeX 直译成中文” |
| 翻译与改写 | 中转中-word | “把零散中文整理成正式论文段落” |
| 长度调整 | 缩写、扩写 | “压短一点”“补充逻辑，但别注水” |
| 表达修改 | 英文润色、中文润色 | “润色这段论文正文”“只改必要问题” |
| 逻辑与风格 | 逻辑检查、英文去 AI 味、中文去 AI 味 | “检查论证跳跃”“写得自然一点” |
| 图表 | 论文架构图、实验绘图推荐 | “设计方法框架图”“这些数据用什么图合适” |
| 图表 | 生成图标题、生成表标题 | “给 Figure 2 写英文标题” |
| 分析与审阅 | 实验分析、Reviewer 审视 | “分析消融结果”“按目标会议审稿” |

## 如何选择工作流

路由遵循三个判断顺序：

1. 先看用户明确提出的任务、语言方向和输出格式。
2. 再判断输入是 LaTeX、Word 风格文本、实验数据还是论文文件。
3. 如果仍有两种合理解释，再向用户确认，不自行猜测。

LaTeX 命令、引用、标签、转义字符和 `$...$` 公式会被视为强格式信号。用户明确指定 Word 或纯文本时，以用户要求为准。

复合任务按用户给出的顺序执行。例如“先缩写，再去 AI 味”会先压缩内容，再处理语言风格。两个操作互相冲突且没有顺序时，Skill 会先询问。

## 使用示例

可以直接用自然语言：

```text
把下面中文翻译成 ICML 风格的英文，输出 LaTeX，并附中文直译供我核对。
```

```text
这段 Related Work 太长了，减少 10 个左右的英文单词，不要删引用和技术细节。
```

```text
根据这张消融实验表写一段 LaTeX 分析。只能使用表中数据，不要虚构显著性结论。
```

也可以显式调用 Skill：

```text
使用 $research-writing-prompts 检查这段方法描述的逻辑问题。
```

## 安装到 Codex

先克隆本 Fork：

```bash
git clone https://github.com/0imzero/awesome-ai-research-writing.git
```

然后把下面的目录复制到 Codex 的本地 Skills 目录：

```text
awesome-ai-research-writing/skills/research-writing-prompts
→ ~/.codex/skills/research-writing-prompts
```

重新启动 Codex 后，可以直接描述任务，也可以使用 `$research-writing-prompts` 显式调用。

## 文件结构

```text
research-writing-prompts/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── translation.md
    ├── revision.md
    ├── figures-and-tables.md
    ├── analysis-and-review.md
    └── provenance.md
```

`SKILL.md` 负责判断任务和格式。详细 Prompt 按用途拆分在 `references/` 中，只在匹配到对应任务时读取。`provenance.md` 记录来源和使用边界。

## 使用边界

- 缺少原文、数据、论文文件或目标会议时，Skill 会先索取必要输入。
- 不会编造实验数值、趋势、引用或审稿证据。
- 用户指定的输出格式优先于默认格式，但事实忠实、非虚构和学术严谨要求仍然保留。

## 来源与许可

Prompt 来源于 [Leey21/awesome-ai-research-writing](https://github.com/Leey21/awesome-ai-research-writing) README 的 Part I。本 Fork 增加了自然语言路由、Codex Skill 目录结构和中文使用说明，Prompt 正文没有被有意改写。

打包时，上游仓库没有声明仓库许可证。本目录不主张对原 Prompt 拥有权，也不授予新的许可证。请保留作者署名和 Fork 关系；如果要把 Prompt 文本复制到无关仓库、重新发布或重新许可，请先取得原作者同意。