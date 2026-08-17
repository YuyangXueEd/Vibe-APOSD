# M4 — 注释与命名

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

| | |
|---|---|
| **章节** | [12 Why Write Comments? The Four Excuses](https://yingang.github.io/aposd2e-zh/en/ch12.html) · [13 Comments Should Describe Things that Aren't Obvious from the Code](https://yingang.github.io/aposd2e-zh/en/ch13.html) · [14 Choosing Names](https://yingang.github.io/aposd2e-zh/en/ch14.html) · [15 Write The Comments First](https://yingang.github.io/aposd2e-zh/en/ch15.html) |
| **中文** | [不写注释的四个借口](https://yingang.github.io/aposd2e-zh/ch12.html) · [注释应该描述代码中难以理解的内容](https://yingang.github.io/aposd2e-zh/ch13.html) · [选取名称](https://yingang.github.io/aposd2e-zh/ch14.html) · [先写注释](https://yingang.github.io/aposd2e-zh/ch15.html) |
| **核心问题** | 注释必须承载什么代码自己承载不了的信息？ |
| **前置** | M1 —— 这个论证依赖 information hiding |
| **状态** | 未开始 |

---

## 读之前，停

**现在别读第 12–15 章。**读书是阶段 3。

## 核心问题

**不是**「该不该写注释」—— 那个问题是个陷阱，第 12 章拆掉了它的四个常见答案。真正的问题是：
**注释能承载什么代码承载不了的东西**，因为那才是唯一值得写下来的东西。

一条复述代码的注释按构造就携带零信息。它不是低价值注释，它是**负价值**注释 —— 因为它终将出错，
届时会主动误导别人。

## vibe coding 在哪里失效

agent 产出大量近乎零信息量的注释文本 —— `# 计数器加一`、把签名用散文渲染回来的 docstring、
三行代码上方的分区横幅。很容易把这归档为风格问题，然后配个 linter。

**那种读法错过了发现。一条复述代码的注释，是「没有任何设计决策被记录下来」的证据 —— 因为本来
就没有设计决策可记录。**注释是症状。真正的病是：关于*为什么*、关于不变量、关于调用方**不许**
做什么，一句陈述都没有。第 14 章对名字说了同样的话：**一个含糊的名字不是文笔潦草，是一个没做
出的决定** —— 而含糊之处正是那个决定本该在的位置。

第 15 章接着把整件事翻转成一项技术。如果注释先写，它们就不再是文档，而成了 **agent 写码时对照
的规格** —— 这就是为什么这个模块属于一门讲 prompt 的课，而不只属于一门讲风格的课。

## 学完你能

- [ ] 把任何注释归类为 interface、data structure、implementation 或 cross-module
- [ ] 删掉一条复述型注释，并从第 13 章而不是从品味给出理由
- [ ] 发现一个含糊的名字，并说出它具体邀请了哪一种误解
- [ ] 把 comment-first 当作生成策略用，而不只是审查判据

## 实践题

**Round A — 基线。**拿 agent 在 M1 或 M2 写过的一个非平凡函数，让它为这个函数写文档。然后把它
产出的**每一条**注释归入第 13 章的某一类，并标出哪些携带了代码没携带的信息。

**诚实地报告那个比例。**现在的 agent 有时做得不错，**一个好结果是一个真实发现** —— 它属于 M6
的证据堆。

**Round B — 反转顺序。**在任何代码存在之前，**你自己**写接口注释。陈述这个函数保证什么、调用方
不许假设什么、什么不变量成立。然后让 agent 照着实现。

**Round B 要盯什么。**不是更好的注释 —— 而是一个**不同的设计**。通常的结果是不同的签名、不同的
错误契约，有时是不同的函数个数。**那个差异就是发现**，也是为什么第 15 章坐在书的设计那一半、
而不是文档那一半。

**顺带说命名。**重构时每次要取名字，把你**否掉了什么、为什么**写下来。第 14 章的论证，从你自己
的三个被丢弃的候选里体会，比从一个现成例子里容易得多。

## 文件

| 路径 | 放什么 |
|---|---|
| [`socratic-log.md`](socratic-log.md) | 阶段 1–3：对话，蒸馏后的 |
| [`case-study/README.md`](case-study/README.md) | brief —— 两轮，逐字记录 |
| `case-study/{python,typescript}/before/` | Round A：函数加生成的注释。不可变。 |
| `case-study/{python,typescript}/after/` | Round B：comment-first 的实现 |
| [`case-study/findings.md`](case-study/findings.md) | 批评、差异、成本 |

## 完成条件

1. [ ] `socratic-log.md` 覆盖阶段 1–3，Grounding 有章节引用
2. [ ] 两种语言都有 `before/` 和 `after/`，代码跑得起来
3. [ ] Round A 的每条注释都已归类，并陈述了携带信息的比例
4. [ ] `findings.md` 说明了 Round B 是否改变了**设计**，而不只是注释
5. [ ] [`../../prompts/`](../../prompts/) 里至少一个 prompt，**Observed effect** 已填
6. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) 长出一行
7. [ ] 根 [README](../../README.zh.md) 进度表已更新
