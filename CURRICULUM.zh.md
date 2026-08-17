# 课程结构

[English](CURRICULUM.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [CURRICULUM.md](CURRICULUM.md) 为准。

*A Philosophy of Software Design*（第二版）全部 22 章，分成 7 个模块。一章不落。

每章都给出中英双链（[英文](https://yingang.github.io/aposd2e-zh/en/) ·
[中文](https://yingang.github.io/aposd2e-zh/)）。22 章的统一索引，附每章在本课程中的用途，
见 [reference/aposd-map.md](reference/aposd-map.md)。

---

## 分组是怎么定的

最直白的做法是把书切成七等份。这几乎就是对的 —— 因为 Ousterhout 自己已经把材料分好组了 ——
但有两处调整很重要。

**第 19 章属于结尾，不属于维护那一组。**「Software Trends」是 Ousterhout 拿 agile、TDD、
设计模式、getters/setters 逐个对照自己的判据打分的一章。它是一章*判断*，不是一章*技术*。
把它放到最后，意味着你花六个模块建立一套判据，然后拿这套判据去审判自己每天在用的工具。
对一门讲 vibe coding 的课来说这是最强的结尾，而如果它只是作为第 18 章的脚注出现，这个价值
就浪费了。

**第 16–18 章是一个想法，不是两个。**修改现有代码（16）、一致性（17）、易理解（18）回答的
是同一个问题：一个系统在被并非其设计者的人不断改动时，如何保持连贯？这也正是一个 agent 在
它从未见过的代码库里做修改时提出的问题 —— 这让这个模块在本课程中承重异常大。

其余部分沿着书自己的自然接缝走。

## 顺序

模块按**依赖关系**排序，不按难度。后面的模块依赖前面建立的词汇，跳着看会读不通：

- **M1–M2 需要 M0 的复杂性定义。**在你能说清复杂性*是什么*、以及为什么「能跑」不是终点线
  之前，“deep module” 这个词毫无意义。
- **M4 需要 M1 的信息隐藏。**agent 的注释之所以没价值，不是因为写得差 —— 而是因为一条复述
  代码的注释不携带任何代码尚未携带的信息。这个论证需要 M1 打底。
- **M5 需要 M2 的分层。**没有「这个改动属于哪一层」的模型，你无法审计一个 diff 的一致性
  断裂。
- **M6 需要全部**，因为给一个趋势打分，前提是判据已经存在。

---

## M0 — 复杂性的本质

**目录：**[`modules/m0-complexity/`](modules/m0-complexity/README.zh.md)

| 章 | 英文 | 中文 |
|---|---|---|
| 1 | [Introduction](https://yingang.github.io/aposd2e-zh/en/ch01.html) | [介绍](https://yingang.github.io/aposd2e-zh/ch01.html) |
| 2 | [The Nature of Complexity](https://yingang.github.io/aposd2e-zh/en/ch02.html) | [复杂性的本质](https://yingang.github.io/aposd2e-zh/ch02.html) |
| 3 | [Working Code Isn't Enough](https://yingang.github.io/aposd2e-zh/en/ch03.html) | [能工作的代码是不够的](https://yingang.github.io/aposd2e-zh/ch03.html) |

**核心问题。**复杂性到底从哪来，为什么「能跑」不是终点线？

**vibe coding 在哪里失效。**生成的代码第一天过测试，第三十天改不动了。所有人都经历过。几乎
没人能说出**机制**。第 2 章点了三个名字 —— change amplification、cognitive load、
unknown unknowns —— 而第三个在有 agent 的情况下最要紧，因为它是唯一一个**你无法通过阅读
被展示给你的代码来发现**的。

**学完你能：**

- 指着真实 diff 里的某一行，说出它产生了三个症状中的哪一个
- 解释为什么 agent 在构造上就是 tactical，而不是偶然是
- 论证：当生成代码免费时，strategic programming 还买得到吗
- 说出你自己的工作流必须改掉哪一件事，才买得到它

**实践题形状。**让 agent 造点小而诚实的东西 —— 一个读 CSV 订单、打印汇总的 CLI。然后追加
三次它事先不知道的需求。**复杂性不出现在第一次生成里，它出现在序列里。**这就是第 2 章的全部
要点，而一次性的 case study 无法展示它。

---

## M1 — 深模块

**目录：**[`modules/m1-deep-modules/`](modules/m1-deep-modules/README.zh.md)

| 章 | 英文 | 中文 |
|---|---|---|
| 4 | [Modules Should Be Deep](https://yingang.github.io/aposd2e-zh/en/ch04.html) | [模块应该是深的](https://yingang.github.io/aposd2e-zh/ch04.html) |
| 5 | [Information Hiding (and Leakage)](https://yingang.github.io/aposd2e-zh/en/ch05.html) | [信息隐藏和信息泄露](https://yingang.github.io/aposd2e-zh/ch05.html) |
| 6 | [General-Purpose Modules are Deeper](https://yingang.github.io/aposd2e-zh/en/ch06.html) | [通用的模块是更深的](https://yingang.github.io/aposd2e-zh/ch06.html) |

**核心问题。**什么让一个模块变深？你怎么决定什么该藏在接口后面？

**vibe coding 在哪里失效。**「写个 helper 处理 X」是一条关于*实现*的指令，它可靠地产出一个
shallow module：接口几乎和它包裹的函数体一样复杂。修复点在代码生成的**上游** —— 在于你如何
在 agent 动手之前指定边界。这个模块是课程从「事后 code review」转向「prompt 设计」的地方。

**学完你能：**

- 认出 shallow module，并说出让它成为 shallow 的那个 interface-vs-implementation 成本
- 在两个看起来互相独立的模块之间找到 information leakage
- 判断一个抽象是过于通用、过于专用，还是「适度通用」
- 写出一段既指定了边界、又没指定实现的任务描述

**实践题形状。**给 HTTP client 加 rate limiting。这是教科书级的深度测试：朴素版会把算法从
接口漏出去，而深的版本把一个真正困难的问题藏在大约两个方法后面。对比 agent 在收到「加个
rate limiting」时的产出，和收到一份接口契约时的产出。

---

## M2 — 抽象与分层

**目录：**[`modules/m2-abstraction-layers/`](modules/m2-abstraction-layers/README.zh.md)

| 章 | 英文 | 中文 |
|---|---|---|
| 7 | [Different Layer, Different Abstraction](https://yingang.github.io/aposd2e-zh/en/ch07.html) | [不同的层级，不同的抽象](https://yingang.github.io/aposd2e-zh/ch07.html) |
| 8 | [Pull Complexity Downwards](https://yingang.github.io/aposd2e-zh/en/ch08.html) | [下沉复杂性](https://yingang.github.io/aposd2e-zh/ch08.html) |
| 9 | [Better Together Or Better Apart?](https://yingang.github.io/aposd2e-zh/en/ch09.html) | [在一起更好还是分开更好？](https://yingang.github.io/aposd2e-zh/ch09.html) |

**核心问题。**谁来吸收复杂性？这该是一个东西还是两个？

**vibe coding 在哪里失效。**这个模块有意思，因为 agent **两个方向都会翻车**。要一个功能，
经常拿到一个干五件事的扁平函数。要「clean architecture」，经常拿到四个类、每个方法都在往
下一个转发 —— 一条 pass-through 链，加了名字却没加任何新抽象。两者都是分层失效，但诊断
不同。

**学完你能：**

- 叫出 pass-through method、pass-through variable、decorator class 的名字
- 从复杂性论证「拆还是合」，而不是从文件长度或品味
- 说出把复杂性往*上*推给调用方、而不是往*下*沉进模块时，是谁在付账
- 认出「separation of concerns」被用在了本来就不该分开的东西上

**实践题形状。**给数据访问路径加一层 cache。cache 是第 7 章最干净的测试，因为一个把自己的
存在往上漏的 cache，恰好在唯一一件事上失败了。盯住 agent 把 cache invalidation 的决定放在
哪里。

---

## M3 — 设计流程

**目录：**[`modules/m3-design-process/`](modules/m3-design-process/README.zh.md)

| 章 | 英文 | 中文 |
|---|---|---|
| 10 | [Define Errors Out Of Existence](https://yingang.github.io/aposd2e-zh/en/ch10.html) | [通过定义来规避错误](https://yingang.github.io/aposd2e-zh/ch10.html) |
| 11 | [Design it Twice](https://yingang.github.io/aposd2e-zh/en/ch11.html) | [设计两次](https://yingang.github.io/aposd2e-zh/ch11.html) |

**核心问题。**能靠重新定义「这个操作是什么意思」来删掉一整类 bug 吗？以及，为什么你的第一版
设计几乎从来不是该交付的那一版？

**vibe coding 在哪里失效。**让 agent「make it robust」，你会得到防御性代码：更多分支、更多
异常类型、更多处理 —— 全都尽职尽责地正确，全都是一个更好的定义本可以删掉的复杂性。第 11 章
是整本书里最便宜的 prompt 干预：**先给我两个设计，再写代码。**两个设计的代价是多一次生成，
现在这几乎免费。

**学完你能：**

- 重写一份规格，让一个原本要处理的错误不再是错误
- 区分「defined out of existence」和它的邪恶双胞胎「silently swallowed」
- 用 agent 跑一次两设计对比，并按复杂性评判结果
- 解释为什么 design-it-twice 在 agent 时代变便宜了，而 design-once 变得更诱人

**实践题形状。**config 加载。文件缺失、key 不存在、类型不对、值格式错 —— 朴素设计里有四条
错误路径，更好的设计里少得多。先生成朴素版，然后**重新设计接口，而不是重新设计错误处理**。

---

## M4 — 注释与命名

**目录：**[`modules/m4-naming-comments/`](modules/m4-naming-comments/README.zh.md)

| 章 | 英文 | 中文 |
|---|---|---|
| 12 | [Why Write Comments? The Four Excuses](https://yingang.github.io/aposd2e-zh/en/ch12.html) | [不写注释的四个借口](https://yingang.github.io/aposd2e-zh/ch12.html) |
| 13 | [Comments Should Describe Things that Aren't Obvious from the Code](https://yingang.github.io/aposd2e-zh/en/ch13.html) | [注释应该描述代码中难以理解的内容](https://yingang.github.io/aposd2e-zh/ch13.html) |
| 14 | [Choosing Names](https://yingang.github.io/aposd2e-zh/en/ch14.html) | [选取名称](https://yingang.github.io/aposd2e-zh/ch14.html) |
| 15 | [Write The Comments First](https://yingang.github.io/aposd2e-zh/en/ch15.html) | [先写注释](https://yingang.github.io/aposd2e-zh/ch15.html) |

**核心问题。**注释必须承载什么代码自己承载不了的信息？

**vibe coding 在哪里失效。**agent 产出大量近乎零信息量的注释文本 —— `# 计数器加一`、把签名
用散文重述一遍的 docstring。很容易把这归档为风格问题。**它不是。**一条复述代码的注释，是
**没有任何设计决策被记录下来的证据 —— 因为本来就没有设计决策可记录**。第 15 章接着把整件事
翻转成一项技术：如果注释先写，它们就成了 agent 写码时对照的规格。

**学完你能：**

- 把任何注释归类为 interface、data structure、implementation 或 cross-module
- 见到复述型注释就删，并从第 13 章而不是从品味给出理由
- 发现一个含糊的名字，并说出它具体邀请了哪一种误解
- 把 comment-first 当作生成策略用，而不只是审查判据

**实践题形状。**拿 agent 在前面模块写过的一个非平凡函数，让它为这个函数写文档。然后**反转
顺序**：你自己先写接口注释，让 agent 照着实现。第二份产物通常是个不同的*设计*，而不只是注释
不同 —— 那个差异就是发现。

---

## M5 — 一致性与修改

**目录：**[`modules/m5-consistency-maintenance/`](modules/m5-consistency-maintenance/README.zh.md)

| 章 | 英文 | 中文 |
|---|---|---|
| 16 | [Modifying Existing Code](https://yingang.github.io/aposd2e-zh/en/ch16.html) | [修改现有的代码](https://yingang.github.io/aposd2e-zh/ch16.html) |
| 17 | [Consistency](https://yingang.github.io/aposd2e-zh/en/ch17.html) | [一致性](https://yingang.github.io/aposd2e-zh/ch17.html) |
| 18 | [Code Should be Obvious](https://yingang.github.io/aposd2e-zh/en/ch18.html) | [代码应该是易理解的](https://yingang.github.io/aposd2e-zh/ch18.html) |

**核心问题。**如何在改动系统时，不让你起初的设计退化？

**vibe coding 在哪里失效。**这是最高风险的 agent 操作，同时也是最常见的。一个 agent 改它没
写过的代码，可靠地产出：一个复制了三个文件之外已有抽象的局部修复；对一条从没人写下来的约定的
静默破坏；一条留在正确改动之上、如今自信地错着的过期注释。每一条单独看都微不足道。第 16 章的
论证是：**累积才是设计的死法** —— 而累积恰恰是 agent 在加速的东西。

**学完你能：**

- 对照从未被写下来的约定，审计一个 diff 的一致性断裂
- 在别人的 PR 里区分 strategic edit 和 tactical edit
- 说出为了做出不退化的改动，agent 必须事先被告知什么
- 认出「这很明显」其实是「我写的，我还记得」

**实践题形状。**把 M2 的 `after/` 代码当作既有系统，让一个**没有课程上下文**的 agent 加个新
功能。这是全课唯一一个建立在前一个模块之上的 case study，而这是刻意的：**你无法研究代码修改，
除非先有一个值得被破坏的设计。**

---

## M6 — 趋势、权衡与判断

**目录：**[`modules/m6-trends-tradeoffs/`](modules/m6-trends-tradeoffs/README.zh.md)

| 章 | 英文 | 中文 |
|---|---|---|
| 19 | [Software Trends](https://yingang.github.io/aposd2e-zh/en/ch19.html) | [软件发展趋势](https://yingang.github.io/aposd2e-zh/ch19.html) |
| 20 | [Designing for Performance](https://yingang.github.io/aposd2e-zh/en/ch20.html) | [性能设计](https://yingang.github.io/aposd2e-zh/ch20.html) |
| 21 | [Decide What Matters](https://yingang.github.io/aposd2e-zh/en/ch21.html) | [决定什么是重要的](https://yingang.github.io/aposd2e-zh/ch21.html) |
| 22 | [Conclusion](https://yingang.github.io/aposd2e-zh/en/ch22.html) | [结论](https://yingang.github.io/aposd2e-zh/ch22.html) |

**核心问题。**Ousterhout 拿自己的判据给 agile、TDD、设计模式、getters/setters 打了分。用同一
套判据给 vibe coding 打分 —— 并且**愿意接受一个你本来不想要的结论**。

**vibe coding 在哪里失效。**或者说，也许并没有。这是唯一一个**允许结论有利于 vibe coding**
的模块。第 21 章问什么才真正值得投入注意力；第 20 章坚持性能工作必须被测量而不是被假设 ——
那正是这整门课对设计施加的同一种纪律。产出是一条**校准过的规则**：什么时候放 agent 全速跑，
什么时候拦住它。不是任何一个方向上的一刀切政策。

**学完你能：**

- 用第 19 章的判据给 vibe coding 打分，写下来，**包含反面情形**
- 说出在代码免费的前提下，设计投资的哪些部分还在回本、哪些不再回本
- 陈述你自己「该慢下来」的阈值，具体到足以被证伪
- 论证 APOSD 的建议在这个时代是需要修订，还是仅仅需要执行

**实践题形状。**不生成新代码。改为：把前面六份 `findings.md` 当作一个数据集重读，写出那份
评分。证据是在整门课的过程中收集的，正是为了让这个模块能做实证而不是修辞。

---

## 不在范围内

本课程不涵盖测试策略、CI、code review 流程、团队实践，也不把 prompt engineering 当作一个
一般性学科来讲。这些东西碰到设计的地方会出现在某个模块内部；其余部分是别人的课。
