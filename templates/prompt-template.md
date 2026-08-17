---
id: m_N_-_slug_
principle: _the design principle this enforces_
chapter: _n_
phase: before-generation | during-review | before-modification
status: untested
---

# _Prompt name_

## Intent

<!-- What design failure this exists to prevent. One or two sentences. -->

## When to use

## When NOT to use

<!-- Required. A constraint applied everywhere is a convention, and conventions belong in
     CLAUDE.md rather than in a prompt template. If this applies to every task, it is in the
     wrong file. -->

---

## The prompt

```text

```

---

## Why it works

<!-- Tie this to the chapter's actual argument, not to prompt folklore. "LLMs respond well to
     structure" is folklore. "It forces the interface to be named before the implementation
     exists, so the implementation cannot leak into it (Ch 5)" is an argument. -->

## Observed effect

**Required — do not leave empty.**

| | |
|---|---|
| Tried on | _task_ |
| Model / tool | |
| Date | |

<!-- What actually changed in the output. "It seemed better" is not an observation. Name a
     structural difference: fewer parameters, the cache stopped leaking upward, the error
     branch disappeared. -->

## Known failure modes

**Required — do not leave empty.**

<!-- Every constraint has a cost or a way to be over-applied. Common ones worth checking for:
     over-abstraction on a task that did not need it; the agent optimizing for the letter of
     the constraint; a much longer generation for no structural gain. If you cannot name a
     single failure mode, you have not used this enough to publish it — set status to
     `untested` and say so. -->

-

---

## Provenance

Extracted from `modules/m_N_-_slug_/case-study/findings.md`, section _"What the agent would
have needed to know up front"_.
