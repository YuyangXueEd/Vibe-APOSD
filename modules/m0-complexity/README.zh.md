# M0 — 复杂性的本质

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

| | |
|---|---|
| **章节** | [1 Introduction](https://yingang.github.io/aposd2e-zh/en/ch01.html) · [2 The Nature of Complexity](https://yingang.github.io/aposd2e-zh/en/ch02.html) · [3 Working Code Isn't Enough](https://yingang.github.io/aposd2e-zh/en/ch03.html) |
| **中文** | [介绍](https://yingang.github.io/aposd2e-zh/ch01.html) · [复杂性的本质](https://yingang.github.io/aposd2e-zh/ch02.html) · [能工作的代码是不够的](https://yingang.github.io/aposd2e-zh/ch03.html) |
| **核心问题** | 复杂性从哪来，为什么「能跑」不是终点线？ |
| **前置** | 无 —— 从这里开始 |
| **状态** | 未开始 |

---

## 读之前，停

**现在别读第 1–3 章。**读书是阶段 3，不是阶段 1。

如果先读，你会采纳 Ousterhout 的立场却从未注意到它和你原本的想法有什么不同，最后带着一套
借来的、你用不上的观点结束这个模块。**对话必须在你的直觉还属于你的时候抓住它。**

*已经读过这本书？* 在第一条消息里说明。老师会改用书没有直接回答的场景，并且会探查你能否
**应用**这套词汇，而不是**背诵**它。

## 核心问题

每个用 coding agent 的人都见过同一件事：输出第一天过测试，到第三十天，任何改动都像做手术。
这个体验是普遍的。**机制却几乎从不被点名** —— 而一个没被点名的机制只能在事后被抱怨，永远
无法被预防。

这个模块就是来点名的。

## vibe coding 在哪里失效

第 3 章画了一条线，分开 **tactical** programming（让这个现在能跑）和 **strategic**
programming（投资于让它保持可用）。整门课建立在这个不舒服的观察上：

> agent 优化眼前这个 prompt，对下个季度的维护不承担任何利害，而且永远不会累。
> **tactical 不是它犯的错误，而是它的默认值** —— 除非你提供另一样东西。

第 2 章的三个症状 —— change amplification、cognitive load、unknown unknowns —— 是诊断词汇。
第三个在这里最要紧，因为它是**唯一一个你无法通过阅读被展示给你的代码来发现的**。

## 学完你能

- [ ] 指着真实 diff 里的某一行，说出它产生了三个症状中的哪一个
- [ ] 解释为什么 agent 在构造上就是 tactical，而不是偶然是
- [ ] 论证：当生成代码免费时，strategic programming 还买得到吗
- [ ] 说出你自己的工作流必须改掉哪一件事，才买得到它

## 实践题

**Round A — 基线。**让 agent 写一个 CLI：读一个 CSV 订单文件，打印汇总 —— 总营收、订单数、
最畅销商品。prompt 里不加任何设计指导。

**Round B、C、D — 三个它事先不知道的需求。**一次一个，分开的轮次，每个都用**一个利益相关方
会用的说法**来提：

1. 按日期区间过滤
2. 除 CSV 外也接受 JSON 输入
3. 除文本外也输出 JSON，并按区域拆分

**为什么是四轮而不是一轮。**复杂性不出现在第一次生成里 —— 第一次通常看着还行，**这正是它难被
讨论的原因**。它出现在*序列*里。change amplification 按定义就是在有东西改变之前不可见的。
一次性的 case study 无法演示第 2 章，还会悄悄误导你以为问题在代码质量。

**记下每个需求碰了几个文件。那个数字就是发现。**

## 文件

| 路径 | 放什么 |
|---|---|
| [`socratic-log.md`](socratic-log.md) | 阶段 1–3：对话，蒸馏后的 |
| [`case-study/README.md`](case-study/README.md) | brief —— 任务逐字记录、withheld 了什么 |
| `case-study/{python,typescript}/before/` | 每轮的 agent 原始输出。不可变。 |
| `case-study/{python,typescript}/after/` | 重构 |
| [`case-study/findings.md`](case-study/findings.md) | 批评、before/after 差异、成本 |

每轮在 `before/` 下各占一个子目录 —— `round-a/` 到 `round-d/` —— 让增长在目录树里可见，
而不是只在 git history 里。

## 完成条件

1. [ ] `socratic-log.md` 覆盖阶段 1–3，Grounding 有章节引用
2. [ ] 两种语言都有 `before/`（四轮全）和 `after/`，代码跑得起来
3. [ ] `findings.md` 点出具体原则对具体行号，并陈述差异
4. [ ] [`../../prompts/`](../../prompts/) 里至少一个 prompt，**Observed effect** 已填
5. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) 长出一行
6. [ ] 根 [README](../../README.zh.md) 进度表已更新
