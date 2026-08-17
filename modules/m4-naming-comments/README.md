# M4 — Comments and Naming

**English** · [中文](README.zh.md)

| | |
|---|---|
| **Chapters** | [12 Why Write Comments? The Four Excuses](https://yingang.github.io/aposd2e-zh/en/ch12.html) · [13 Comments Should Describe Things that Aren't Obvious from the Code](https://yingang.github.io/aposd2e-zh/en/ch13.html) · [14 Choosing Names](https://yingang.github.io/aposd2e-zh/en/ch14.html) · [15 Write The Comments First](https://yingang.github.io/aposd2e-zh/en/ch15.html) |
| **中文** | [不写注释的四个借口](https://yingang.github.io/aposd2e-zh/ch12.html) · [注释应该描述代码中难以理解的内容](https://yingang.github.io/aposd2e-zh/ch13.html) · [选取名称](https://yingang.github.io/aposd2e-zh/ch14.html) · [先写注释](https://yingang.github.io/aposd2e-zh/ch15.html) |
| **Core question** | What information must a comment carry that the code cannot? |
| **Prerequisite** | M1 — the argument depends on information hiding |
| **Status** | Not started |

---

## Stop before you read

**Do not read Chapters 12–15 yet.** Reading is phase 3.

## The core question

Not "should you write comments" — that question is a trap and Chapter 12 dismantles the four
usual answers to it. The real question is what a comment can carry that code cannot, because
that is the only thing worth writing down.

A comment that restates the code carries zero information by construction. It is not a
low-value comment; it is a *negative*-value comment, because it will eventually be wrong and
will then actively mislead someone.

## Where vibe coding breaks

Agents produce a great deal of comment text with near-zero information content —
`# increment the counter`, docstrings that render the signature back as prose, section banners
above three-line blocks. It is tempting to file this as a style complaint and set up a linter.

That reading misses the finding. **A comment that repeats the code is evidence that no design
decision was recorded — because there was no design decision to record.** The comment is a
symptom. The absence of any statement about *why*, about invariants, about what the caller must
not do, is the disease. Chapter 14 makes the same point about names: a vague name is not sloppy
writing, it is an unmade decision, and the vagueness is where the decision should have been.

Chapter 15 then inverts the whole thing into a technique. If comments come first, they stop
being documentation and become the specification the agent writes against — which is why this
module belongs in a course about prompting and not only in a course about style.

## What you should be able to do afterward

- [ ] Classify any comment as interface, data structure, implementation, or cross-module
- [ ] Delete a restating comment and justify it from Chapter 13 rather than from taste
- [ ] Detect a vague name and say which specific misunderstanding it invites
- [ ] Use comments-first as a generation strategy, not just as a review criterion

## The exercise

**Round A — the baseline.** Take a non-trivial function the agent wrote in M1 or M2 and ask it
to document that function. Then classify **every** comment it produced into one of Chapter 13's
categories, and mark which ones carry information the code does not.

Report the ratio honestly. Modern agents sometimes do this well, and a good result is a real
finding — one that belongs in M6's evidence pile.

**Round B — invert the order.** Write the interface comment yourself, before any code exists.
State what the function guarantees, what the caller must not assume, and what invariant holds.
Then have the agent implement against it.

**What to look for in Round B.** Not better comments — a different **design**. The usual
outcome is a different signature, a different error contract, sometimes a different number of
functions. That difference is the finding, and it is why Chapter 15 sits in the design half of
the book rather than the documentation half.

**Naming, in passing.** Every time you reach for a name during the refactor, write down what
you rejected and why. Chapter 14's argument is much easier to feel from your own three
discarded candidates than from a worked example.

## Files

| Path | What goes there |
|---|---|
| [`socratic-log.md`](socratic-log.md) | Phases 1–3: the dialogue, distilled |
| [`case-study/README.md`](case-study/README.md) | The brief — both rounds, verbatim |
| `case-study/{python,typescript}/before/` | Round A: the function plus generated comments. Immutable. |
| `case-study/{python,typescript}/after/` | Round B: comment-first implementation |
| [`case-study/findings.md`](case-study/findings.md) | Critique, delta, cost |

## Done when

1. [ ] `socratic-log.md` covers phases 1–3, Grounding cites chapters
2. [ ] Both languages have `before/` and `after/`, and the code runs
3. [ ] Every Round A comment is classified, with the information-bearing ratio stated
4. [ ] `findings.md` says whether Round B changed the *design*, not just the comments
5. [ ] At least one prompt in [`../../prompts/`](../../prompts/), **Observed effect** filled in
6. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) gained a line
7. [ ] Progress table in the root [README](../../README.md) updated
