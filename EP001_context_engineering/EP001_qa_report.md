# EP001 QA Report — Context Engineering Slide Deck

生成日期:2026-10-02 · 工具链:ppt-master quick-generate(13 页 SVG → native PPTX → PowerPoint 导出 PDF/PNG)

## 1. Visual QA(全部 13 页逐页渲染审查)

渲染方式:PowerPoint COM 将最终 PPTX 逐页导出为 1600×900 PNG(即用户实际所见),逐页人工审查。

| 检查项 | 结果 |
|---|---|
| text overflow / clipping | 通过(P03 标题早期超宽 1% 已缩短修复) |
| overlapping | 首轮发现 S7 预算条内 "DYNAMIC CONTEXT" 与竞争项标签重叠 → 已修复(标签上移为段头);复检通过 |
| tiny text / contrast | 通过(最小字号 13px 仅用于 bar 内部项名与 gate 检验句,对比度 ≥4.5:1) |
| alignment / margins | 通过(13 页 kicker/hairline/页码位置一致) |
| Chinese font fallback / tofu | 通过(Microsoft YaHei / Consolas / SimSun 均正常渲染) |
| broken icon / SVG | 通过(36 个 tabler-outline 图标全部嵌入渲染) |
| 全页被栅格化 | 无 — 全部 native 形状/文本(仅 funnel、chevron 为原生 preset 形状) |
| 图像内异常文字 | 不适用(零 AI 生成图像) |

**结论:13/13 页通过**(S7 修复后重新导出并复验)。

## 2. Content QA(TRD §17 八问)

| # | 问题 | 结果 | 证据 |
|---|---|---|---|
| Q1 | 无来源的具体百分比/数字? | ✅ 无 | 预算条各段为示意宽度,未标任何百分比;无 benchmark、无固定 token 分配。唯一数字是封面 "1M Token" — 来自 episode spec 指定的 Hook 标题(Non-goal:讲者口播可泛化为"窗口已到百万级") |
| Q2 | 把 Context = Conversation History? | ✅ 否 | S02/S03/S09 明确"必要历史以已核验结论进入,而非全量对话" |
| Q3 | 把 Memory = Context? | ✅ 否 | S02 底注:"Memory / RAG / History 只是 Context 的候选来源,不是 Context 本身" |
| Q4 | 把 RAG = Context Engineering? | ✅ 否 | S02 中 RAG 仅作为候选来源节点出现,未与 CE 混同 |
| Q5 | 体现 Relevance ≠ Authority? | ✅ 是 | S06 整页:Authority×Relevance 象限 + 注入文本例("语义相关 ≠ 指令权威") |
| Q6 | 展示 Candidate Pool → Selection → Working Set? | ✅ 是 | S03(架构)、S08→S09(running example 的 before/after)、S05(五道 Gate) |
| Q7 | 解释 Compaction ≠ Context Engineering? | ✅ 是 | S12:压缩产物仍只是候选、仍要过 Compiler;本身有损;只是机制之一 |
| Q8 | 绝对化 / 越界 claim? | ✅ 无 | 全片措辞收敛("可能继续""更容易遗漏");D_budget 公式已注明"工程抽象,不是行业标准公式"(S07);无厂商特定 API 内容 |

## 3. Story QA(缩略图叙事线)

仅看 13 张缩略图可读出:Problem(1)→ Definition(2)→ Compiler(3)→ Selection(4-5)→ Conflict/Authority(6)→ Budget(7)→ Real Example before/after(8-9)→ Failure(10-11)→ Compression(12)→ Mental Model(13)。✅ 与 spec Narrative Arc 一致,未按源文档章节机械摘要。

## 4. 时长核算(TRD §20)

按 manifest 逐页 speaker time 合计 = **9:00**,落在 8:00–10:00 目标区间。✅

## 5. 来源纪律

- 事实主来源:M018(160_深读_AgentContextAssembly…V2-M018.md),已导入项目 `sources/`
- 三个层次已区分:source-supported fact(S02 六类存储、五维度、注入示例)、engineering abstraction(D_budget 公式)、explanatory example(修复登录 Bug 的 running example,spec 指定)
- 无网络补充内容(No-Web Default ✓);未虚构 benchmark/成功率/厂商特性
- Out of scope 边界遵守:Memory 架构、压缩算法、RAG 检索算法、Prompt Injection 防御体系均未展开

## 6. 已知未解决问题

无阻塞问题。两点备注:
1. S11 三张故障卡中部留白略大(表现列表与后果之间)——三卡一致,作为呼吸空间保留;
2. 引号字形:中文语境下的直引号("…")由 YaHei 渲染,如需书名号风格可后续统一替换。

## 7. 与 NotebookLM 原型对比

`上下文工程.pdf` 在本机未找到,按 TRD §21 条件未生成对比报告文件。基于 TRD §2 记录的已知问题的改进在最终汇报中列出。
