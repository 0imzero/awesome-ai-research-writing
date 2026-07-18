---
name: research-writing-prompts
description: Route specific academic and research-writing requests to specialized source prompt workflows. Use for Chinese-English academic translation in LaTeX or Word/plain text, Chinese academic rewriting, shortening or expansion, English or Chinese paper polishing, logic checking, academic de-AI/humanization, paper architecture diagrams, experimental plot recommendations, figure or table titles, experiment-result analysis, and reviewer-style paper evaluation. Infer the workflow from natural language, content, and formatting clues. Do not use for end-to-end paper drafting, citation research, conference templates, camera-ready preparation, or generic non-academic prose editing.
---

# Research Writing Prompts

Infer the user's academic-writing intent, load only the matching source prompt, and execute it. Preserve that prompt's original output contract unless the user explicitly overrides it.

## Route the request

Evaluate evidence in this order:

1. Obey the user's explicit task, language direction, format, and output instructions.
2. Infer the intended outcome from semantic meaning, not exact keyword matching.
3. Inspect the input for LaTeX commands, formulas, citations, tables, data, or plain prose.
4. Apply the defaults below only when stronger evidence is absent.

Do not announce the internal route or reference-file selection in the normal result.

### Translation and rewriting

Read [references/translation.md](references/translation.md), then select exactly one prompt:

| Intent | Route |
|---|---|
| Translate a Chinese draft into academic English | 中转英-latex or 中转英-word |
| Translate English LaTeX into Chinese for comprehension | 英转中-latex |
| Rewrite rough Chinese ideas as formal Chinese paper prose | 中转中-word |

Treat requests such as “翻译成英文并润色” as translation because the source translation workflow already includes polishing.

### Revision and humanization

Read [references/revision.md](references/revision.md), then select exactly one prompt:

| Intended outcome | Route |
|---|---|
| Make an English LaTeX passage slightly shorter without losing information | 缩写 |
| Make an English LaTeX passage slightly longer by exposing implicit logic | 扩写 |
| Improve academic English while preserving LaTeX | 表达润色（英文论文） |
| Correct only necessary issues in Chinese academic prose | 表达润色（中文论文） |
| Diagnose coherence, reasoning gaps, or unsupported claims | 逻辑检查 |
| Make English LaTeX sound less AI-generated | 去 AI 味（LaTeX 英文） |
| Make Chinese Word/plain text sound less AI-generated | 去 AI 味（Word 中文） |

Interpret natural phrases semantically. For example, “压短一点” means shortening, “补充一点但别注水” means expansion, and “从逻辑上挑问题” means logic checking.

### Figures and tables

Read [references/figures-and-tables.md](references/figures-and-tables.md), then select exactly one prompt:

| Intended outcome | Route |
|---|---|
| Plan or generate a paper method/framework/pipeline diagram | 论文架构图 |
| Recommend a chart for experimental data and a desired claim | 实验绘图推荐 |
| Generate an English figure title or caption | 生成图的标题 |
| Generate an English table title or caption | 生成表的标题 |

### Analysis and review

Read [references/analysis-and-review.md](references/analysis-and-review.md), then select exactly one prompt:

| Intended outcome | Route |
|---|---|
| Analyze results, trends, comparisons, ablations, or trade-offs | 实验分析 |
| Evaluate an uploaded paper from a target venue's reviewer perspective | 论文整体以 Reviewer 视角进行审视 |

## Select the format

- Honor explicit `LaTeX` or `Word` instructions first.
- Treat `\cite{}`, `\ref{}`, `\label{}`, `\textbf{}`, LaTeX environments, escaped symbols, and `$...$` formulas as strong LaTeX evidence.
- Otherwise select the Word/plain-text variant when both variants exist.
- Preserve commands, formulas, symbols, and escaping exactly as required by the selected prompt.

## Apply the output contract

- Use the selected prompt's original section names, languages, formatting restrictions, and self-review procedure by default.
- Treat only output literally: do not add Markdown code fences, preambles, commentary, or labels that the prompt or user did not request.
- Let explicit user instructions override the original output format, length, language, or requested sections.
- Retain the selected prompt's substantive fidelity, rigor, and non-fabrication constraints after an override.
- Do not expose internal self-review text unless the selected output contract requests it.

## Handle compound requests

- Execute an explicit sequence such as “先缩写，再去 AI 味” in the stated order.
- Use the final stage's output contract unless the user specifies another format.
- If operations conflict and no order is given, ask one concise clarification instead of guessing.
- Do not load unrelated prompt sections.

## Handle missing or out-of-scope inputs

- Request only the missing source text, data, diagram requirements, paper file, or target venue needed to proceed.
- Never fabricate paper content, citations, experimental values, trends, or reviewer evidence.
- If both LaTeX and Word routes remain materially plausible, ask which format is intended.
- Do not force an unsupported request into one of these workflows.

Use `ml-paper-writing` instead for end-to-end paper drafting, citation verification, conference templates, or camera-ready preparation. Use generic humanizer skills for non-academic prose.

For origin and usage restrictions, read [references/provenance.md](references/provenance.md) only when provenance or redistribution is relevant.