# Vibe APOSD

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

**一门用苏格拉底式教学法讲「AI 生成代码时代的软件设计」的课程。**

教材：*A Philosophy of Software Design*（第二版），John Ousterhout 著。
22 章，7 个模块，每个模块用现场生成的 AI 代码做一个 case study。

---

## 这门课为什么存在

Ousterhout 的核心主张与打字速度无关。它是这句话：限制我们构建软件的最大因素，是
**我们理解自己所造系统的能力**。复杂性的定义是结构性的 —— 系统形状中任何让它难以理解、
难以修改的东西。

现在看 AI coding agent 改变了什么，又留下了什么没动：

| | agent 之前 | 有了 agent |
|---|---|---|
| **生产**代码的成本 | 高 | 接近零 |
| **理解**代码的成本 | 高 | **没变** |
| 什么在限制复杂性增长 | 你的打字速度、你的耐心 | **没有东西在限制** |

过去拖慢复杂性的那点摩擦从来不是设计保障 —— 它是个意外。摩擦一去，复杂性就以你能敲出
prompt 的速度累积。

这本书在第 3 章已经给出了精确的词汇。Ousterhout 区分 **tactical** programming（优化「让
这个现在能跑」）和 **strategic** programming（投资于一个能持续可用的设计）。他说的
*tactical tornado*，是那种交付速度惊人、留下一地残骸给别人过日子的开发者。

> AI coding agent 在构造上就是个 tactical programmer。它优化眼前这个 prompt，对下个季度的
> 维护负担毫无利害关系，而且永远不会累。如果你不提供 strategic intent，就没有人提供。

所以人的工作转移了。少写代码，多**指定约束、审查结构**。APOSD 是这两半工作共同的词汇表。
这就是为什么是这本书，为什么是现在。

## 为什么用苏格拉底式，而不是给你一份清单

有个很强的诱惑是直接跳到答案：把 Ousterhout 的原则抽成 bullet list，粘进 system prompt，
收工。很多人试过。不行。

**清单不是能力。**能力是在凌晨 11 点、代码就在你屏幕上、所有测试都过了的时候，**认出**这是
个 shallow module、这里 abstraction 漏了、这条注释没有信息量。认出这件事无法靠断言转移，
只能靠在你即将犯错的那一刻被问对问题。

所以这门课从不以结论开场。它先给一个你已经有看法的场景，一直追问到你的答案要么崩掉、
要么你能说清它为什么成立，然后才让你去读文本，看看 Ousterhout 是否同意。

## 教学循环

每个模块都跑同样的六个阶段。

| 阶段 | 发生什么 | 产出 |
|---|---|---|
| 1. **直觉** | 老师给一个具体场景。你凭经验回答。**先不读书。** | `socratic-log.md` |
| 2. **追问** | 一直追到你的直觉崩掉，或者你能说清它为何成立。 | `socratic-log.md` |
| 3. **回到文本** | 你在章节里找到那个论证，用自己的话陈述原则。 | `socratic-log.md` |
| 4. **生成** | 你给 AI agent 一个真实任务，**故意不加任何设计约束**。保留原始输出。 | `case-study/*/before/` |
| 5. **审查与重构** | 应用本模块的原则。**先批评，再改码。**记录差异。 | `case-study/*/after/`、`findings.md` |
| 6. **提炼** | 把你不得不对 agent 说的话，蒸馏成一条可复用的约束。 | `prompts/` |

**让阶段 4 有意义的那条规则：**agent 必须产出它的*诚实默认输出*。如果你在生成 prompt 里
偷偷夹带设计指导，case study 就不再是证据，而变成了一场演示。**故意随便地生成** —— 那才是
实验。

完整机制和 definition of done 见 [modules/README.zh.md](modules/README.zh.md)。

## 课程结构

| 模块 | 章节 | 核心问题 | 对应的 vibe coding 失效 |
|---|---|---|---|
| [M0 — 复杂性](modules/m0-complexity/README.zh.md) | 1–3 | 复杂性从哪来？为什么「能跑」不是终点线？ | 生成的代码第一天过测试，第三十天改不动了 |
| [M1 — 深模块](modules/m1-deep-modules/README.zh.md) | 4–6 | 什么让模块变深？什么该藏在接口后面？ | 在 agent 动手**之前**如何定义模块边界 |
| [M2 — 抽象与分层](modules/m2-abstraction-layers/README.zh.md) | 7–9 | 谁来吸收复杂性？这该是一个东西还是两个？ | agent 产出扁平一把梭函数，或 pass-through 链 |
| [M3 — 设计流程](modules/m3-design-process/README.zh.md) | 10–11 | 能靠重新定义语义删掉一整类 bug 吗？ | 在 prompt 里强制「先设计后写码」 |
| [M4 — 注释与命名](modules/m4-naming-comments/README.zh.md) | 12–15 | 注释必须承载什么代码承载不了的信息？ | 逐行复述代码的注释 |
| [M5 — 一致性与修改](modules/m5-consistency-maintenance/README.zh.md) | 16–18 | 如何在改动系统时不破坏它的设计？ | agent 最危险的操作：改它没写过的代码 |
| [M6 — 趋势与权衡](modules/m6-trends-tradeoffs/README.zh.md) | 19–22 | Ousterhout 给 agile、TDD、设计模式打过分。现在给 vibe coding 打分。 | 什么时候放 agent 跑，什么时候拦住它 |

逐章拆解和分组理由见 [CURRICULUM.zh.md](CURRICULUM.zh.md)。

## 目录结构

```
.
├── README.md          课程论点、方法、结构总表（英文，权威版）
├── CLAUDE.md          给「扮演老师的 agent」的操作规程
├── CURRICULUM.md      22 章映射到 7 模块，含分组理由
├── modules/           每个模块一个目录；接口相同，内容不同
│   └── mN-name/
│       ├── README.md       章节、核心问题、学习目标、实践题
│       ├── socratic-log.md 对话，蒸馏成教学素材
│       └── case-study/     AI 生成的代码、批评、重构
│           ├── python/
│           └── typescript/
├── prompts/           从各模块提炼出的「设计约束型」prompt 模板
├── templates/         log / case study / findings / prompt 的空表
└── reference/         教材章节索引；我们自己长出来的 review checklist
```

**每个模块目录暴露完全相同的三件套接口，各自把自己的混乱藏在后面。**这是第 4、5 章在文件
系统层面的应用 —— 一门讲信息隐藏的课程，没有立场把自己组织得很乱。

## 怎么用这个仓库

**自己上这门课。**Clone 下来，用能读项目指令的 agentic 工具打开
（[Claude Code](https://claude.com/claude-code)，或任何读 `CLAUDE.md` / `AGENTS.md` 的
工具），说一句 *「开始 M0」*。agent 会从 [CLAUDE.md](CLAUDE.md) 接过老师角色、硬性规则和
六阶段循环。**按顺序走** —— 后面的模块依赖前面建立的词汇。

**读别人跑完的记录。**那些 `socratic-log.md` **就是**课程本身。把它们当推理过程的记录读，
不要当文档读。case study 是那套推理经受住真实代码检验的证据。

**只想拿走有用的部分。**`prompts/` 和 `reference/review-checklist.md` 是可携带的产出。它们
被刻意放在最后写，因为**一条你没亲眼见它失败过的约束，只是迷信**。

## Case study 约定

每个 case study 都出 **Python** 和 **TypeScript** 两版。这两版不是互相翻译 —— 它们是一组
对照实验。动态语言把 interface complexity 赤裸地暴露出来，没有编译器帮你拦。静态语言把一部分
复杂性搬进签名里，使它*可见*；又把另一部分藏进类型系统里，使它*不可见*。看同一个设计失效在
两边落地方式的差异，本身就是课程的一部分。

## 教材与出处

*A Philosophy of Software Design*, 2nd edition — John Ousterhout, Yaknyam Press。

社区翻译项目把两个语言版本并排发布，所以无论你读哪一版这门课都能用：

- **英文：**<https://yingang.github.io/aposd2e-zh/en/>
- **中文：**<https://yingang.github.io/aposd2e-zh/>
- **22 章全索引，附每章在本课程中的用途：**[reference/aposd-map.md](reference/aposd-map.md)

本仓库**引用并与书争论**，不复制它。原书没有替代品，而且原书很短。**去买。**

## 语言约定

课程的**工作产出全部用英文**（`socratic-log.md`、`findings.md`、代码、commit message），
这样对更多人有用。**入口文档**（本文件、CURRICULUM、7 个模块 brief）另有中文平行版本，
方便中文读者判断和上手 —— 英文版是权威版本。

上课本身可以用任何语言。log 记录的是*推理*，不是逐字对话。技术术语在任何语境下都保持英文。

## 进度

| 模块 | Socratic log | Case study | 提炼的 prompt |
|---|---|---|---|
| M0 — 复杂性 | 未开始 | 未开始 | — |
| M1 — 深模块 | 未开始 | 未开始 | — |
| M2 — 抽象与分层 | 未开始 | 未开始 | — |
| M3 — 设计流程 | 未开始 | 未开始 | — |
| M4 — 注释与命名 | 未开始 | 未开始 | — |
| M5 — 一致性与修改 | 未开始 | 未开始 | — |
| M6 — 趋势与权衡 | 未开始 | 未开始 | — |

## 许可

本仓库的课程材料：[MIT](LICENSE)。教材不属于我们，也不包含在这里。
