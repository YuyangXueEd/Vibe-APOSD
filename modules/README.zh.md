# 一个模块是怎么运作的

[English](README.md) · **中文**

> 英文版是权威版本。两者若有分歧，以 [README.md](README.md) 为准。

本课程每个模块都跑同样的六个阶段，产出同样的三样东西。这种统一是刻意的：做完 M0 之后，你就
知道 M1 到 M6 会怎么跑，脑子里唯一需要装的东西是设计问题本身。

---

## 六个阶段

### 阶段 1 — 直觉

老师给出一个来自日常软件工程的具体场景 —— 请求校验、config 加载、重试逻辑、报表生成。你凭
经验回答。

**不读书。**不读章节，不读总结，也不提示这是要往哪走。**先读会摧毁整个方法**：你会采纳
Ousterhout 的立场，却从未注意到它和你原本的想法有什么不同 —— 什么都没学到，因为什么都没被
押上赌桌。

产出：场景、问题、答案，以及最重要的 ——**这个答案隐含地承诺了什么**。把那条隐含规则显式化，
才让阶段 2 有东西可测试。

### 阶段 2 — 追问

老师构造**最小**的那个反例：在这个例子里，你自己说出的规则会导出一个你不会为之辩护的结果。
然后问你想怎么办。

两种有效结局：

- **直觉崩了。**在 log 里标出崩点。这是好情况。
- **直觉扛住了。**同样是好情况 —— 但前提是你现在能说清它*为什么*扛住。一条恰好正确但未经
  检验的规则，仍然是未经检验的。

老师**永远不说**「其实，答案是……」。让矛盾去教。

### 阶段 3 — 回到文本

现在，也只有现在，读那一章。你读完，用**自己的话**陈述那条原则。老师拿文本核对你的陈述，
并给出章节引用。

log 里有两节比其余部分更重要：

- **我在哪里不同意 Ousterhout。**鼓励，不是劝阻。一个对整本书每句话都同意的学习者，大概
  并没有真正跟它交手。
- **我在阶段 1 错在哪。**直觉和文本之间的具体差值。**这才是真正学到的东西**，而且这是唯一
  能记录它的地方。

### 阶段 4 — 生成

你给 agent 一个真实任务，agent 用 Python 和 TypeScript 各产出一份**诚实的默认输出**。

这是一场实验，它有一条污染规则：**prompt 里不许有任何设计约束。**不许「写干净点」，不许
「用好的抽象」，不许提到本模块的原则。给出的任务必须**逐字**记录在
`case-study/README.md` 里 —— 一个被转述过的实验条件不是实验条件。

agent 不许因为知道即将被审查而提高水准，也不许为了做出更好的教学例子而故意写烂。任何一边都会
让结果一文不值。**一个诚实基线结果很好，是一个真实发现** —— 照实记录，然后继续。

`before/` 一旦提交就不可变。里面的 bug 是**结果**，不是错误。

### 阶段 5 — 审查与重构

**先批评，后写码。**写出 findings，就「到底哪里错了」达成一致，然后才动实现。

把这个顺序反过来是浪费一个模块最常见的方式。先改完再解释产出的是一个**没人能评估的重构** ——
理由会被事后编造来迎合已经写出的代码，最后你手里是一个 diff，而不是一条原则。

一条 finding 必须点出位置和原则。「这个模块太浅」是意见。「`load_config` 在
`before/config.py:14` 收六个参数，为调用方省了四行代码 —— interface complexity 超过了它所隐藏
的 implementation complexity（Ch 4）」是 finding。

然后重构进 `after/`，保持可观察行为不变。如果行为不得不变，那本身就是一条值得写下来的独立
finding。

### 阶段 6 — 提炼

把「本可以阻止这次失效」的那条约束蒸馏进 `prompts/`，并给
`reference/review-checklist.md` 加至少一行。

prompt 模板有两个必填节 —— **Observed effect** 和 **Known failure modes** —— 任何一个都不许
留空。**一条你没亲眼见它成功*也*没见它失败过的 prompt，是迷信**，而这个仓库不做迷信生产。

---

## 产出物

| 文件 | 是什么 | 什么时候写 |
|---|---|---|
| `README.md` | 模块 brief：章节、核心问题、目标、实践题 | 开始之前 |
| `socratic-log.md` | 对话，蒸馏成教学素材 | 阶段 1–3 |
| `case-study/README.md` | 实验 brief：任务逐字记录、withheld 了什么 | 阶段 4 |
| `case-study/{python,typescript}/before/` | agent 原始输出，不可变 | 阶段 4 |
| `case-study/{python,typescript}/after/` | 重构 | 阶段 5 |
| `case-study/findings.md` | 批评、before/after 差异、成本 | 阶段 5 |
| `prompts/m<N>-*.md` | 提炼出的约束 | 阶段 6 |

**边走边写 log**，每个阶段结束时写。一份在模块末尾追溯重建的 log，是一份结论摘要 —— 而结论从
来不是有价值的那部分。

## 为什么 Python 和 TypeScript 都要

不是为了覆盖面，也不是为了触达更多读者。**它们是一组对照实验。**

动态语言把 interface complexity 赤裸地暴露出来 —— 一个带三个可选 dict 的六参数函数肉眼可见地
糟糕，而且没有任何东西会拦它。静态语言把其中一部分复杂性搬进签名，使它变得*可读*；又把另一部分
藏进类型系统，使它变得*不可见*。同一个设计失效在两边落地方式不同，而「哪个语言让它更容易被
看见」记录在每一份 `findings.md` 里。

**每一版都按各自语言的习惯写。**一份加了分号的 Python 直译文件什么也教不了。

## Definition of done

一个模块在下面六条全部为真时才算完成 —— 见 [CLAUDE.md](../CLAUDE.md) §9：

1. `socratic-log.md` 覆盖阶段 1–3，Grounding 节有章节引用
2. `case-study/` 两种语言都有 `before/` 和 `after/`，且代码跑得起来
3. `findings.md` 点出具体原则对具体行号，并陈述差异
4. `prompts/` 至少一个文件，**Observed effect** 由实际使用填写
5. `reference/review-checklist.md` 长出至少一行
6. 根目录 [README.md](../README.md) 的进度表已更新

**六条里做了四条就是做了四条。**说清缺哪两条。

## 模块索引

| 模块 | 章节 | 核心问题 |
|---|---|---|
| [m0-complexity](m0-complexity/README.zh.md) | 1–3 | 复杂性从哪来？为什么「能跑」不够？ |
| [m1-deep-modules](m1-deep-modules/README.zh.md) | 4–6 | 什么让模块变深？什么该藏在接口后面？ |
| [m2-abstraction-layers](m2-abstraction-layers/README.zh.md) | 7–9 | 谁吸收复杂性？这该是一个东西还是两个？ |
| [m3-design-process](m3-design-process/README.zh.md) | 10–11 | 能靠重新定义语义删掉一整类 bug 吗？ |
| [m4-naming-comments](m4-naming-comments/README.zh.md) | 12–15 | 注释必须承载什么代码承载不了的信息？ |
| [m5-consistency-maintenance](m5-consistency-maintenance/README.zh.md) | 16–18 | 如何在改动系统时不破坏它的设计？ |
| [m6-trends-tradeoffs](m6-trends-tradeoffs/README.zh.md) | 19–22 | 用 Ousterhout 自己的判据给 vibe coding 打分。 |
