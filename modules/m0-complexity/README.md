# M0 — The Nature of Complexity

**English** · [中文](README.zh.md)

| | |
|---|---|
| **Chapters** | [1 Introduction](https://yingang.github.io/aposd2e-zh/en/ch01.html) · [2 The Nature of Complexity](https://yingang.github.io/aposd2e-zh/en/ch02.html) · [3 Working Code Isn't Enough](https://yingang.github.io/aposd2e-zh/en/ch03.html) |
| **中文** | [介绍](https://yingang.github.io/aposd2e-zh/ch01.html) · [复杂性的本质](https://yingang.github.io/aposd2e-zh/ch02.html) · [能工作的代码是不够的](https://yingang.github.io/aposd2e-zh/ch03.html) |
| **Core question** | Where does complexity come from, and why is "it works" not a finish line? |
| **Prerequisite** | None — start here |
| **Status** | Not started |

---

## Stop before you read

**Do not read Chapters 1–3 yet.** Reading is phase 3, not phase 1.

If you read first, you will adopt Ousterhout's position without ever noticing it differed
from your own, and you will finish the module holding a set of borrowed opinions you cannot
apply. The dialogue has to catch your actual intuition while it is still yours.

*Already read the book?* Say so in the first message. The teacher will pose scenarios the
book does not directly answer, and will probe whether you can apply the vocabulary rather
than recite it.

## The core question

Everyone who uses a coding agent has watched the same thing happen: the output passes its
tests on day one, and by day thirty every change to it feels like surgery. The experience is
universal. The *mechanism* almost never gets named — and an unnamed mechanism can only be
complained about after the fact, never prevented.

This module is about naming it.

## Where vibe coding breaks

Chapter 3 draws a line between **tactical** programming (get this working now) and
**strategic** programming (invest so it stays workable). The uncomfortable observation this
whole course is built on:

> An agent optimizes for the prompt in front of it, carries no stake in next quarter's
> maintenance, and never gets tired. Tactical is not a mistake it makes. It is the default it
> has, unless you supply the other thing.

Chapter 2's three symptoms — change amplification, cognitive load, unknown unknowns — are the
diagnostic vocabulary. The third is the one that matters most here, because it is the only one
you cannot detect by reading the code you were shown.

## What you should be able to do afterward

- [ ] Point at a specific line in a real diff and say which of the three symptoms it produces
- [ ] Explain why an agent is tactical by construction rather than by accident
- [ ] Argue whether "strategic programming" is even purchasable when generating code is free
- [ ] Name one thing you would have to change in your own workflow to buy it

## The exercise

**Round A — the baseline.** Have the agent build a CLI that reads a CSV of orders and prints
a summary: total revenue, order count, top product. No design guidance in the prompt.

**Rounds B, C, D — three requirements it was never told about.** Apply them one at a time, in
separate turns, each phrased the way a stakeholder would phrase it:

1. Filter by date range
2. Accept JSON input as well as CSV
3. Emit JSON output as well as text, broken down by region

**Why four rounds and not one.** Complexity does not appear in the first generation — the
first generation usually looks fine, which is exactly why this is hard to argue about. It
appears in the *sequence*. Change amplification is by definition invisible until something
changes. A one-shot case study cannot demonstrate Chapter 2 and will quietly mislead you into
thinking the problem is code quality.

Record how many files each requirement touched. That number is the finding.

## Files

| Path | What goes there |
|---|---|
| [`socratic-log.md`](socratic-log.md) | Phases 1–3: the dialogue, distilled |
| [`case-study/README.md`](case-study/README.md) | The brief — task verbatim, what was withheld |
| `case-study/{python,typescript}/before/` | Raw agent output after each round. Immutable. |
| `case-study/{python,typescript}/after/` | The refactor |
| [`case-study/findings.md`](case-study/findings.md) | Critique, before/after delta, cost |

Keep each round in its own subdirectory under `before/` — `round-a/` through `round-d/` — so
the growth is visible in the tree rather than only in the git history.

## Done when

1. [ ] `socratic-log.md` covers phases 1–3, Grounding cites chapters
2. [ ] Both languages have `before/` (all four rounds) and `after/`, and the code runs
3. [ ] `findings.md` names principles against specific lines, with the delta stated
4. [ ] At least one prompt in [`../../prompts/`](../../prompts/), **Observed effect** filled in
5. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) gained a line
6. [ ] Progress table in the root [README](../../README.md) updated
