# M6 — 趋势、权衡与判断

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

| | |
|---|---|
| **章节** | [19 Software Trends](https://yingang.github.io/aposd2e-zh/en/ch19.html) · [20 Designing for Performance](https://yingang.github.io/aposd2e-zh/en/ch20.html) · [21 Decide What Matters](https://yingang.github.io/aposd2e-zh/en/ch21.html) · [22 Conclusion](https://yingang.github.io/aposd2e-zh/en/ch22.html) |
| **中文** | [软件发展趋势](https://yingang.github.io/aposd2e-zh/ch19.html) · [性能设计](https://yingang.github.io/aposd2e-zh/ch20.html) · [决定什么是重要的](https://yingang.github.io/aposd2e-zh/ch21.html) · [结论](https://yingang.github.io/aposd2e-zh/ch22.html) |
| **核心问题** | 用 Ousterhout 自己的趋势判据给 vibe coding 打分。 |
| **前置** | **前面全部六个模块**，包括它们的 `findings.md` |
| **状态** | 未开始 |

---

## 读之前，停

**现在特别别读第 19 章** —— 这是全书被剧透代价最高的一章。在这一章里，Ousterhout 拿 agile
开发、单元测试、TDD、设计模式、getters 和 setters，逐个对照他花了十八章建立起来的判据打分。
有的过了，有的没过。**在给出你自己的评分之前读到他的评分，会把这个 capstone 变成同意练习。**

第 20–22 章可以照常在阶段 3 读。

## 核心问题

你花了六个模块建立一套判据。这个模块把它转向你每天在用的工具。

具体要求：**愿意接受一个你本来不想要的结论。**一门课如果用六个模块把 vibe coding 框定为风险、
然后结论是它是风险，那它什么都没证明 —— 它只是确认了自己的框定。**如果你 `findings.md` 里的
证据说那些诚实基线大多没问题，那就是发现**，它要进 verdict。

第 20 章提供了让这件事可能的纪律。它关于性能的那条规则 —— **测量，不要假设** —— 全力适用于
设计直觉，而这个模块就是把它施加到**本课程自己的主张**上的地方。每份 `findings.md` 都有一张
差异表，正是为此。

## vibe coding 在哪里失效

或者说，也许并没有。**这是唯一一个允许结论有利于它的模块。**

第 21 章问什么才真正值得投入注意力，而这正是本课程一直隐性推迟的问题。如果生成代码免费，某些
设计投资就不再回本：**为什么要精心设计一个你九秒钟就能重新生成的接口？**反驳是：重新生成很
便宜，但*理解*不便宜，而接口是理解的单位 —— 但这是一个**论证，不是证明**，而你在这里的工作就是
用你自己六个模块的数据检验它。

产出不是一条政策，而是一个**阈值**：你在哪些具体条件下放 agent 全速跑，在哪些具体条件下拦住
它。**具体到足以让你被证明是错的。**

## 学完你能

- [ ] 用第 19 章的判据给 vibe coding 打分，写下来，包含反面情形
- [ ] 说出在代码免费的前提下，设计投资的哪些部分还在回本、哪些不再回本
- [ ] 陈述你自己「该慢下来」的阈值，**具体到可被证伪**
- [ ] 论证 APOSD 在这个时代是需要修订，还是仅仅需要执行

## 实践题

### 第一部分 — 测量陷阱（Ch 20）

一轮短生成，让这个模块保持诚实而非纯回顾。

拿前面任何模块的代码，说 `「让它更快」`。别的什么都不说 —— 不给 profile，不给 benchmark，不说
什么慢。

然后**测量** agent 优化了什么、以及什么实际是热点。第 20 章的论证是：没有测量的优化是**多绕了
几步的猜测**，而一个被要求优化的 agent 永远能找到*某样东西*来改。那样东西是否要紧，是一个花十
分钟就能定案的实证问题。

### 第二部分 — 评分（Ch 19、21、22）

不写新代码。改为：把前面六份 `findings.md` 当作一个数据集读，写出
[`case-study/verdict.md`](case-study/)。它必须包含：

1. **用第 19 章判据给 vibe coding 打分** —— 用 Ousterhout 对待 agile 和 TDD 的同样待遇，同样
   愿意**把评分拆开**而不是给一个总分。
2. **证据表。**跨六个模块：诚实基线实际有多少次是糟的？哪些失效模式反复出现？哪些只出现过一次、
   再没出现？**数字从差异表里拿，不要靠回忆重建。**
3. **成本核算。**每份 `findings.md` 都记了生成、审查、重构各花多久。受约束的生成端到端是否比
   「不受约束然后修补」更便宜？这个问题多数人是靠感觉回答的，**而你现在有六个数据点**。
4. **你的阈值**，以可证伪的方式陈述。
5. **checklist 对书。**把 [`reference/review-checklist.md`](../../reference/review-checklist.md)
   和书自己的总结附录对比。**重叠证明推导有效。分歧要么是书因为写在 coding agent 之前而遗漏的
   东西** —— 那是有意思的结局 —— **要么是你从单个 case study 过度泛化了。分辨这两者，是整门课的
   最后一道练习。**

## 文件

| 路径 | 放什么 |
|---|---|
| [`socratic-log.md`](socratic-log.md) | 阶段 1–3：对话，蒸馏后的 |
| [`case-study/README.md`](case-study/README.md) | 第一部分的 brief |
| `case-study/{python,typescript}/before/` | 第一部分：未经测量的优化。不可变。 |
| `case-study/{python,typescript}/after/` | 第一部分：经过测量的那次，带数字 |
| [`case-study/findings.md`](case-study/findings.md) | 第一部分的 findings |
| `case-study/verdict.md` | **第二部分 —— capstone。**这个文件需要你创建。 |

## 完成条件

1. [ ] `socratic-log.md` 覆盖阶段 1–3，Grounding 有章节引用
2. [ ] 第一部分两种语言都有，带**实际测量数据**，不是估算
3. [ ] `verdict.md` 包含全部五节
4. [ ] verdict 引用具体的 `findings.md`，而不是笼统印象
5. [ ] **反面情形在场** —— 至少一处证据与你的先验相反
6. [ ] 根 [README](../../README.zh.md) 进度表已更新，课程标记为完成
