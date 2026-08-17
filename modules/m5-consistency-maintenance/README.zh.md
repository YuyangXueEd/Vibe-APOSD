# M5 — 一致性与修改

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

| | |
|---|---|
| **章节** | [16 Modifying Existing Code](https://yingang.github.io/aposd2e-zh/en/ch16.html) · [17 Consistency](https://yingang.github.io/aposd2e-zh/en/ch17.html) · [18 Code Should be Obvious](https://yingang.github.io/aposd2e-zh/en/ch18.html) |
| **中文** | [修改现有的代码](https://yingang.github.io/aposd2e-zh/ch16.html) · [一致性](https://yingang.github.io/aposd2e-zh/ch17.html) · [代码应该是易理解的](https://yingang.github.io/aposd2e-zh/ch18.html) |
| **核心问题** | 如何在改动系统时，不让你起初的设计退化？ |
| **前置** | **特别是 M2** —— 这个模块修改 M2 的 `after/` 代码 |
| **状态** | 未开始 |

---

## 读之前，停

**现在别读第 16–18 章。**读书是阶段 3。

## 核心问题

三章，一个问题。修改现有代码（16）、一致性（17）、易理解（18）都在问：**一个系统在被并非其
设计者的人不断改动时，如何保持连贯？**

这个说法应该听起来很熟，因为它精确地描述了**一个 agent 在改你的代码库**。

## vibe coding 在哪里失效

这是最高风险的 agent 操作，而且 —— 很不方便地 —— 也是最频繁的。一个 agent 改它没写过的代码，
可靠地产出下面几样的某种组合：

- 一个**复制了已有抽象的局部修复**，而那个抽象就在三个文件之外，没被读到
- 对一条**从没人写下来的约定的静默破坏**，因为它一直只是个 pattern
- 一条**过期注释**留在正确改动之上，如今自信地错着
- 一个**改在错误的层**的改动，因为错误的那层恰好在上下文里

每一条单独看都微不足道，而且单独看都站得住。第 16 章的论证是：**累积才是设计的死法** ——
而累积恰恰是 agent 在加速的东西，因为过去节流它的那个单次改动成本已经归零了。

第 18 章提供了那个值得坐下来想想的不舒服问题：**对谁明显？**「这很明显」经常可以解码成「我写
的，而且我还记得为什么」。**agent 完全不记得写过它 —— 这让它成了「下一个读者」的一个出乎意料
好用的代理。**

## 学完你能

- [ ] 对照从未被写下来的约定，审计一个 diff 的一致性断裂
- [ ] 在别人的 PR 里区分 strategic edit 和 tactical edit
- [ ] 说出为了做出不退化的改动，agent 必须事先被告知什么
- [ ] 认出「这很明显」其实是「我写的，我还记得」

## 实践题

**Round A — 基线。**拿 M2 的 `after/` 代码 —— 你重构过的那条带 cache 的数据访问路径 —— 让
agent 加一个新功能。**两个条件都重要，而且都容易搞错：**

1. **全新 session，没有课程上下文。**没有 `CLAUDE.md`，没有设计约束，不提 APOSD。否则基线被
   污染，这个模块什么也产不出。
2. **一个碰到你建立的层边界的功能。**比如批量查询，或者 per-tenant 隔离。一个**完全落在单个
   文件里**的功能无法让设计退化，也无法演示第 16 章。

然后对照上面四种失效模式审计 diff，**一条一条点名**。

**Round B — 受约束的修改。**同样的功能、同样的起始代码，但你提供 agent 当时需要的东西：那些
从没被写下来的约定、这个改动属于哪一层、什么不许变。对比。

**这个模块为什么建立在 M2 之上。**你无法研究代码修改，除非已经有一个**值得被破坏的设计**。为此
专门生成一个一次性系统会毁掉它 —— 你知道它是用完就扔的，就不会在乎它被搞成什么样。用你自己的
重构成果意味着**退化对你有代价**，而这是这个模块能教会你东西的唯一条件。

## 文件

| 路径 | 放什么 |
|---|---|
| [`socratic-log.md`](socratic-log.md) | 阶段 1–3：对话，蒸馏后的 |
| [`case-study/README.md`](case-study/README.md) | brief —— 两轮，加上所用的 M2 commit |
| `case-study/{python,typescript}/before/` | 无约束 diff 应用到 M2 代码后的结果。不可变。 |
| `case-study/{python,typescript}/after/` | 受约束的修改，加上对 Round A 的修复 |
| [`case-study/findings.md`](case-study/findings.md) | 批评、差异、成本 |

**记下你起始的那个 M2 commit hash。**没有它，没人能复现这个 diff，case study 就退化成一则轶事。

## 完成条件

1. [ ] `socratic-log.md` 覆盖阶段 1–3，Grounding 有章节引用
2. [ ] 两种语言都有 `before/` 和 `after/`，代码跑得起来
3. [ ] diff 已对照全部四种失效模式审计，每一种都被明确点名
4. [ ] 起始的 M2 commit 已记录在 `case-study/README.md`
5. [ ] [`../../prompts/`](../../prompts/) 里至少一个 prompt，标记为 `before-modification`
6. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) 长出一行
7. [ ] 根 [README](../../README.zh.md) 进度表已更新
