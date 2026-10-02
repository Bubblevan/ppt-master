# AGENTS.md

This file is the project entry point for general AI agents.

**You MUST read [`skills/ppt-master/SKILL.md`](skills/ppt-master/SKILL.md) before any PPT generation task or repo modification.** It owns global execution discipline and points to the route selector; after routing, the selected runtime authority owns its steps, gates, and commands.

**Repository execution anchor**: resolve the absolute repository root from this
file's supplied path and retain the absolute `skills/ppt-master` root before the
first command. Paths in this file are repository-relative notation only; invoke
them through those absolute roots, retain the absolute project path returned by
initialization, and never issue `cd skills/ppt-master` or `cd projects/...`.
When parsing machine-readable stdout, keep stderr separate and never place
`2>&1` upstream of a JSON or XML parser. Invoke each such command once per
concrete argument set; never encode its executable or flag list in scalar shell
strings, batch it through a shell loop, or add a downstream parser when the
command provides a compact view.

## Project Overview

PPT Master turns source material into natively editable DrawingML PPTX. Generate has two mutually exclusive runtimes: Default Strategist → Image_Generator → Executor, and self-contained Quick without separate strategy/confirmation. Beautify selects from explicit Quick intent; Image to PPTX always uses Quick.

**Route selection authority**: [`skills/ppt-master/workflows/routing.md`](skills/ppt-master/workflows/routing.md) owns the three top-level artifact routes: Generate PPTX, Create Template, and Edit Native PPTX. Child workflows, profiles, stages, and governance documents refine one selected route; they are not competing top-level routes.

- Topic-only or fact-insufficient inputs run [`topic-research`](skills/ppt-master/workflows/stages/topic-research.md) inside the selected Generate profile's source intake; its facts URLs are not auto-expanded. After normal image search fails, one relevant webpage may be fetched as a source package and only reviewed selections enter the runtime image pool.
- Default Generate prepares template candidates internally in Step 3, then confirms the communication contract and free-design/template choice together in Stage 1. A template never rewrites the confirmed communication contract; selected roots are installed before template-aware Stage 2. Quick skips this interaction.
- Raw PPTX template plus new material/topic routes to [`edit-native-pptx`](skills/ppt-master/workflows/edit-native-pptx.md): a `pptx_to_svg.py --roundtrip` workspace where unchanged pages are referenced byte-for-byte and only planned pages are edited; it never enters Generate.
- Raw PPTX cannot be consumed as a Generate template workspace; run [`create-template`](skills/ppt-master/workflows/create-template.md) first and return with the generated workspace root as a Stage-1 candidate. Never add Master/Layout structure directly to an existing PPTX/SVG; generate new structured SVG pages from the workspace.
- Explicit quick/fast or skip-strategy generation uses [`quick-generate`](skills/ppt-master/workflows/profiles/quick-generate.md): prepare sources/resources as needed, decide without interaction, omit Strategist/confirmation/spec/lock, hand-author `svg_output/`, pass its lockless final checker, and export.
- Recorded, self-running, or video-directed Generate work conditionally loads [`video-design`](skills/ppt-master/references/video-design.md) inside the selected Default or explicit Quick runtime before page planning. It changes scene, script, and motion design—not the runtime/profile or artifact route.
- PPTX beautify is a strict 1:1 Generate [`profile`](skills/ppt-master/workflows/profiles/beautify-pptx.md), not a separate route. Explicit Quick intent uses the Quick runtime; otherwise it uses Default. Any split/merge/drop/reorder disables Beautify and returns to ordinary Generate in the selected runtime.
- Page-image reconstruction uses the Codex-supported, Quick-only [`image-to-pptx`](skills/ppt-master/workflows/profiles/image-to-pptx.md) profile. Normalize input page frames; one frame becomes one slide. Restore text natively, reconstruct low-resolution graphics without changing identity, and derive registered clean-base/scene layers. Padded-bbox-disjoint objects may share a generated plate and become independent crops. Never use a full-slide screenshot skin. Other hosts are unsupported.
- Finished PPTX notes / narration / timings / transitions with visible slides untouched also use [`edit-native-pptx`](skills/ppt-master/workflows/edit-native-pptx.md); export must report `rebuilt=0`.
- [`visual-review`](skills/ppt-master/workflows/stages/visual-review.md), [`customize-animations`](skills/ppt-master/workflows/stages/customize-animations.md), and [`generate-audio`](skills/ppt-master/workflows/stages/generate-audio.md) are supporting stages; their trigger rules remain explicit/conditional.

## Execution Requirements

- For any `brand`, `style`, `layout`, or `deck` workspace creation from PPTX/SVG, images/PDFs, documents/websites, brand assets, direct text, or mixed references, enter [`skills/ppt-master/workflows/create-template.md`](skills/ppt-master/workflows/create-template.md); it keeps the fixed Create Template name and dispatches exactly one of [`create-brand`](skills/ppt-master/workflows/create-template/create-brand.md), [`create-style`](skills/ppt-master/workflows/create-template/create-style.md), [`create-layout`](skills/ppt-master/workflows/create-template/create-layout.md), or [`create-deck`](skills/ppt-master/workflows/create-template/create-deck.md).
- Always-on SVG constraints and shared visual-quality defaults live in [`skills/ppt-master/references/shared-standards-core.md`](skills/ppt-master/references/shared-standards-core.md). Default and Quick Generate load [`svg-effects.md`](skills/ppt-master/references/svg-effects.md) on the executor-base routing trigger (the everyday effects live in the executor core); other routes load it, [`native-data-interface.md`](skills/ppt-master/references/native-data-interface.md), and [`pptx-structure-interface.md`](skills/ppt-master/references/pptx-structure-interface.md) only when their documented execution triggers apply.
- Canvas choices live in [`skills/ppt-master/references/canvas-formats.md`](skills/ppt-master/references/canvas-formats.md).
- Icon library details live in [`skills/ppt-master/templates/icons/README.md`](skills/ppt-master/templates/icons/README.md).

## Required Conventions

- **Repo-wide style rules** — when editing prompt files under [`skills/ppt-master/references/`](skills/ppt-master/references/), Python under [`skills/ppt-master/scripts/`](skills/ppt-master/scripts/), or any other code/prose in the repo, follow the matching style rule in [`docs/rules/`](docs/rules/).
- **Prompt content layers** — follow [`docs/rules/prompt-layers.md`](docs/rules/prompt-layers.md): a prompt file holds craft (design judgment) and the minimal contract the model writes; enforced grammar, importer behavior, and restated procedure live in [`scripts/docs/`](skills/ppt-master/scripts/docs/), one owner per rule with pointers elsewhere.
- **Prompt decision ownership** — follow [`docs/rules/ownership.md`](docs/rules/ownership.md); every cross-file rule has one owner recorded in [`docs/rules/rule-owners.md`](docs/rules/rule-owners.md). Default Strategist prepares project-local resources and Executor realizes them; Quick's current agent decides and prepares before SVG authoring. This is not downstream acquisition. Every project icon is prepared material; `icons.inventory` indexes the default plan's curated bundled pool, not page usage or an execution whitelist. Sounds follow [`animations.md`](skills/ppt-master/references/animations.md) §2.2.
- **Markdown language consistency** — follow [`docs/rules/language.md`](docs/rules/language.md): one language per file, mirroring the siblings in that directory; a non-English string may appear in an English file only as quoted content (user trigger text, sample values, rendered labels, proper nouns), never as the wording of a rule; never hard-code which language the model replies in. Chat replies are unaffected.

## Compatibility Boundary

- This repository is a workflow/skill package, not an app or service scaffold.
- Do NOT assume generic-project conventions like `.worktrees/`, CI, or mandatory branch setup unless the user explicitly requests them. The only test location is `skills/ppt-master/scripts/tests/` under the conditions in [`docs/rules/code-style.md`](docs/rules/code-style.md) §11.
- On conflict with a generic coding skill, prioritize [`skills/ppt-master/SKILL.md`](skills/ppt-master/SKILL.md) inside this repository.

## Command Quick Reference

Convenience summary only — route selection starts in [`SKILL.md`](skills/ppt-master/SKILL.md). Image to PPTX always uses [`quick-generate.md`](skills/ppt-master/workflows/profiles/quick-generate.md); Beautify uses it only when Quick is explicit, otherwise [`generate-pptx.md`](skills/ppt-master/workflows/generate-pptx.md).

```bash
python3 skills/ppt-master/scripts/source_to_md.py <file_or_URL_or_dir> [...]          # source conversion
python3 skills/ppt-master/scripts/project_manager.py init <project_name>              # --format only for an exact registered canvas
python3 skills/ppt-master/scripts/project_manager.py import-sources <project_path> <sources...>
python3 skills/ppt-master/scripts/project_manager.py validate <project_path>
python3 skills/ppt-master/scripts/icon_sync.py <project_path> <lib/name> [...]        # missing names -> non-zero = re-pick
python3 skills/ppt-master/scripts/confirm_ui/server.py <project_path> --daemon        # then --wait-only --wait-stage stage1
python3 skills/ppt-master/scripts/analyze_images.py <project_path>/images
python3 skills/ppt-master/scripts/image_gen.py --manifest <project_path>/images/image_prompts.json   # in-pipeline AI images, even for 1
python3 skills/ppt-master/scripts/svg_editor/server.py <project_path> --live --daemon
python3 skills/ppt-master/scripts/svg_quality_checker.py <project_path> --canonical-authoring --stage final --json   # Quick adds --quick-generate; --json writes the report the exporter reads, stdout stays the summary
python3 skills/ppt-master/scripts/pptx_to_svg.py <source.pptx> -o projects/<slug>_<YYYYMMDD> --inheritance-mode both --roundtrip   # Edit Native PPTX
python3 skills/ppt-master/scripts/svg_to_pptx.py projects/<slug>_<YYYYMMDD> --roundtrip
```

Every other command (sound sync, slicing, template materialization and preview, animation config, authoring-view refresh) is listed by the route or stage that owns it and in [`svg-pipeline.md`](skills/ppt-master/scripts/docs/svg-pipeline.md).

For Generate PPTX serial post-processing and export, follow [`generate-pptx.md`](skills/ppt-master/workflows/generate-pptx.md) Step 7 exactly; Edit Native PPTX exports through its own §7. See [`svg-pipeline.md`](skills/ppt-master/scripts/docs/svg-pipeline.md) for tool flags and behavior.

## Core Directories

- `skills/ppt-master/SKILL.md` — global discipline and route-entry authority.
- `skills/ppt-master/workflows/generate-pptx.md` — Generate PPTX Step 1–7 authority.
- `skills/ppt-master/references/` — role cores plus conditionally loaded role and technical modules.
- `skills/ppt-master/scripts/` — runnable tool scripts.
- `skills/ppt-master/scripts/docs/` — topic-focused script docs.
- `skills/ppt-master/templates/` — layout templates, chart templates, icon library, brand presets.
- `skills/ppt-master/workflows/` — top-level route authorities plus supporting child workflows, profiles, stages, and governance runbooks.
- `docs/` — user-facing documentation (FAQ, installation, technical design, templates guide, audio narration).
- `docs/rules/` — repo-wide style rules.
- `projects/` — user project workspace.

---

## Local Workflow Notes (fork-specific, Bubblevan)

> 本节是仓库所有者(Bubblevan)的本地工作流沉淀,不属于上游 ppt-master 规范;rebase 上游时如冲突,保本节内容。与上游 skill 权威文件冲突时以上游为准;本节只补充"这台机器 + 这套个人流程"的约定。

### 工作区与环境(硬约定)

- **所有工作区、项目、临时文件一律放本仓库内**(如 `EP001_context_engineering/`、`projects/`),绝不写 C 盘;产出物不要散落到 `Documents`。
- **Python 统一用 `D:\MyLab\ppt-master\.venv\Scripts\python.exe`**(已按 `requirements.txt` 装好 skill 全部依赖)。本机 PATH 很乱:`python` 指向 hermes-agent 的 venv、`python3` 是失效的 Microsoft Store 占位符、`pip` 指向 Anaconda base——三者都不要用;skill 文档里的 `python3 ...` 命令一律替换成 `.venv` 的 python 绝对路径。
- **PDF 导出与视觉验收**:本机装有 PowerPoint,用 COM 自动化(`SaveAs 32` 出 PDF,`Slide.Export` 逐页出 PNG)。视觉验收以 PowerPoint 渲染出的 PNG 为准,不要只看 SVG/XML。
- 本仓库 remote `upstream` 指向我自己的 fork(Bubblevan/ppt-master),同步真正的上游时另加别的 remote 名。

### 偏好管线:NotebookLM 原型 → PPT Master 正式版

以后知识类视频 deck 大多走这条两段式流程:

1. **NotebookLM 先生成一版原型 PDF**(约 8 页)。它只是 *visual reference / illustration source / 叙事 baseline*,**不是事实来源**;内容 authority 是研究 markdown(如 `LLM-Agent百科全书/M018`)+ episode spec。原型里无来源的固定百分比、绝对化结论**禁止**带入正式版。
2. **PPT Master quick-generate 出 native 骨架**(explicit quick 意图,免交互):先冻结 13 页左右的 roster 和每页认知任务,保证结构与叙事完整、全 native 可编辑。
3. **第二轮视觉吸收**(hybrid):从原型 PDF 裁插画作为独立 image asset,放进 `images/notebooklm_reference/`,配 `image_sources.json`(license_tier: no-attribution)。

### NotebookLM 资产制作经验(踩过的坑)

- 用 PyMuPDF 2x 渲染整页,再 PIL 裁切。**先渲染放大、量准文字 bbox 再裁**——EP001 连续三次因目测坐标出错(标签是双行的、比预估宽、机器底座被切掉);每次裁完立刻查看渲染图检查,不要批量盲裁。
- **擦内嵌文字**用"同高度无字竖条横向拉伸"补丁(渐变背景不留痕),不要用纯色方块填充;克隆源本身可能含文字(曾把 'deep layer' 克隆成双份、把显示器碎片贴到别处)。
- 允许:裁无关键文字的插画区、把插画当独立 asset、按参考图重构。禁止:整页截图当 slide 背景、用图中文字替代 native text、内嵌文字与 native text 重叠。**含关键教学文字的区域整块排除**(如放大镜里的"原文→压缩后"对比、右侧文字卡);纯装饰性块标签(箱子上的"几百页 PDF")可保留;有叙事语义的内嵌文字(如"测试已通过/测试失败"气泡)可保留但必须与 native 文本分区。
- 并列结构的多张插画(如三张故障卡)**必须用完全相同的 crop 帧高**,否则破坏 parallel exposition。
- 视觉节奏配比:visual-heavy 约 5 页(封面/开场架构/结尾前的机制页)+ native 技术页 7 页 + minimal 收尾 1 页,效果很好;不要每页都塞插画。

### SVG/工具链细节(免得再查)

- `image_sources.json` 必须是 `{"items": [...]}`,且 `filename` 是**裸文件名**(不能带 `notebooklm_reference/` 前缀,子目录只出现在 SVG 的 `href` 里);`analyze_images.py` 的参数是 images 子目录本身。
- SVG 文本:一个段落 = 一个 `<text>` + 定位 `<tspan>`(兄弟 `<text>` 会被判段落拆分告警);**悬挂缩进的代码行必须逐行独立 `<text>`**(checker 明确要求)。写坐标前先跑 `text_measure.py calibrate` 并用速率表估宽,CJK+Latin 混排分行计算。
- 根组 `data-pptx-bounds` = 子元素几何并集 + margin;相邻根组留 ≥2px;把箭头/连线归组时先算它的 bounds 会不会和邻居重叠(EP001 在 S06/S08/S11 栽过)。
- preset 形状(funnel/chevron 等)用 `preset_shape_svg.py render-batch` 生成后整组可 transform(rotate/平移),但**永远不要手改 registry path**;漏同步 icon 会在 checker 报 "Project-local icon not found",单独 `icon_sync.py` 补。
- **字体约定:全 deck 只用 Microsoft YaHei(文本)+ Consolas(代码/公式),不要混入宋体/SimSun**——引言、金句也用雅黑加粗(用户明确偏好,EP001 已返工)。
- 深底页不投黑色阴影(用 hairline 或亮色描边);editorial 风格下阴影克制到 0(规则与线分隔)。
- checker 剩余 warning 的取舍:sibling-paragraph 告警(代码块逐行)是可接受形态;noncanonical hoist 类建议顺手修(把共享 fill/字号提升到 `<g>`)。

### 修订节奏

改 SVG 后的固定循环:`svg_quality_checker.py --quick-generate --canonical-authoring --stage final --json` → `svg_to_pptx.py --quick-generate --with-notes` → COM 出 PDF + 渲染 PNG → 逐页看图。历史导出版本保留在 `exports/`,交付物在项目根目录用语义文件名(hybrid 版不覆盖 v1)。
