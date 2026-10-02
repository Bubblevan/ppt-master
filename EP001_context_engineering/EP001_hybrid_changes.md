# EP001 Hybrid Changes — NotebookLM 视觉资产吸收记录

日期:2026-10-03 · 基线:EP001_context_engineering.pptx(v1,保留未覆盖)· 产出:EP001_context_engineering_hybrid.pptx / .pdf

## 资产来源与处理

所有资产裁自 `D:\下载\上下文工程.pdf`(NotebookLM 原型,仅作 visual reference / illustration source,非事实来源),存放于项目 `images/notebooklm_reference/`,provenance 见 `build/.../images/image_sources.json`。裁切均为无关键文字区域或经梯度保持式擦除(背景竖条拉伸)的去字版本;未整页截图;未覆盖原 PDF。

| Asset | 来源页 | 处理 |
|---|---|---|
| hook_overloaded_context.png | P1 | 裁取左侧吊车+集装箱插画,排除右侧文字卡片 |
| storage_working_set.png | P2 | 裁取货架+聚光灯,擦除全部内嵌文字(deep/surface、货架标签、工作集标签) |
| context_compiler_machine.png | P3 | 裁取阀门管道机械带(本身无文字),去除边缘残块 |
| failure_noise.png | P6 | 裁取海浪插画(无文字),统一帧宽 |
| failure_staleness.png | P6 | 裁取机器人+新旧气泡插画(气泡内"测试已通过/测试失败"为插画语义保留) |
| failure_authority.png | P6 | 裁取 Malicious URL 撞击 SYSTEM PROMPT 插画(内嵌标签为隐喻载体保留) |
| compaction_machine.png | P7 | 裁取历史→压缩机→输出箭头,擦除底部三个阶段标签;排除右侧放大镜(含关键文字) |

## 逐页变更

### Slide 01 — visual-heavy
- 吸收:P1 吊车/超载集装箱插画,作为主 hero,置于深色封面右侧展示板(hairline 边框)。
- 保留 native:标题、kicker(episode metadata)、"大窗口 ≠ 好上下文"强调线、本期问题。
- 移除:v1 的 native 塞爆窗口隐喻块(由插画替代其表现职责);未保留 NotebookLM 文字卡片。

### Slide 02 — visual-heavy
- 吸收:P2 四货架+聚光灯插画(去字版)作为左侧主视觉。
- 新增 native:四个货架下方的 Conversation Logs / Memory / RAG / Search Index / Agent Checkpoints 标签(与图中货架对位)、MODEL-VISIBLE WORKING SET 徽章、右侧两张定义卡(STORAGE / CONTEXT ENGINEERING,含 M018 "一万段材料"表述)。
- 保留 native:页标题、两行核心陈述、底部"候选来源 ≠ Context"边界注。
- 移除:v1 的漏斗与六节点存储字段(选择语义由聚光灯隐喻 + S03 Compiler 承担)。

### Slide 03 — visual-heavy(轻量)
- 吸收:P3 阀门管道机械带(无文字),置入 Compiler 容器内部作为视觉 anchor,不承载信息。
- 保留 native:Candidate Pool 八项清单、汇流线、01–04 FILTER/RANK/BUDGET/ASSEMBLE 步骤条、输出深色框、全部箭头。

### Slides 04–10 — native(未改动)
- S04 ADMIT/DROP、S05 五道 Gate、S06 Authority×Relevance、S07 预算条(未引入 P4 的 15%/10%/10%/40%/25% 固定比例)、S08 Candidate Pool、S09 Working Set、S10 Bad vs Good — 保持 native system-diagram 风格,全部可编辑。

### Slide 11 — visual-heavy
- 吸收:P6 三幅故障隐喻插画分别置入三张故障卡(噪声=碎块巨浪;过期=机器人新旧状态冲突;权威=恶意内容越过信任边界)。
- 保留 native:卡片标题、编号、解释两行、后果行;移除 v1 的"表现"要点列表(语义并入解释行,信息等价)。
- 插画内嵌文字(测试已通过/测试失败、Malicious URL、SYSTEM PROMPT)为插画语义载体,与 native 文本零重叠。

### Slide 12 — visual-heavy
- 吸收:P7 历史→压缩机→输出箭头插画(阶段标签已擦除),配 native 阶段标签 Long History / COMPRESSION · 压缩。
- 保留 native:四条技术要点卡(控制增长/本身有损/不承担权威/只是机制之一)、三段 chevron 链(Candidate Information → Context Compiler → Model-visible Context,传达"压缩产物仍要过 Compiler")、EP002 teaser。
- 排除:P7 放大镜(内含"原文/压缩后"关键文字)。

### Slide 13 — minimal(未改动)
- 保持 v1 的 Append ✕ vs Compile 对比与宋体最终陈述,无插画。

## 视觉节奏(13 页)

- Visual-heavy:1、2、3、11、12(5 页)
- Native technical:4、5、6、7、8、9、10(7 页,其中 S07 偏概念图)
- Minimal:13(1 页)

## QA 复检(TRD 7 项)

1. 技术叙事保持:✅ 13 页 roster、顺序、技术内容与 v1 完全一致,仅视觉层变化。
2. 无整页栅格化截图:✅ 7 处插画均为局部 image,页面标题/图表/卡片仍为 native 对象(渲染检查确认)。
3. NotebookLM 内嵌文字与 native text 重叠:✅ 无——storage 标签带已擦除后由 native 标签对位;S01 文字卡片已裁除;S11 内嵌文字与 native 分区各置。
4. 不支持的数字:✅ NotebookLM P4 的 15%/10%/10%/40%/25% 未进入 deck(S07 维持无比例弹性预算条)。
5. 技术 diagram 可编辑:✅ S03/S08/S09/S12 的节点、箭头、chevron、卡片、公式均为 native 形状/文本。
6. 插画改善视觉层次:✅ S01 形成技术 YouTube 封面级钩子;S02 聚光灯隐喻直接承载"每轮选择";S11 故障卡获得记忆点;S12 压缩机器强化"手段"叙事。
7. 缩略图视觉节奏:✅ 见上方节奏分布,深色封面 → 浅色机制段(带两处插画)→ native 实例段 → 插画故障/压缩 → 极简收尾。

工具链复检:ppt-master final checker 0 error(1 条已接受的 advisory:S13 代码块逐行文本);导出 postflight passed;S01/S02 notes 已随视觉更新。

## 文件

- `EP001_context_engineering_hybrid.pptx` / `EP001_context_engineering_hybrid.pdf`(新,未覆盖 v1)
- `assets/slide_01–13.png`(hybrid 渲染图)
- `build/EP001_context_engineering_20261002/images/notebooklm_reference/`(7 个资产 + image_sources.json)

## 修订记录

- 2026-10-03 v1.1:字体统一——按用户要求移除 S09/S13 的 SimSun(宋体)引言字体,改为 Microsoft YaHei 加粗;全 deck 现仅 Microsoft YaHei(文本)+ Consolas(代码/公式)。重新过 final checker(0 error)、重导出 hybrid PPTX/PDF 并复验渲染。约定已沉淀至仓库 AGENTS.md「Local Workflow Notes」。
