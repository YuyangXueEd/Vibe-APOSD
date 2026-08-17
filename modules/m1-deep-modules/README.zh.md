# M1 — 深模块

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

| | |
|---|---|
| **章节** | [4 Modules Should Be Deep](https://yingang.github.io/aposd2e-zh/en/ch04.html) · [5 Information Hiding (and Leakage)](https://yingang.github.io/aposd2e-zh/en/ch05.html) · [6 General-Purpose Modules are Deeper](https://yingang.github.io/aposd2e-zh/en/ch06.html) |
| **中文** | [模块应该是深的](https://yingang.github.io/aposd2e-zh/ch04.html) · [信息隐藏和信息泄露](https://yingang.github.io/aposd2e-zh/ch05.html) · [通用的模块是更深的](https://yingang.github.io/aposd2e-zh/ch06.html) |
| **核心问题** | 什么让一个模块变深，什么该藏在接口后面？ |
| **前置** | M0 —— 没有复杂性的定义，「深」这个字没有意义 |
| **状态** | 未开始 |

---

## 读之前，停

**现在别读第 4–6 章。**读书是阶段 3。

这个模块**特别容易糊弄过去**。「模块应该是深的」是句好记的口号，你可以在完全不会应用它的
情况下把它复述出来。对话存在的意义就是查清你手里是哪一个。

## 核心问题

**深度是一个比值，不是一个尺寸。**当一个模块的接口复杂性相对于它所隐藏的复杂性很小时，它是
深的。这里面没有任何东西要求模块很大，也没有任何东西让一个大模块自动变深。

有意思的推论是：**你无法只看实现来判断深度。**你必须看**调用方被迫知道什么**。这就是为什么
这个模块是课程从「事后 code review」转向「prompt 设计」的地方。

## vibe coding 在哪里失效

`「写个 helper 处理 X」` 是一条关于**实现**的指令。它可靠地产出一个 shallow module —— 接口
几乎和它包裹的函数体一样复杂，为调用方省了四行，却要求调用方理解六个参数。

修复点在生成的**上游**：在于你如何陈述一个边界而不陈述一个实现 —— 这件事写起来出乎意料地
困难，而它才是这个模块真正训练的技能。

第 6 章加上了校准问题，而 agent 以一种具体的方式让它变糟了：**当两种写法的成本都是零时**，
「适度通用」不再是两种努力程度之间的折中，而纯粹变成了一个关于未来变化的判断。你现在必须
就事论事地做这个判断，**没有努力梯度可以躲**。

## 学完你能

- [ ] 认出 shallow module，并说出让它成为 shallow 的 interface-vs-implementation 成本
- [ ] 在两个看起来互相独立的模块之间找到 information leakage
- [ ] 判断一个抽象是过于通用、过于专用，还是适度通用
- [ ] 写出一段指定了边界、但没指定实现的任务描述

## 实践题

**Round A — 基线。**给 agent 一个 HTTP client，说 `「加 rate limiting」`。别的什么都不说。

**Round B — 受约束版。**同样的任务，但你先给出接口契约：调用方**可以**知道什么、**不能**
知道什么、竞争条件下会发生什么。**不要描述算法。**

**为什么选 rate limiting。**它是个异常干净的深度测试。朴素版会把算法从接口漏出去 —— 调用方
最后得传 window size，或者得处理一个它自己还要决定怎么重试的 `RateLimitExceeded`。深的版本把
一个真正困难的问题藏在大约两个方法后面。两种结局之间的差距大到无法争辩 —— 这对第一个「你在给
自己的 prompt 打分而不是给 agent 的代码打分」的模块来说很重要。

**盯什么。**调用方必须提供的每个参数、必须区分的每个异常、必须遵守的每个顺序约束。**那些就是
接口。数一下。**

## 文件

| 路径 | 放什么 |
|---|---|
| [`socratic-log.md`](socratic-log.md) | 阶段 1–3：对话，蒸馏后的 |
| [`case-study/README.md`](case-study/README.md) | brief —— 两轮，逐字记录 |
| `case-study/{python,typescript}/before/` | Round A 输出。不可变。 |
| `case-study/{python,typescript}/after/` | Round B 输出，加上对 Round A 的重构 |
| [`case-study/findings.md`](case-study/findings.md) | 批评、差异、成本 |

**Round B 是第二次实验，不是重构** —— 保持两者可区分。真正重要的对比是「受约束的生成」对
「不受约束的生成然后修补」，而其中一条更便宜。

## 完成条件

1. [ ] `socratic-log.md` 覆盖阶段 1–3，Grounding 有章节引用
2. [ ] 两种语言都有 `before/` 和 `after/`，代码跑得起来
3. [ ] `findings.md` **数出**了重构前后的接口表面积，而不只是描述它
4. [ ] [`../../prompts/`](../../prompts/) 里至少一个 prompt，**Observed effect** 已填
5. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) 长出一行
6. [ ] 根 [README](../../README.zh.md) 进度表已更新
