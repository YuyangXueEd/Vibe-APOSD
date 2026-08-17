# APOSD chapter index

*A Philosophy of Software Design*, 2nd edition — John Ousterhout.

Two reading paths for the same text, courtesy of the community translation project:

- **English:** <https://yingang.github.io/aposd2e-zh/en/>
- **中文:** <https://yingang.github.io/aposd2e-zh/>

The right-hand column is **this course's** use for each chapter, not a summary of it. Read the
chapter; nothing here substitutes for it.

---

## Front matter

| Section | English | 中文 |
|---|---|---|
| Preface | [Preface](https://yingang.github.io/aposd2e-zh/en/) | [前言](https://yingang.github.io/aposd2e-zh/) |

---

## Chapters

| Ch | English | 中文 | Module | What this course uses it for |
|---|---|---|---|---|
| 1 | [Introduction](https://yingang.github.io/aposd2e-zh/en/ch01.html) | [介绍](https://yingang.github.io/aposd2e-zh/ch01.html) | M0 | Establishes complexity as *the* constraint — the premise everything else rests on |
| 2 | [The Nature of Complexity](https://yingang.github.io/aposd2e-zh/en/ch02.html) | [复杂性的本质](https://yingang.github.io/aposd2e-zh/ch02.html) | M0 | The three symptoms. Our vocabulary for diagnosing generated code |
| 3 | [Working Code Isn't Enough (Strategic vs. Tactical Programming)](https://yingang.github.io/aposd2e-zh/en/ch03.html) | [能工作的代码是不够的](https://yingang.github.io/aposd2e-zh/ch03.html) | M0 | The course's central claim: an agent is a tactical programmer by construction |
| 4 | [Modules Should Be Deep](https://yingang.github.io/aposd2e-zh/en/ch04.html) | [模块应该是深的](https://yingang.github.io/aposd2e-zh/ch04.html) | M1 | The depth test we apply to every generated module |
| 5 | [Information Hiding (and Leakage)](https://yingang.github.io/aposd2e-zh/en/ch05.html) | [信息隐藏和信息泄露](https://yingang.github.io/aposd2e-zh/ch05.html) | M1 | What to put in the prompt as a boundary, and what to leave out |
| 6 | [General-Purpose Modules are Deeper](https://yingang.github.io/aposd2e-zh/en/ch06.html) | [通用的模块是更深的](https://yingang.github.io/aposd2e-zh/ch06.html) | M1 | Calibrating generality when the cost of writing either version is zero |
| 7 | [Different Layer, Different Abstraction](https://yingang.github.io/aposd2e-zh/en/ch07.html) | [不同的层级，不同的抽象](https://yingang.github.io/aposd2e-zh/ch07.html) | M2 | Naming the pass-through failure mode agents fall into when asked for structure |
| 8 | [Pull Complexity Downwards](https://yingang.github.io/aposd2e-zh/en/ch08.html) | [下沉复杂性](https://yingang.github.io/aposd2e-zh/ch08.html) | M2 | Deciding who pays — the module or every one of its callers |
| 9 | [Better Together Or Better Apart?](https://yingang.github.io/aposd2e-zh/en/ch09.html) | [在一起更好还是分开更好？](https://yingang.github.io/aposd2e-zh/ch09.html) | M2 | Split-or-merge as a complexity argument rather than a file-length rule |
| 10 | [Define Errors Out Of Existence](https://yingang.github.io/aposd2e-zh/en/ch10.html) | [通过定义来规避错误](https://yingang.github.io/aposd2e-zh/ch10.html) | M3 | The alternative to "make it robust", which only ever adds branches |
| 11 | [Design it Twice](https://yingang.github.io/aposd2e-zh/en/ch11.html) | [设计两次](https://yingang.github.io/aposd2e-zh/ch11.html) | M3 | The cheapest prompt intervention in the book, and the one agents made cheaper still |
| 12 | [Why Write Comments? The Four Excuses](https://yingang.github.io/aposd2e-zh/en/ch12.html) | [不写注释的四个借口](https://yingang.github.io/aposd2e-zh/ch12.html) | M4 | Why volume of comments is not the metric anyone should be tracking |
| 13 | [Comments Should Describe Things that Aren't Obvious from the Code](https://yingang.github.io/aposd2e-zh/en/ch13.html) | [注释应该描述代码中难以理解的内容](https://yingang.github.io/aposd2e-zh/ch13.html) | M4 | The argument for deleting an agent's restating comments on sight |
| 14 | [Choosing Names](https://yingang.github.io/aposd2e-zh/en/ch14.html) | [选取名称](https://yingang.github.io/aposd2e-zh/ch14.html) | M4 | Vague names as a symptom of an unmade design decision |
| 15 | [Write The Comments First](https://yingang.github.io/aposd2e-zh/en/ch15.html) | [先写注释](https://yingang.github.io/aposd2e-zh/ch15.html) | M4 | Turned into a generation strategy: the comment becomes the spec |
| 16 | [Modifying Existing Code](https://yingang.github.io/aposd2e-zh/en/ch16.html) | [修改现有的代码](https://yingang.github.io/aposd2e-zh/ch16.html) | M5 | The highest-risk agent operation, and the most frequent one |
| 17 | [Consistency](https://yingang.github.io/aposd2e-zh/en/ch17.html) | [一致性](https://yingang.github.io/aposd2e-zh/ch17.html) | M5 | Auditing a diff against conventions nobody wrote down |
| 18 | [Code Should be Obvious](https://yingang.github.io/aposd2e-zh/en/ch18.html) | [代码应该是易理解的](https://yingang.github.io/aposd2e-zh/ch18.html) | M5 | Whose obviousness — the author's, or the next reader's |
| 19 | [Software Trends](https://yingang.github.io/aposd2e-zh/en/ch19.html) | [软件发展趋势](https://yingang.github.io/aposd2e-zh/ch19.html) | M6 | The rubric. We add vibe coding to Ousterhout's list and grade it |
| 20 | [Designing for Performance](https://yingang.github.io/aposd2e-zh/en/ch20.html) | [性能设计](https://yingang.github.io/aposd2e-zh/ch20.html) | M6 | Measure-before-optimize, applied to design intuition as well as to speed |
| 21 | [Decide What Matters](https://yingang.github.io/aposd2e-zh/en/ch21.html) | [决定什么是重要的](https://yingang.github.io/aposd2e-zh/ch21.html) | M6 | Where design investment still pays when code is free |
| 22 | [Conclusion](https://yingang.github.io/aposd2e-zh/en/ch22.html) | [结论](https://yingang.github.io/aposd2e-zh/ch22.html) | M6 | Closing position statement for the course |

---

## Back matter — the Summary appendix

The book closes with a summary of its design principles and a summary of its red flags.

**We deliberately do not copy it here.** Two reasons, and the second is the real one:

1. It is the author's work, and this repository cites rather than republishes.
2. A checklist you did not derive is a checklist you cannot apply. Applying a principle
   requires recognizing the failure in front of you, and recognition is the one thing that
   cannot be transferred by reading a list.

Our own version is built from scratch, one line per module, in
[`review-checklist.md`](review-checklist.md). At the end of M6 we compare the two — the
overlaps confirm the reasoning worked, and the differences are the interesting part.

---

## Citation convention

Cite by chapter number and the specific claim, not the chapter title:

> ✅ Ch 4 — interface complexity exceeds the implementation complexity it hides
> ❌ Ch 4 — "Modules Should Be Deep"

The title is a slogan and slogans are not arguments. Naming the claim forces you to have
understood which part of the chapter you are relying on, and it makes the citation checkable
by someone who disagrees.

Reproduce at most a short phrase, and only where the exact wording is the point. Never paste
passages.

## Buy the book

It is short, it is cheap, and the translation exists because people thought it was worth the
effort. <https://web.stanford.edu/~ouster/cgi-bin/aposd.php>
