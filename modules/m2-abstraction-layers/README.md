# M2 — Abstraction and Layers

| | |
|---|---|
| **Chapters** | [7 Different Layer, Different Abstraction](https://yingang.github.io/aposd2e-zh/en/ch07.html) · [8 Pull Complexity Downwards](https://yingang.github.io/aposd2e-zh/en/ch08.html) · [9 Better Together Or Better Apart?](https://yingang.github.io/aposd2e-zh/en/ch09.html) |
| **中文** | [不同的层级，不同的抽象](https://yingang.github.io/aposd2e-zh/ch07.html) · [下沉复杂性](https://yingang.github.io/aposd2e-zh/ch08.html) · [在一起更好还是分开更好？](https://yingang.github.io/aposd2e-zh/ch09.html) |
| **Core question** | Who absorbs the complexity, and should this be one thing or two? |
| **Prerequisite** | M1 — layers are made of modules, and you need the depth test first |
| **Status** | Not started |

---

## Stop before you read

**Do not read Chapters 7–9 yet.** Reading is phase 3.

## The core question

Two questions that turn out to be the same question.

*Who absorbs the complexity?* Every awkward detail lands somewhere. Chapter 8 argues it should
land inside the module, once, rather than in every caller, repeatedly — and the reason is
arithmetic, not aesthetics.

*Should this be one thing or two?* Chapter 9 refuses to answer with a rule about file length or
function size. The answer comes from whether splitting reduces total complexity or merely
relocates it and adds an interface to the bill.

## Where vibe coding breaks

This module is interesting because agents fail in **both** directions, and the two failures
look like opposites while sharing a cause.

Ask for a feature and you often get one flat function doing five things. Ask for *clean
architecture* and you often get four classes in which each method forwards to the next — a
pass-through chain that adds names, files, and indirection without adding a single new
abstraction. Chapter 7 has a term for it, and once you have the term you cannot unsee it.

Both are the same failure: no decision was made about what each layer is *for*. One flattened
the decision away, the other performed the appearance of having made it.

## What you should be able to do afterward

- [ ] Identify pass-through methods, pass-through variables, and decorator classes by name
- [ ] Argue split-or-merge from complexity rather than from file length or taste
- [ ] Say who pays when complexity is pushed *up* to callers instead of *down* into a module
- [ ] Notice when "separation of concerns" was applied to things that were never separate

## The exercise

**Round A — the baseline.** Take a data access path (a user lookup backed by a database is
enough) and say `"add caching"`.

**Round B — after grounding.** Same task, with the layer boundary specified.

**Why caching.** It is the cleanest available test of Chapter 7, because a cache has exactly
one job at the interface level: *not existing*. A caller that has to know a cache is there —
or worse, has to decide about it — has been handed a leak, and the leak is visible in the
signature.

**The specific tell to watch for.** A `use_cache: bool = False` parameter appearing on the
public lookup function. It is the single most common way an agent surfaces a caching decision
upward, it looks like helpful flexibility, and it means every caller now has to have an opinion
about cache semantics. Also watch where invalidation lands — if the caller is responsible for
calling `invalidate()`, the cache is not a layer, it is a chore.

**Keep the output.** M5 uses this module's `after/` code as its existing system, so the
refactor here needs to be a design worth degrading. It is the one place in the course where
being sloppy has a downstream cost.

## Files

| Path | What goes there |
|---|---|
| [`socratic-log.md`](socratic-log.md) | Phases 1–3: the dialogue, distilled |
| [`case-study/README.md`](case-study/README.md) | The brief — both rounds, verbatim |
| `case-study/{python,typescript}/before/` | Round A output. Immutable. |
| `case-study/{python,typescript}/after/` | The refactor — **M5's starting point** |
| [`case-study/findings.md`](case-study/findings.md) | Critique, delta, cost |

## Done when

1. [ ] `socratic-log.md` covers phases 1–3, Grounding cites chapters
2. [ ] Both languages have `before/` and `after/`, and the code runs
3. [ ] `findings.md` records where the cache leaked and where invalidation ended up
4. [ ] At least one prompt in [`../../prompts/`](../../prompts/), **Observed effect** filled in
5. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) gained a line
6. [ ] Progress table in the root [README](../../README.md) updated
7. [ ] `after/` is clean enough to hand to M5 as a real system
