# M2 — 抽象与分层

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

| | |
|---|---|
| **章节** | [7 Different Layer, Different Abstraction](https://yingang.github.io/aposd2e-zh/en/ch07.html) · [8 Pull Complexity Downwards](https://yingang.github.io/aposd2e-zh/en/ch08.html) · [9 Better Together Or Better Apart?](https://yingang.github.io/aposd2e-zh/en/ch09.html) |
| **中文** | [不同的层级，不同的抽象](https://yingang.github.io/aposd2e-zh/ch07.html) · [下沉复杂性](https://yingang.github.io/aposd2e-zh/ch08.html) · [在一起更好还是分开更好？](https://yingang.github.io/aposd2e-zh/ch09.html) |
| **核心问题** | 谁来吸收复杂性，这该是一个东西还是两个？ |
| **前置** | M1 —— 层是由模块构成的，你需要先有深度测试 |
| **状态** | 未开始 |

---

## 读之前，停

**现在别读第 7–9 章。**读书是阶段 3。

## 核心问题

两个问题，最后发现是同一个问题。

*谁来吸收复杂性？* 每一个别扭的细节都会落在某个地方。第 8 章论证它应该**落在模块内部一次**，
而不是**落在每个调用方那里反复落**。理由是算术，不是美学。

*这该是一个东西还是两个？* 第 9 章拒绝用「文件多长」「函数多大」之类的规则来回答。答案取决于
拆分是**降低了总复杂性**，还是仅仅**把它搬了个地方、还往账单上添了一个接口**。

## vibe coding 在哪里失效

这个模块有意思，因为 agent **两个方向都会翻车** —— 而两种失效看起来是相反的，实际上同源。

要一个功能，经常拿到一个干五件事的扁平函数。要 *clean architecture*，经常拿到四个类、每个
方法都在往下一个转发 —— 一条 pass-through 链，加了名字、文件和间接层，**却没加一个新抽象**。
第 7 章给它起了名字，而一旦你有了这个名字，你就再也无法不看见它。

**两者是同一种失效：没有任何关于「每一层是为了什么」的决定被做出。**一个把决定压平掉了，
另一个表演了做决定的样子。

## 学完你能

- [ ] 叫出 pass-through method、pass-through variable、decorator class 的名字
- [ ] 从复杂性论证「拆还是合」，而不是从文件长度或品味
- [ ] 说出把复杂性往*上*推给调用方、而不是往*下*沉进模块时，是谁在付账
- [ ] 认出「separation of concerns」被用在了本来就不该分开的东西上

## 实践题

**Round A — 基线。**拿一条数据访问路径（一个走数据库的 user lookup 就够了），说 `「加 cache」`。

**Round B — grounding 之后。**同样的任务，但指定层边界。

**为什么选 cache。**它是第 7 章最干净的测试，因为一个 cache 在接口层面**恰好只有一件工作：
不存在**。一个必须知道 cache 在那里的调用方 —— 更糟，一个必须**为它做决定**的调用方 —— 已经
被交了一个泄露，而这个泄露在签名里就看得见。

**要盯的具体信号。**公开的 lookup 函数上出现一个 `use_cache: bool = False` 参数。这是 agent
把 caching 决定往上翻的最常见方式，它看起来像是贴心的灵活性，**实际意味着每个调用方从此都得对
cache 语义有个看法**。另外盯住 invalidation 落在哪 —— 如果调用方要负责调 `invalidate()`，
那这个 cache 不是一层，是一件家务。

**保留产出。**M5 会把这个模块的 `after/` 当作它的既有系统，所以这里的重构必须是一个**值得被
破坏的设计**。这是全课唯一一处「敷衍会有下游代价」的地方。

## 文件

| 路径 | 放什么 |
|---|---|
| [`socratic-log.md`](socratic-log.md) | 阶段 1–3：对话，蒸馏后的 |
| [`case-study/README.md`](case-study/README.md) | brief —— 两轮，逐字记录 |
| `case-study/{python,typescript}/before/` | Round A 输出。不可变。 |
| `case-study/{python,typescript}/after/` | 重构 —— **M5 的起点** |
| [`case-study/findings.md`](case-study/findings.md) | 批评、差异、成本 |

## 完成条件

1. [ ] `socratic-log.md` 覆盖阶段 1–3，Grounding 有章节引用
2. [ ] 两种语言都有 `before/` 和 `after/`，代码跑得起来
3. [ ] `findings.md` 记录了 cache 在哪里漏了、invalidation 最后落在哪
4. [ ] [`../../prompts/`](../../prompts/) 里至少一个 prompt，**Observed effect** 已填
5. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) 长出一行
6. [ ] 根 [README](../../README.zh.md) 进度表已更新
7. [ ] `after/` 干净到可以作为一个真实系统交给 M5
