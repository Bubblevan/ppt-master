# EP001 Slide Manifest — Context Engineering

| Slide | Purpose(认知任务) | Main Visual(主视觉) | Source Section(来源) | Speaker Time |
|---|---|---|---|---|
| 01 | 打破"窗口大就不用做 Context Engineering"的直觉,抛出全片核心问题 | 深色封面:被各类材料塞爆并溢出的 Context Window 框 | M018 阅读主线 / Anthropic context engineering 观点;Spec Slide 01 | 30s |
| 02 | 建立 Storage(系统知道什么)与 Model-visible Working Set(模型此刻看到什么)的区分 | 左侧 6 项存储字段 → 漏斗(选择)→ 右上工作集;底部"候选来源≠Context"边界注 | M018-Q1(存储范围 vs 模型可见范围);Spec Slide 02 | 40s |
| 03 | 给出全片统一架构:Context Compiler 的输入、四步动作与输出 | 8 项候选清单 → 汇流 → 编译器(FILTER/RANK/BUDGET/ASSEMBLE)→ 深色工作集输出框 | M018-Q10 Assembler 流程 + 阅读主线"编译成下一步输入";Spec Slide 03 | 45s |
| 04 | 把"选择"落到具体决策:同一候选池中谁进谁出 | ADMIT / DROP 两列四张 ContextCard(来源/相关性/时效状态 badge + 判定章) | M018-Q4(硬约束保留、失效状态、决策影响);Spec Slide 04 | 40s |
| 05 | 说明五个选择维度,并强调维度之间会冲突 | 候选材料穿过五道 Gate(RELEVANCE/AUTHORITY/FRESHNESS/PERMISSION/TOKEN COST)+ 四个冲突示例卡 | M018-Q4 打分维度与冲突;Spec Slide 05 | 50s |
| 06 | 展开"最相关 ≠ 最有权威":指令/证据/不可信内容不能按相关性混层 | Authority × Relevance 二维象限四卡,含 "Ignore previous instructions" 注入文本示例 | M018-Q9(Prompt Injection、来源标签、权限分层);Spec Slide 06 | 40s |
| 07 | 解释为什么窗口再大也需要预算;给出预算记账的工程抽象 | 分段预算条(System/Task/Tools/Dynamic Context/Output Reserve)+ D_budget = W−S−U−T−R(已注明工程抽象) | M018-Q2(Token Budget 记账模型,硬约束 vs 软预算);Spec Slide 07 | 45s |
| 08 | 首次完整呈现 running example:第 6 轮调用前的全部候选 | 左侧 Round 1–5 执行时间线 + 右侧 11 项 Candidate Pool 双列 | M018-Q10 Coding Agent 分阶段上下文;Spec Slide 08 | 40s |
| 09 | 展示选择的结果:IN 的最小充分集与 OUT/DOWNWEIGHT | 候选堆 → COMPILE → 7 项 Working Set;5 个 OUT 胶囊;宋体金句"不是最少,而是充分" | M018-Q5(混合方案、按任务装配);Spec Slide 09 | 50s |
| 10 | 把 Context 质量与 Agent 行为直接挂钩 | 中央模型节点 + 左 BAD / 右 GOOD 两份上下文汇入,底部两种"下一步"后果带 | M018-Q4/Q5(质量决定行动);Spec Slide 10 | 40s |
| 11 | 系统化三种失败模式,收束"越多越好"的反例 | 三列故障卡:NOISE / STALENESS / AUTHORITY(表现 + 后果) | M018-Q7(过度压缩表现)+ Q9(注入/过期);Spec Slide 11 | 45s |
| 12 | 界定 Compaction 的位置:控制增长的手段,有损、不承担权威 | 五段 chevron 流水线:Long History → Summarize/Compress/Evict/Reload → Candidate Information → Context Compiler → Model-visible Context + EP002 teaser | M018-Q6(Compaction 保留物、流程)+ Q8(与 checkpoint 区分);Spec Slide 12 | 45s |
| 13 | 收束为统一心智模型:Compile, not Append | 左 APPEND 代码块(红叉)vs 右 COMPILE 代码块;宋体最终陈述 | M018 阅读主线 + One-Sentence Thesis;Spec Slide 13 | 30s |

**Total: 9:00**(目标区间 8:00–10:00 ✓;spec 时长表逐页合计 540s)

## 全片统一元素

- Running example:P08–P12 全部围绕"修复登录 Bug 且测试不回归"的第 6 轮调用展开
- 统一组件:ContextCard(白卡+细边+来源/维度 badge)、SourceBadge、kicker/hairline/页码 chrome
- 语义色:teal=入选/编译器,green=admitted,gray=storage/dropped,amber/red=stale/conflict/risky
- 方向语义:Candidate → Compiler → Working Set 全片一致从左到右

## Notes

每页 speaker notes 为 prose 讲解要点(非逐字稿),覆盖该页全部信息组;完整记录于 PPTX 备注栏与 `build/EP001_context_engineering_20261002/notes/`。
