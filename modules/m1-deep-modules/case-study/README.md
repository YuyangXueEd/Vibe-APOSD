# M1 Case Study — Rate limiting on an HTTP client

| | |
|---|---|
| **Principle under test** | module depth and information hiding (Ch 4, Ch 5) |
| **Status** | Not started |
| **Languages** | Python, TypeScript |

---

## The brief

### Task given to the agent — verbatim

<!-- Copy exactly what was sent, including any sloppiness. This is the experimental
     condition; paraphrasing it invalidates the study. -->

```text

```

### What was deliberately withheld

<!-- The design constraints NOT stated. This is the independent variable, and it is the
     single most important field in this file. -->

-

### Generation conditions

| | |
|---|---|
| Model | |
| Tool / harness | |
| Context the agent had | |
| Project instructions in effect | |
| Date | |

<!-- "Project instructions in effect" matters: if CLAUDE.md was loaded, the agent was NOT
     running its honest default and the baseline is contaminated. Say so here. -->

---

## Layout

| Path | Contents |
|---|---|
| `python/before/` | Raw agent output, unmodified. **Immutable once committed.** |
| `python/after/` | Refactor after applying the principle. |
| `typescript/before/` | Raw agent output, unmodified. **Immutable once committed.** |
| `typescript/after/` | Refactor after applying the principle. |
| `findings.md` | The critique, the before/after delta, and what it cost. |

## Running it

```bash
# python
cd python/before && python -m main

# typescript
cd typescript/before && npm install && npm start
```

<!-- Replace with whatever is actually true. If before/ does not run, say why — a baseline
     that does not run is itself a finding. -->

---

## Ground rules

1. **`before/` is evidence, not code.** Never fix it. Bugs in it are results.
2. **`after/` preserves observable behaviour.** If behaviour had to change to fix the
   design, that is a separate finding — write it down rather than quietly allowing it.
3. **The two languages are a comparison, not a translation.** Each is written idiomatically
   for its language, so that the same design failure can express itself differently.
4. **Critique before refactor.** Findings are agreed on before any code is touched.
