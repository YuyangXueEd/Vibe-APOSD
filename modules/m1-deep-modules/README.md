# M1 — Deep Modules

| | |
|---|---|
| **Chapters** | [4 Modules Should Be Deep](https://yingang.github.io/aposd2e-zh/en/ch04.html) · [5 Information Hiding (and Leakage)](https://yingang.github.io/aposd2e-zh/en/ch05.html) · [6 General-Purpose Modules are Deeper](https://yingang.github.io/aposd2e-zh/en/ch06.html) |
| **中文** | [模块应该是深的](https://yingang.github.io/aposd2e-zh/ch04.html) · [信息隐藏和信息泄露](https://yingang.github.io/aposd2e-zh/ch05.html) · [通用的模块是更深的](https://yingang.github.io/aposd2e-zh/ch06.html) |
| **Core question** | What makes a module deep, and what belongs behind the interface? |
| **Prerequisite** | M0 — you need a definition of complexity before "deep" means anything |
| **Status** | Not started |

---

## Stop before you read

**Do not read Chapters 4–6 yet.** Reading is phase 3.

This module is especially easy to fake. "Modules should be deep" is a memorable slogan and you
can repeat it without being able to apply it. The dialogue exists to find out which one you
have.

## The core question

Depth is a ratio, not a size. A module is deep when the complexity of its interface is small
relative to the complexity it hides. Nothing about that requires the module to be large, and
nothing about a large module makes it deep.

The interesting consequence is that **you cannot judge depth from the implementation alone.**
You have to look at what a caller is forced to know. That is why this module is where the
course stops being retrospective code review and starts being prompt design.

## Where vibe coding breaks

`"Write a helper for X"` is an instruction about implementation. It reliably produces a
shallow module — an interface almost as complicated as the body it wraps, saving its callers
four lines while requiring them to understand six parameters.

The fix is upstream of generation. It is how you state a boundary without stating an
implementation, which turns out to be a genuinely difficult thing to write and is the real
skill this module trains.

Chapter 6 adds the calibration problem, and agents make it worse in a specific way: when
writing either version costs nothing, "somewhat general-purpose" stops being a compromise
between effort levels and becomes purely a judgment about future change. You now have to make
that judgment on the merits, with no effort gradient to hide behind.

## What you should be able to do afterward

- [ ] Recognize a shallow module and state the interface-vs-implementation cost that makes it one
- [ ] Find information leakage between two modules that look independent
- [ ] Judge an abstraction as too general, too specific, or appropriately general-purpose
- [ ] Write a task description that specifies a boundary without specifying an implementation

## The exercise

**Round A — the baseline.** Give the agent an HTTP client and say `"add rate limiting"`.
Nothing else.

**Round B — the constrained version.** Same task, but you supply the interface contract first:
what a caller may know, what it must not know, what happens under contention. Do not describe
an algorithm.

**Why rate limiting.** It is an unusually clean depth test. The naive version leaks its
algorithm through the interface — callers end up passing window sizes, or handling a
`RateLimitExceeded` they must themselves decide how to retry. The deep version hides a
genuinely hard problem behind roughly two methods. The gap between those two outcomes is large
enough to be unarguable, which matters for the first module where you are grading your own
prompt rather than the agent's code.

**What to look for.** Every parameter a caller must supply, every exception it must
distinguish, every ordering constraint it must respect. Those are the interface. Count them.

## Files

| Path | What goes there |
|---|---|
| [`socratic-log.md`](socratic-log.md) | Phases 1–3: the dialogue, distilled |
| [`case-study/README.md`](case-study/README.md) | The brief — both rounds, verbatim |
| `case-study/{python,typescript}/before/` | Round A output. Immutable. |
| `case-study/{python,typescript}/after/` | Round B output, plus the refactor of Round A |
| [`case-study/findings.md`](case-study/findings.md) | Critique, delta, cost |

Round B is a second experiment, not a refactor — keep the two distinguishable. The comparison
that matters is *constrained generation* against *unconstrained generation then repaired*, and
one of the two is cheaper.

## Done when

1. [ ] `socratic-log.md` covers phases 1–3, Grounding cites chapters
2. [ ] Both languages have `before/` and `after/`, and the code runs
3. [ ] `findings.md` counts interface surface before and after, not just describes it
4. [ ] At least one prompt in [`../../prompts/`](../../prompts/), **Observed effect** filled in
5. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) gained a line
6. [ ] Progress table in the root [README](../../README.md) updated
