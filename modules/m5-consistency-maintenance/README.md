# M5 — Consistency and Modification

| | |
|---|---|
| **Chapters** | [16 Modifying Existing Code](https://yingang.github.io/aposd2e-zh/en/ch16.html) · [17 Consistency](https://yingang.github.io/aposd2e-zh/en/ch17.html) · [18 Code Should be Obvious](https://yingang.github.io/aposd2e-zh/en/ch18.html) |
| **中文** | [修改现有的代码](https://yingang.github.io/aposd2e-zh/ch16.html) · [一致性](https://yingang.github.io/aposd2e-zh/ch17.html) · [代码应该是易理解的](https://yingang.github.io/aposd2e-zh/ch18.html) |
| **Core question** | How do you change a system without degrading the design you started with? |
| **Prerequisite** | **M2 specifically** — this module modifies M2's `after/` code |
| **Status** | Not started |

---

## Stop before you read

**Do not read Chapters 16–18 yet.** Reading is phase 3.

## The core question

Three chapters, one question. Modifying existing code (16), consistency (17), and obviousness
(18) are all asking how a system stays coherent while being changed by people who did not
design it.

That framing should sound familiar, because it is a precise description of an agent editing
your codebase.

## Where vibe coding breaks

This is the highest-risk agent operation there is, and — inconveniently — also the most
frequent. An agent editing code it did not write reliably produces some combination of:

- A **local fix that duplicates an abstraction** already sitting three files away, unread
- A **silent break of a convention** nobody ever wrote down, because it was only ever a pattern
- A **stale comment** left above correctly-changed code, now confidently wrong
- A change made in **the wrong layer**, because the wrong layer was the one in context

Every one of these is individually trivial and individually defensible. Chapter 16's argument is
that the *accumulation* is how designs die — and accumulation is precisely what an agent
accelerates, because the per-change cost that used to throttle it has gone to zero.

Chapter 18 supplies the uncomfortable question to sit with: obvious *to whom?* "It's obvious"
frequently decodes to "I wrote it and I still remember why." An agent has no memory of writing
it at all, which makes it a surprisingly good proxy for the next reader.

## What you should be able to do afterward

- [ ] Audit a diff for consistency breaks against conventions that were never documented
- [ ] Tell a strategic edit from a tactical one in someone else's pull request
- [ ] Say what an agent must be given up front to make a non-degrading change
- [ ] Recognize when "it's obvious" means "I wrote it and I remember"

## The exercise

**Round A — the baseline.** Take M2's `after/` code — the cached data access path you refactored
— and ask an agent for a new feature. Two conditions matter and both are easy to get wrong:

1. **A fresh session with no course context.** No `CLAUDE.md`, no design constraints, no mention
   of APOSD. Otherwise the baseline is contaminated and this module produces nothing.
2. **A feature that touches the layer boundary you established.** Something like bulk lookup,
   or per-tenant isolation. A feature that lands entirely inside one file cannot degrade a
   design and cannot demonstrate Chapter 16.

Then audit the diff against the four failure modes above, one at a time, by name.

**Round B — the constrained edit.** Same feature, same starting code, but you supply what the
agent needed: the conventions that were never written down, the layer the change belongs in,
what must not change. Compare.

**Why this module builds on M2.** You cannot study code modification without code that already
has a design worth degrading. Generating a throwaway system for the purpose would defeat it —
you would know it was disposable and would not care what happened to it. Using your own
refactor means the degradation costs you something, which is the only condition under which
this module teaches anything.

## Files

| Path | What goes there |
|---|---|
| [`socratic-log.md`](socratic-log.md) | Phases 1–3: the dialogue, distilled |
| [`case-study/README.md`](case-study/README.md) | The brief — both rounds, plus the exact M2 commit used |
| `case-study/{python,typescript}/before/` | The unconstrained diff applied to M2's code. Immutable. |
| `case-study/{python,typescript}/after/` | The constrained edit, plus the repair of Round A |
| [`case-study/findings.md`](case-study/findings.md) | Critique, delta, cost |

Record the **M2 commit hash** you started from. Without it, nobody can reproduce the diff, and
the case study becomes an anecdote.

## Done when

1. [ ] `socratic-log.md` covers phases 1–3, Grounding cites chapters
2. [ ] Both languages have `before/` and `after/`, and the code runs
3. [ ] The diff is audited against all four failure modes, each named explicitly
4. [ ] The M2 starting commit is recorded in `case-study/README.md`
5. [ ] At least one prompt in [`../../prompts/`](../../prompts/), tagged `before-modification`
6. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) gained a line
7. [ ] Progress table in the root [README](../../README.md) updated
