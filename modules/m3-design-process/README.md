# M3 — Design Process

| | |
|---|---|
| **Chapters** | [10 Define Errors Out Of Existence](https://yingang.github.io/aposd2e-zh/en/ch10.html) · [11 Design it Twice](https://yingang.github.io/aposd2e-zh/en/ch11.html) |
| **中文** | [通过定义来规避错误](https://yingang.github.io/aposd2e-zh/ch10.html) · [设计两次](https://yingang.github.io/aposd2e-zh/ch11.html) |
| **Core question** | Can you delete a class of bugs by redefining what the operation means? |
| **Prerequisite** | M1, M2 — redefining an operation means moving its boundary |
| **Status** | Not started |

---

## Stop before you read

**Do not read Chapters 10–11 yet.** Reading is phase 3.

Chapter 10 in particular has a conclusion that sounds wrong the first time you hear it, which
makes it the best possible phase 1 material and the worst possible thing to spoil.

## The core question

The instinct on encountering an error condition is to handle it. Chapter 10 proposes something
that initially sounds irresponsible: change the definition of the operation so the condition is
not an error, and there is nothing left to handle.

The distinction that has to be nailed down before this becomes safe advice is the one between
*defined out of existence* and *silently swallowed*. They produce similar-looking code and
opposite outcomes, and the difference is the entire content of the chapter.

Chapter 11 is separate and much simpler: your first design is a first draft, and treating it as
a decision is how you end up living inside it.

## Where vibe coding breaks

Ask an agent to `"make it robust"` and you get defensive code — more branches, more exception
types, more handling, all of it dutifully correct and all of it complexity that a better
definition would have deleted. The prompt asked for robustness and got *handling*, because
handling is what robustness looks like from inside a function.

Chapter 11 is the cheapest intervention in the entire book, and agents made it cheaper. Two
designs used to cost two rounds of human effort, which is why nobody did it. Two designs now
cost one extra generation. The economics inverted, and almost nobody has updated their habits —
including, most of the time, the people who have read the chapter.

## What you should be able to do afterward

- [ ] Rewrite a specification so a previously-handled error is no longer an error at all
- [ ] Tell "defined out of existence" apart from "silently swallowed", with a test that distinguishes them
- [ ] Run a two-design comparison with an agent and judge the results on complexity
- [ ] Say why design-it-twice got cheaper with agents while design-once got more tempting

## The exercise

**Round A — the baseline.** `"Write a function that loads config from a file."` Nothing else.

Then enumerate the error paths in what comes back. The obvious design has at least four: file
missing, key absent, value of the wrong type, value malformed. Count them, and count how many
of them every caller has to know about.

**Round B — redesign the interface, not the error handling.** The intervention is not better
`try/except`. It is a different definition of what loading config *means* — one where several
of those four conditions stop being conditions. Do not skip ahead to the answer; derive it in
phase 2.

**Round C — design it twice.** Same original task, new prompt: two designs before any code,
with the tradeoffs stated. Compare the winner against Round A. The measurement that matters is
whether the second design was better *and* whether it was cheaper than fixing the first one.

**The trap.** A config loader that returns defaults for everything has not defined errors out
of existence — it has hidden a typo in a production config file until 3am. If your redesign
cannot distinguish "this key is absent and that is fine" from "this key is misspelled", it is
the evil twin. Write the test that tells them apart.

## Files

| Path | What goes there |
|---|---|
| [`socratic-log.md`](socratic-log.md) | Phases 1–3: the dialogue, distilled |
| [`case-study/README.md`](case-study/README.md) | The brief — all three rounds, verbatim |
| `case-study/{python,typescript}/before/` | Round A output. Immutable. |
| `case-study/{python,typescript}/after/` | Rounds B and C, kept separate |
| [`case-study/findings.md`](case-study/findings.md) | Critique, delta, cost |

## Done when

1. [ ] `socratic-log.md` covers phases 1–3, Grounding cites chapters
2. [ ] Both languages have `before/` and `after/`, and the code runs
3. [ ] `findings.md` counts error paths before and after, and includes the swallowing test
4. [ ] Round C's two designs are both recorded, including the one that lost
5. [ ] At least one prompt in [`../../prompts/`](../../prompts/), **Observed effect** filled in
6. [ ] [`../../reference/review-checklist.md`](../../reference/review-checklist.md) gained a line
7. [ ] Progress table in the root [README](../../README.md) updated
