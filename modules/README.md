# How a module works

**English** · [中文](README.zh.md)

Every module in this course runs the same six phases and produces the same three artifacts.
The uniformity is deliberate: once you have done M0, you know how M1 through M6 will run,
and the only thing you have to think about is the design question itself.

---

## The six phases

### Phase 1 — Intuition

The teacher poses one concrete scenario drawn from ordinary software engineering — request
validation, config loading, retry logic, a report generator. The learner answers from
experience.

**No reading.** Not the chapter, not the summary, not a hint about where this is going.
Reading first destroys the method: the learner adopts Ousterhout's position without ever
noticing it differed from their own, and nothing is learned because nothing was at stake.

Output: the scenario, the question, the answer, and — most importantly — **what that answer
implicitly commits to**. Making the implicit rule explicit is what gives phase 2 something
to test.

### Phase 2 — Probe

The teacher constructs the smallest case in which the learner's stated rule produces an
outcome they will not defend, and asks what they want to do about it.

Two valid outcomes:

- **The intuition breaks.** Mark the break point in the log. This is the good case.
- **The intuition holds.** Also a good case — but only if the learner can now say *why* it
  holds. An unexamined rule that happens to be correct is still unexamined.

The teacher never says "actually, the answer is". The contradiction does the teaching.

### Phase 3 — Grounding

Now, and only now, the chapter. The learner reads it and states the principle in their own
words. The teacher verifies that restatement against the text and cites chapters.

Two sections of the log matter more than the rest:

- **Where I disagree with Ousterhout.** Encouraged, not discouraged. A learner who agrees
  with every word of a book has probably not engaged with it.
- **What I got wrong in phase 1.** The specific delta between the intuition and the text.
  This is the actual learning, recorded in the only place it can be recorded.

### Phase 4 — Generate

The learner gives the agent a real task and the agent produces its **honest default output**
in both Python and TypeScript.

This is an experiment and it has one contamination rule: **no design constraints in the
prompt.** No "make it clean", no "use good abstractions", no mention of the module's
principle. The task given must be recorded verbatim in `case-study/README.md`, because a
paraphrased condition is not a condition.

The agent must not raise its game because review is coming, and must not sandbag to make a
better teaching example. Either one makes the result worthless. An honest baseline that turns
out to be *good* is a real finding — record it and move on.

`before/` is immutable once committed. Bugs in it are results, not mistakes.

### Phase 5 — Review & Refactor

**Critique first. Code second.** Write the findings, agree on what is actually wrong, and
only then touch the implementation.

Reversing this order is the most common way to waste a module. A refactor produced before the
critique is a refactor nobody can evaluate — the reasoning gets reconstructed after the fact
to justify whatever was written, and the learner ends up with a diff instead of a principle.

A finding must name a location and a principle. "This module is too shallow" is an opinion.
"`load_config` at `before/config.py:14` takes six parameters to save its caller four lines —
interface complexity exceeds the implementation complexity it hides (Ch 4)" is a finding.

Then refactor into `after/`, preserving observable behaviour. If behaviour had to change, that
is itself a separate finding worth writing down.

### Phase 6 — Extract

Distill the constraint that would have prevented the failure into `prompts/`, and add at
least one line to `reference/review-checklist.md`.

The prompt template has two required sections — **Observed effect** and **Known failure
modes** — and neither may be left empty. A prompt nobody has watched succeed *and* fail is a
superstition, and this repository is not in the business of producing more of those.

---

## Artifacts

| File | What it is | Written during |
|---|---|---|
| `README.md` | Module brief: chapters, core question, objectives, exercise | Before starting |
| `socratic-log.md` | The dialogue, distilled into teaching material | Phases 1–3 |
| `case-study/README.md` | The experimental brief: task verbatim, what was withheld | Phase 4 |
| `case-study/{python,typescript}/before/` | Raw agent output, immutable | Phase 4 |
| `case-study/{python,typescript}/after/` | The refactor | Phase 5 |
| `case-study/findings.md` | Critique, before/after delta, cost | Phase 5 |
| `prompts/m<N>-*.md` | The extracted constraint | Phase 6 |

Write the log **as you go**, at the end of each phase. A log reconstructed at the end of a
module is a summary of conclusions, and the conclusions were never the valuable part.

## Why both Python and TypeScript

Not for coverage, and not to reach more readers. They are a controlled comparison.

A dynamic language exposes interface complexity nakedly — a six-parameter function with three
optional dicts is visibly awful and nothing intercepts it. A static language moves some of
that complexity into a signature where it becomes *legible*, and hides other complexity
inside the type system where it becomes *invisible*. The same design failure lands
differently, and which language made it easier to see is recorded in every `findings.md`.

Write each version idiomatically for its language. A transliterated Python file with
semicolons teaches nothing.

## Definition of done

A module is finished when all six of these are true — see [CLAUDE.md](../CLAUDE.md) §9:

1. `socratic-log.md` covers phases 1–3, with chapter citations in Grounding
2. `case-study/` has `before/` and `after/` for both languages, and the code runs
3. `findings.md` names specific principles against specific lines, with the delta stated
4. At least one `prompts/` file, with **Observed effect** filled in from actual use
5. `reference/review-checklist.md` gained at least one line
6. The progress table in the root [README.md](../README.md) is updated

Four of six is four of six. Say which two are missing.

## Module index

| Module | Chapters | Core question |
|---|---|---|
| [m0-complexity](m0-complexity/) | 1–3 | Where does complexity come from, and why isn't "it works" enough? |
| [m1-deep-modules](m1-deep-modules/) | 4–6 | What makes a module deep, and what belongs behind the interface? |
| [m2-abstraction-layers](m2-abstraction-layers/) | 7–9 | Who absorbs the complexity, and should this be one thing or two? |
| [m3-design-process](m3-design-process/) | 10–11 | Can you delete a bug class by redefining the semantics? |
| [m4-naming-comments](m4-naming-comments/) | 12–15 | What must a comment carry that the code cannot? |
| [m5-consistency-maintenance](m5-consistency-maintenance/) | 16–18 | How do you change a system without degrading its design? |
| [m6-trends-tradeoffs](m6-trends-tradeoffs/) | 19–22 | Grade vibe coding by Ousterhout's own rubric. |
