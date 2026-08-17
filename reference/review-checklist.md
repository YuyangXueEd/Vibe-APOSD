# Design review checklist

**This file starts empty on purpose.**

The book already contains a summary of its design principles and a summary of its red flags.
Copying either one here would take about five minutes and would defeat the entire course. A
checklist you did not derive is a checklist you cannot apply, because applying it requires
recognizing the failure — and recognition is the thing that has to be built.

So this file grows by **at least one line per module**, written after the case study, in your
own words.

---

## Rules for a line in this checklist

A line earns its place only if all four hold:

1. **Checkable.** A reviewer can look at a diff and decide yes or no. "Is this module deep
   enough?" fails. "Does any caller of this module need to know how it stores its state?"
   passes.
2. **In your own words.** Not the book's phrasing. If you cannot restate it, you have not got
   it yet.
3. **Cited.** Chapter number, so the argument can be re-read when the line seems wrong.
4. **Earned.** You watched this failure happen in a case study in this repository. Link the
   finding.

A line that fails any of these is a line you will skip during a real review at 11pm, which
makes it worse than no line at all — it creates the impression of a check that is not
happening.

---

## The checklist

<!-- Format:

### C1 — <the question a reviewer asks>

| | |
|---|---|
| Chapter | Ch 4 |
| Earned in | [M1 findings](../modules/m1-deep-modules/case-study/findings.md) F2 |
| Applies to | new code / modifications / both |
| Catches | change amplification / cognitive load / unknown unknowns |

**How to check it.** <The concrete thing you look at.>

**What a violation looks like.** <From the case study, not invented.>

-->

_Empty. First line lands at the end of M0._

---

## Contributions by module

| Module | Lines contributed |
|---|---|
| M0 — Complexity | — |
| M1 — Deep Modules | — |
| M2 — Abstraction & Layers | — |
| M3 — Design Process | — |
| M4 — Comments & Naming | — |
| M5 — Consistency & Modification | — |
| M6 — Trends & Tradeoffs | — |

---

## At the end of the course

Compare this file against the book's own summary of design principles. Two questions worth
answering in writing:

- **What did you derive that the book also lists?** Confirmation that the reasoning worked.
- **What did you derive that the book does not list?** Either you found something the book
  omits because it predates coding agents — which is the interesting outcome and belongs in
  M6 — or you over-generalized from one case study. Both results are worth having, and
  telling them apart is the last exercise.
