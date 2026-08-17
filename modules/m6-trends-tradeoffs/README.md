# M6 — Trends, Tradeoffs, and Judgment

| | |
|---|---|
| **Chapters** | [19 Software Trends](https://yingang.github.io/aposd2e-zh/en/ch19.html) · [20 Designing for Performance](https://yingang.github.io/aposd2e-zh/en/ch20.html) · [21 Decide What Matters](https://yingang.github.io/aposd2e-zh/en/ch21.html) · [22 Conclusion](https://yingang.github.io/aposd2e-zh/en/ch22.html) |
| **中文** | [软件发展趋势](https://yingang.github.io/aposd2e-zh/ch19.html) · [性能设计](https://yingang.github.io/aposd2e-zh/ch20.html) · [决定什么是重要的](https://yingang.github.io/aposd2e-zh/ch21.html) · [结论](https://yingang.github.io/aposd2e-zh/ch22.html) |
| **Core question** | Grade vibe coding by Ousterhout's own rubric for software trends. |
| **Prerequisite** | **All six previous modules**, including their `findings.md` files |
| **Status** | Not started |

---

## Stop before you read

**Do not read Chapter 19 yet** — it is the one chapter in the book where being spoiled costs
the most. In it, Ousterhout takes agile development, unit testing, test-driven development,
design patterns, and getters and setters, and grades each one against the criteria he spent
eighteen chapters building. Some pass. Some do not. Reading his grades before assigning your
own turns the capstone into agreement practice.

Chapters 20–22 can be read during phase 3 as usual.

## The core question

You have spent six modules building a rubric. This module turns it on the tool you use every
day.

The specific demand: **be willing to reach a conclusion you did not want.** A course that
frames vibe coding as a hazard for six modules and then concludes it is a hazard has proven
nothing — it has only confirmed its own framing. If the evidence in your `findings.md` files
says the honest baselines were mostly fine, that is the finding, and it goes in the verdict.

Chapter 20 supplies the discipline that makes this possible. Its rule about performance —
measure, do not assume — applies with full force to design intuition, and this module is where
it gets applied to *this course's own claims*. Every `findings.md` has a delta table for
exactly this reason.

## Where vibe coding breaks

Or does not. This is the one module allowed to come out in favour.

Chapter 21 asks what actually deserves attention, and it is the question this course has been
implicitly deferring. If code generation is free, some kinds of design investment stop paying:
why carefully design an interface you can regenerate in nine seconds? The counter-argument is
that regenerating is cheap while *understanding* is not, and interfaces are the units of
understanding — but that is an argument, not a proof, and it is your job here to test it
against six modules of your own data.

The output is not a policy. It is a **threshold**: the specific conditions under which you let
the agent run at full speed, and the specific conditions under which you stop it. Stated
precisely enough that you could be shown to be wrong.

## What you should be able to do afterward

- [ ] Grade vibe coding by Chapter 19's criteria, in writing, with the negative case included
- [ ] Say which parts of design investment still pay under free code generation, and which stop
- [ ] State your own threshold for slowing down, specifically enough to be falsifiable
- [ ] Defend a position on whether APOSD needs revision for this era, or merely enforcement

## The exercise

### Part 1 — the measurement trap (Ch 20)

One short generation round, to keep this module honest rather than purely retrospective.

Take any code from an earlier module and say `"make this faster"`. Nothing else — no profile,
no benchmark, no statement of what is slow.

Then measure what the agent optimized and what was actually hot. Chapter 20's argument is that
optimization without measurement is guesswork with extra steps, and an agent asked to optimize
will always find *something* to change. Whether that something mattered is an empirical
question that takes ten minutes to settle.

### Part 2 — the verdict (Ch 19, 21, 22)

No new code. Instead, read all six previous `findings.md` files as a dataset and write
[`case-study/verdict.md`](case-study/). It must contain:

1. **Vibe coding, graded by Chapter 19's criteria** — the same treatment Ousterhout gives agile
   and TDD, with the same willingness to split the verdict rather than issue one.
2. **The evidence table.** Across six modules: how often was the honest baseline actually bad?
   Which failure modes recurred? Which appeared once and never again? Pull the numbers from the
   delta tables; do not reconstruct them from memory.
3. **The cost accounting.** Every `findings.md` recorded time to generate, review, and refactor.
   Was constrained generation cheaper end to end than unconstrained-then-repaired? You now have
   six data points on a question most people answer by vibes.
4. **Your threshold**, stated falsifiably.
5. **Checklist vs. book.** Compare [`reference/review-checklist.md`](../../reference/review-checklist.md)
   against the book's own summary appendix. Overlaps confirm the derivation worked. Divergences
   are either something the book omits because it predates coding agents — the interesting
   outcome — or somewhere you over-generalized from a single case study. Telling those two apart
   is the final exercise of the course.

## Files

| Path | What goes there |
|---|---|
| [`socratic-log.md`](socratic-log.md) | Phases 1–3: the dialogue, distilled |
| [`case-study/README.md`](case-study/README.md) | The brief for Part 1 |
| `case-study/{python,typescript}/before/` | Part 1: the unmeasured optimization. Immutable. |
| `case-study/{python,typescript}/after/` | Part 1: the measured one, with the numbers |
| [`case-study/findings.md`](case-study/findings.md) | Part 1's findings |
| `case-study/verdict.md` | **Part 2 — the capstone.** Create this file. |

## Done when

1. [ ] `socratic-log.md` covers phases 1–3, Grounding cites chapters
2. [ ] Part 1 has both languages, with **actual measurements**, not estimates
3. [ ] `verdict.md` contains all five required sections
4. [ ] The verdict cites specific `findings.md` files rather than general impressions
5. [ ] The negative case is present — at least one place the evidence went against your prior
6. [ ] Progress table in the root [README](../../README.md) updated, course marked complete
