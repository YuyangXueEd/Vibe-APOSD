# M3 — 设计流程

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

| | |
|---|---|
| **章节** | [10 Define Errors Out Of Existence](https://yingang.github.io/aposd2e-zh/en/ch10.html) · [11 Design it Twice](https://yingang.github.io/aposd2e-zh/en/ch11.html) |
| **中文** | [通过定义来规避错误](https://yingang.github.io/aposd2e-zh/ch10.html) · [设计两次](https://yingang.github.io/aposd2e-zh/ch11.html) |
| **核心问题** | 能靠重新定义「这个操作是什么意思」来删掉一整类 bug 吗？ |
| **前置** | M1、M2 —— 重新定义一个操作，意味着移动它的边界 |
| **状态** | 未开始 |

---

## 读之前，停

**现在别读第 10–11 章。**读书是阶段 3。

第 10 章尤其如此：它的结论第一次听到时**听起来是错的**，这让它成为最好的阶段 1 材料，也让它
成为最不该被剧透的东西。

## 核心问题

碰到一个错误条件时，本能是**处理**它。第 10 章提出一件初听起来像不负责任的事：**改变这个操作
的定义，让这个条件不再是错误 —— 于是没有东西需要处理。**

在这变成安全的建议之前，必须先钉死一个区分：**defined out of existence** 和
**silently swallowed**。两者产出看起来相似的代码，和相反的结局，而这个差别就是那一章的全部
内容。

第 11 章是独立的，而且简单得多：**你的第一版设计是初稿**，把它当成决定，就是你最后住进它里面
的方式。

## vibe coding 在哪里失效

让 agent `「make it robust」`，你会得到防御性代码 —— 更多分支、更多异常类型、更多处理，全都
尽职尽责地正确，全都是一个更好的定义本可以删掉的复杂性。prompt 要的是 robustness，拿到的是
*handling* —— 因为**从函数内部看，robustness 长得就像 handling**。

第 11 章是整本书最便宜的干预，而 agent 让它更便宜了。两个设计过去要花两轮人力，这就是没人做的
原因。**两个设计现在的代价是多一次生成。经济学翻转了**，而几乎没人更新自己的习惯 —— 包括大多数
读过这一章的人。

## 学完你能

- [ ] 重写一份规格，让一个原本要处理的错误不再是错误
- [ ] 区分「defined out of existence」和「silently swallowed」，**并给出能区分它们的测试**
- [ ] 用 agent 跑一次两设计对比，并按复杂性评判结果
- [ ] 说出为什么 design-it-twice 变便宜了，而 design-once 变得更诱人

## 实践题

**Round A — 基线。**`「写一个从文件加载 config 的函数。」` 别的什么都不说。

然后**枚举**返回结果里的错误路径。朴素设计至少有四条：文件缺失、key 不存在、值类型不对、值格式
错。数一下，再数一下**其中有几条是每个调用方都必须知道的**。

**Round B — 重新设计接口，不是重新设计错误处理。**干预不是更好的 `try/except`。而是一个不同的
「加载 config 意味着什么」的定义 —— 在那个定义下，四条里有几条不再是条件。**不要跳到答案**，
在阶段 2 里推出来。

**Round C — 设计两次。**同样的原始任务，新的 prompt：先给两个设计再写代码，并陈述权衡。把胜者
和 Round A 对比。真正要测的是：第二个设计**是否更好**，*以及*它是否**比修补第一个更便宜**。

**陷阱。**一个对所有东西都返回默认值的 config loader **没有**把错误定义掉 —— 它只是把生产
配置文件里的一个拼写错误藏到了凌晨三点。如果你的重新设计无法区分「这个 key 不存在，而这没
问题」和「这个 key 拼错了」，那它就是那个邪恶双胞胎。**写出能区分它们的测试。**

## 文件

| 路径 | 放什么 |
|---|---|
| [`socratic-log.md`](socratic-log.md) | 阶段 1–3：对话，蒸馏后的 |
| [`case-study/README.md`](case-study/README.md) | brief —— 三轮，逐字记录 |
| `case-study/{python,typescript}/before/` | Round A 输出。不可变。 |
| `case-study/{python,typescript}/after/` | Round B 和 C，分开放 |
| [`case-study/findings.md`](case-study/findings.md) | 批评、差异、成本 |

## 完成条件

1. [ ] `socratic-log.md` 覆盖阶段 1–3，Grounding 有章节引用
2. [ ] 两种语言都有 `before/` 和 `after/`，代码跑得起来
3. [ ] `findings.md` 数出了前后的错误路径条数，并包含那个 swallowing 测试
4. [ ] Round C 的两个设计都被记录，**包括输掉的那个**
5. [ ] [`../../prompts/`](../../prompts/) 里至少一个 prompt，**Observed effect** 已填
6. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) 长出一行
7. [ ] 根 [README](../../README.zh.md) 进度表已更新
