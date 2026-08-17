# Curriculum

**English** · [中文](CURRICULUM.zh.md)

All 22 chapters of *A Philosophy of Software Design* (2nd ed.), grouped into 7 modules.
Nothing is skipped.

Every chapter is linked in both languages, courtesy of the community translation project —
[English](https://yingang.github.io/aposd2e-zh/en/) and
[中文](https://yingang.github.io/aposd2e-zh/). A single index of all 22 chapters with each
one's role in this course lives in [reference/aposd-map.md](reference/aposd-map.md).

---

## How the grouping was chosen

The obvious approach is to cut the book into seven equal chunks. That is nearly right,
because Ousterhout already grouped his material — but two adjustments matter.

**Chapter 19 belongs at the end, not with the maintenance chapters.** "Software Trends" is
where Ousterhout takes agile, TDD, design patterns, and getters/setters, and grades each one
against his own criteria. It is a chapter of *judgment*, not of technique. Putting it last
means the learner spends six modules building a rubric and then turns that rubric on the
tool they use every day. That is the strongest possible ending for a course about vibe
coding, and it is wasted if it appears as a footnote to Chapter 18.

**Chapters 16–18 are one idea, not two.** Modifying existing code (16), consistency (17),
and obviousness (18) all answer a single question: how does a system stay coherent while
being changed by people who did not design it? That is also the exact question posed by an
agent editing a codebase it has never seen, which makes the module unusually load-bearing
for this course.

Everything else follows the book's own natural seams.

## Sequencing

Modules are ordered by dependency, not by difficulty. Later modules assume vocabulary built
earlier and will not make sense out of order:

- **M1–M2 need M0's definition of complexity.** "Deep module" is meaningless until you can
  say what complexity *is* and why "it works" is not the finish line.
- **M4 needs M1's information hiding.** The reason an agent's comments are worthless is not
  that they are badly written — it is that a comment restating code carries no information
  the code does not already carry. That argument requires M1.
- **M5 needs M2's layers.** You cannot audit a diff for consistency breaks without a model
  of which layer the change belongs in.
- **M6 needs all of it,** because grading a trend requires the rubric to already exist.

---

## M0 — The Nature of Complexity

**Directory:** [`modules/m0-complexity/`](modules/m0-complexity/)

| Ch | English | 中文 |
|---|---|---|
| 1 | [Introduction](https://yingang.github.io/aposd2e-zh/en/ch01.html) | [介绍](https://yingang.github.io/aposd2e-zh/ch01.html) |
| 2 | [The Nature of Complexity](https://yingang.github.io/aposd2e-zh/en/ch02.html) | [复杂性的本质](https://yingang.github.io/aposd2e-zh/ch02.html) |
| 3 | [Working Code Isn't Enough (Strategic vs. Tactical Programming)](https://yingang.github.io/aposd2e-zh/en/ch03.html) | [能工作的代码是不够的](https://yingang.github.io/aposd2e-zh/ch03.html) |

**Core question.** Where does complexity actually come from, and why is "it works" not a
finish line?

**Where vibe coding breaks.** Generated code passes its tests on day one and becomes
unmodifiable by day thirty. Everyone has experienced this. Almost nobody can name the
mechanism. Chapter 2 names three — change amplification, cognitive load, unknown unknowns —
and the third is the one that matters most with agents, because it is the one you cannot
detect by reading the code you were shown.

**By the end you can:**

- Point at a specific line in a real diff and say which of the three symptoms it produces
- Explain why an agent is a tactical programmer by construction rather than by accident
- Argue whether "strategic programming" is even purchasable when code generation is free
- State what you personally would have to change about your workflow to buy it

**Case study shape.** Have an agent build something small and honest — a CLI that ingests a
CSV of orders and prints a summary. Then extend it three times with requirements it was
never told about. The complexity does not appear in the first generation; it appears in the
sequence. That is the whole point of Chapter 2, and a single-shot case study cannot show it.

---

## M1 — Deep Modules

**Directory:** [`modules/m1-deep-modules/`](modules/m1-deep-modules/)

| Ch | English | 中文 |
|---|---|---|
| 4 | [Modules Should Be Deep](https://yingang.github.io/aposd2e-zh/en/ch04.html) | [模块应该是深的](https://yingang.github.io/aposd2e-zh/ch04.html) |
| 5 | [Information Hiding (and Leakage)](https://yingang.github.io/aposd2e-zh/en/ch05.html) | [信息隐藏和信息泄露](https://yingang.github.io/aposd2e-zh/ch05.html) |
| 6 | [General-Purpose Modules are Deeper](https://yingang.github.io/aposd2e-zh/en/ch06.html) | [通用的模块是更深的](https://yingang.github.io/aposd2e-zh/ch06.html) |

**Core question.** What makes a module deep, and how do you decide what belongs behind the
interface?

**Where vibe coding breaks.** "Write a helper for X" is an instruction about *implementation*
and reliably produces a shallow module: an interface almost as complicated as the body it
wraps. The fix is upstream of code generation — it is how you specify the boundary before
the agent writes anything. This module is where the course stops being retrospective review
and starts being prompt design.

**By the end you can:**

- Recognize a shallow module and state the interface-vs-implementation cost that makes it one
- Find information leakage across two modules that appear independent
- Judge whether an abstraction is too general, too specific, or "somewhat general-purpose"
- Write a task description that specifies a boundary without specifying an implementation

**Case study shape.** Rate limiting on an HTTP client. It is a textbook depth test: the naive
version leaks its algorithm through the interface, and the deep version hides a genuinely
hard problem behind about two methods. Compare what the agent produces when told *"add rate
limiting"* against what it produces when given an interface contract.

---

## M2 — Abstraction and Layers

**Directory:** [`modules/m2-abstraction-layers/`](modules/m2-abstraction-layers/)

| Ch | English | 中文 |
|---|---|---|
| 7 | [Different Layer, Different Abstraction](https://yingang.github.io/aposd2e-zh/en/ch07.html) | [不同的层级，不同的抽象](https://yingang.github.io/aposd2e-zh/ch07.html) |
| 8 | [Pull Complexity Downwards](https://yingang.github.io/aposd2e-zh/en/ch08.html) | [下沉复杂性](https://yingang.github.io/aposd2e-zh/ch08.html) |
| 9 | [Better Together Or Better Apart?](https://yingang.github.io/aposd2e-zh/en/ch09.html) | [在一起更好还是分开更好？](https://yingang.github.io/aposd2e-zh/ch09.html) |

**Core question.** Who should absorb the complexity, and should this be one thing or two?

**Where vibe coding breaks.** Agents fail in *both* directions, which is what makes this
module interesting. Ask for a feature and you often get one flat function doing five things.
Ask for clean architecture and you often get four classes where each method forwards to the
next — a pass-through chain that adds names without adding abstraction. Both are layer
failures, and the diagnosis differs.

**By the end you can:**

- Identify pass-through methods, pass-through variables, and decorator classes by name
- Decide split-or-merge from a complexity argument rather than from taste or file length
- Say who pays when complexity is pushed *up* to callers instead of *down* into the module
- Notice when "separation of concerns" has been applied to things that were never separate

**Case study shape.** Add a caching layer to a data access path. Caching is the cleanest
available test of Chapter 7, because a cache that leaks its existence upward has failed at
exactly one job. Watch where the agent puts the cache-invalidation decision.

---

## M3 — Design Process

**Directory:** [`modules/m3-design-process/`](modules/m3-design-process/)

| Ch | English | 中文 |
|---|---|---|
| 10 | [Define Errors Out Of Existence](https://yingang.github.io/aposd2e-zh/en/ch10.html) | [通过定义来规避错误](https://yingang.github.io/aposd2e-zh/ch10.html) |
| 11 | [Design it Twice](https://yingang.github.io/aposd2e-zh/en/ch11.html) | [设计两次](https://yingang.github.io/aposd2e-zh/ch11.html) |

**Core question.** Can you delete an entire class of bugs by redefining what the operation
means? And why is your first design almost never the one to ship?

**Where vibe coding breaks.** Asking an agent to "make it robust" produces defensive code:
more branches, more exception types, more handling. Chapter 10 argues the opposite move —
change the semantics so the error condition does not exist and there is nothing to handle.
Chapter 11 is the cheapest prompt intervention in the whole book: *give me two designs before
you write any code.* Two designs cost one extra generation, which is now nearly free.

**By the end you can:**

- Rewrite a specification so a previously-handled error is no longer an error at all
- Tell "defined out of existence" apart from "silently swallowed", which is its evil twin
- Run a two-design comparison with an agent and judge the results on complexity
- Explain why design-it-twice got *cheaper* with agents while design-once got more tempting

**Case study shape.** Config loading. Missing file, absent key, wrong type, malformed value —
four error paths in the obvious design, and a much smaller number in a better one. Generate
the obvious version first, then redesign the interface rather than the error handling.

---

## M4 — Comments and Naming

**Directory:** [`modules/m4-naming-comments/`](modules/m4-naming-comments/)

| Ch | English | 中文 |
|---|---|---|
| 12 | [Why Write Comments? The Four Excuses](https://yingang.github.io/aposd2e-zh/en/ch12.html) | [不写注释的四个借口](https://yingang.github.io/aposd2e-zh/ch12.html) |
| 13 | [Comments Should Describe Things that Aren't Obvious from the Code](https://yingang.github.io/aposd2e-zh/en/ch13.html) | [注释应该描述代码中难以理解的内容](https://yingang.github.io/aposd2e-zh/ch13.html) |
| 14 | [Choosing Names](https://yingang.github.io/aposd2e-zh/en/ch14.html) | [选取名称](https://yingang.github.io/aposd2e-zh/ch14.html) |
| 15 | [Write The Comments First](https://yingang.github.io/aposd2e-zh/en/ch15.html) | [先写注释](https://yingang.github.io/aposd2e-zh/ch15.html) |

**Core question.** What information must a comment carry that the code cannot carry itself?

**Where vibe coding breaks.** Agents produce a great deal of comment text with near-zero
information content — `# increment the counter`, docstrings that restate the signature in
prose. It is tempting to file this as a style complaint. It is not. A comment that repeats
the code is *evidence that no design decision was recorded*, because there was no design
decision to record. Chapter 15 then flips the whole thing into a technique: if comments come
first, they become the specification the agent writes against.

**By the end you can:**

- Classify any comment as interface, data structure, implementation, or cross-module
- Delete restating comments on sight and justify it from Chapter 13 rather than from taste
- Detect a vague name and say which specific misunderstanding it invites
- Use comment-first as a generation strategy, not just a review criterion

**Case study shape.** Take a non-trivial function the agent wrote in an earlier module and
ask it to document that function. Then reverse the order: write the interface comment
yourself and have the agent implement against it. The second artifact is usually a different
*design*, not merely differently commented — that difference is the finding.

---

## M5 — Consistency and Modification

**Directory:** [`modules/m5-consistency-maintenance/`](modules/m5-consistency-maintenance/)

| Ch | English | 中文 |
|---|---|---|
| 16 | [Modifying Existing Code](https://yingang.github.io/aposd2e-zh/en/ch16.html) | [修改现有的代码](https://yingang.github.io/aposd2e-zh/ch16.html) |
| 17 | [Consistency](https://yingang.github.io/aposd2e-zh/en/ch17.html) | [一致性](https://yingang.github.io/aposd2e-zh/ch17.html) |
| 18 | [Code Should be Obvious](https://yingang.github.io/aposd2e-zh/en/ch18.html) | [代码应该是易理解的](https://yingang.github.io/aposd2e-zh/ch18.html) |

**Core question.** How do you change a system without degrading the design you started with?

**Where vibe coding breaks.** This is the highest-risk agent operation there is, and it is
also the most common one. An agent editing code it did not write reliably produces: a local
fix that duplicates an abstraction already present three files away; a silent break of a
convention nobody wrote down; a stale comment above correctly-changed code. Each is
individually trivial. Chapter 16's argument is that the *accumulation* is how designs die,
and the accumulation is exactly what agents accelerate.

**By the end you can:**

- Audit a diff for consistency breaks against conventions that were never documented
- Tell a strategic edit from a tactical one in someone else's pull request
- Say what an agent must be given up front to make a non-degrading change
- Recognize when "it's obvious" means "I wrote it and I remember"

**Case study shape.** Use M2's `after/` code as the existing system, and ask an agent — with
no course context — for a new feature. This is the only module where the case study builds on
a previous one, and that is deliberate: you cannot study code modification without code that
already has a design worth degrading.

---

## M6 — Trends, Tradeoffs, and Judgment

**Directory:** [`modules/m6-trends-tradeoffs/`](modules/m6-trends-tradeoffs/)

| Ch | English | 中文 |
|---|---|---|
| 19 | [Software Trends](https://yingang.github.io/aposd2e-zh/en/ch19.html) | [软件发展趋势](https://yingang.github.io/aposd2e-zh/ch19.html) |
| 20 | [Designing for Performance](https://yingang.github.io/aposd2e-zh/en/ch20.html) | [性能设计](https://yingang.github.io/aposd2e-zh/ch20.html) |
| 21 | [Decide What Matters](https://yingang.github.io/aposd2e-zh/en/ch21.html) | [决定什么是重要的](https://yingang.github.io/aposd2e-zh/ch21.html) |
| 22 | [Conclusion](https://yingang.github.io/aposd2e-zh/en/ch22.html) | [结论](https://yingang.github.io/aposd2e-zh/ch22.html) |

**Core question.** Ousterhout grades agile, TDD, design patterns, and getters/setters against
his own criteria. Apply the same rubric to vibe coding — and be willing to reach a
conclusion you did not want.

**Where vibe coding breaks.** Or does not. This module is the one that is allowed to come out
in favour. Chapter 21 asks what actually deserves attention; Chapter 20 insists performance
work be measured rather than assumed, which is the same discipline this whole course applies
to design. The output is a calibrated rule for when to let the agent run at full speed and
when to stop it — not a blanket policy in either direction.

**By the end you can:**

- Grade vibe coding by Chapter 19's criteria, in writing, with the negative case included
- Say which parts of design investment pay off under free code generation and which stop
  paying
- State your own threshold for slowing down, in terms specific enough to be wrong
- Defend a position on whether APOSD's advice needs revision for this era, or merely
  enforcement

**Case study shape.** No new code generation. Instead: re-read all six earlier
`findings.md` files as a dataset, and write the grade. The evidence was collected across the
whole course precisely so this module can be empirical instead of rhetorical.

---

## Out of scope

This course does not cover testing strategy, CI, code review process, team practices, or
prompt engineering as a general subject. Where they touch design they appear inside a
module; otherwise they are somebody else's course.
