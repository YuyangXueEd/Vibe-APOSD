# M1 Findings — Rate limiting on an HTTP client

**Principles applied:** module depth and information hiding (Ch 4, Ch 5)

---

## Baseline honesty check

Answer before writing any finding. If the baseline was contaminated, the rest of this file is
commentary rather than evidence, and it should say so at the top.

| | |
|---|---|
| Did the generating agent know the output would be reviewed against APOSD? | |
| Were project instructions (`CLAUDE.md`) loaded during generation? | |
| Any urge-to-restructure noted at generation time but suppressed? | |
| Verdict | clean baseline / contaminated / partially contaminated |

<!-- An honest baseline that turned out GOOD is a valid and interesting result. Say so
     plainly. Do not go looking for faults to justify the exercise. -->

---

## Findings

### F1 — _one-line claim_

| | |
|---|---|
| Location | `python/before/_file_.py:_line_` |
| Also in TS? | yes / no / differently — see Language comparison |
| Principle | Ch _n_ — _the specific claim, not the chapter title_ |
| Symptom | change amplification / cognitive load / unknown unknowns |
| Severity | design-breaking / annoying / cosmetic |

**The claim.**

**Why this is a design problem and not a style preference.**

<!-- Required. If you cannot answer this, it is a style preference and belongs in a linter
     config, not in a findings file. -->

**What changed in `after/`.**

---

### F2 — _one-line claim_

<!-- Same structure. Three to five real findings beat twelve padded ones. -->

---

## Delta

| Measure | Before | After | Note |
|---|---|---|---|
| Public interface surface — params + methods a caller must know | | | |
| Call sites that must change to add _a plausible new requirement_ | | | Name the requirement |
| Files to read to understand one behaviour end to end | | | |
| Distinct concepts a newcomer must hold at once | | | |
| Lines of code | | | For honesty, not as a goal |

<!-- Lines of code frequently go UP after a good refactor: a deep module absorbs complexity
     that used to be spread across its callers. If LOC dropped sharply, check that a feature
     was not quietly deleted. -->

---

## Language comparison

| | Python | TypeScript |
|---|---|---|
| Did the same failure appear? | | |
| Easier or harder to see, and why? | | |
| Did the type system expose it, hide it, or relocate it? | | |
| Did the refactor differ in shape, not just syntax? | | |

<!-- The most useful entries here are the asymmetries. Two identical columns usually mean the
     TypeScript version was transliterated rather than written. -->

---

## What the agent would have needed to know up front

<!-- Write this BEFORE writing the prompt in prompts/. State it as information the agent
     lacked, not as an instruction — the instruction is derived from it in phase 6. -->

---

## Cost

| | |
|---|---|
| Time to generate `before/` | |
| Time to review and write findings | |
| Time to refactor into `after/` | |
| Would a constrained prompt have been cheaper end to end? | |

<!-- Recorded in every module because M6 grades vibe coding empirically. Without this table
     the final module has nothing but opinion to work from. -->
