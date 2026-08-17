# Design-constraint prompts

Prompt templates extracted from the modules. Each one exists because a specific design
failure was observed in a specific case study, and each one names the failure it prevents.

**Nothing goes in here that was not derived from a `findings.md`.** This directory is output,
not input. Writing a plausible-sounding constraint before watching the corresponding failure
is exactly the shortcut this course is built to avoid.

---

## Three places a constraint can intervene

| Phase | Tag | What it does | Relative cost |
|---|---|---|---|
| Before generation | `before-generation` | Specifies the boundary, interface, or design process before any code exists | Cheapest |
| During review | `during-review` | Audits generated code against one named principle | Moderate |
| Before modification | `before-modification` | Constrains an edit to an existing system so the design does not degrade | Highest stakes |

**Prefer the earliest intervention that works.** A review prompt that reliably catches a
shallow module is useful; a generation prompt that prevents it is strictly better, because the
review still has to be read, judged, and acted on by a human. Chapter 11 is the argument in
miniature — designing twice costs one extra generation, which is nearly free, while
un-designing something afterward costs a refactor.

`before-modification` is tagged separately from `before-generation` because Chapter 16 is a
different problem. Generating into an empty directory has no design to preserve. Editing a
live system does, and the constraint has to name what must not change.

## What not to build

**Do not write the mega-prompt.** The tempting move is to compress all 22 chapters into one
system prompt and never think again. It fails, for a reason worth stating precisely:
constraints compete for attention, and a prompt that asks for everything is a prompt that
prioritizes nothing. It also produces a specific and recognizable failure — over-abstraction
on tasks that never needed it, because the agent is now optimizing for a rubric instead of a
problem.

One constraint, chosen for the task in front of you, tied to a principle you can name.

**Do not accept a prompt you have not watched fail.** Both `Observed effect` and
`Known failure modes` are required sections in the template, and an empty one is a bug. A
prompt with no known failure mode has not been used enough to be published — set its status
to `untested` and say so in the file.

## Conventions

- Filename: `m<N>-<slug>.md` — the module number records where the evidence came from
- Front matter: `id`, `principle`, `chapter`, `phase`, `status`
- `status`: `untested` → `tested-once` → `in-regular-use` → `retired`
- Retired prompts stay in the repository with a note explaining what replaced them. A
  constraint that stopped working is more instructive than one that always did.
- Template: [`../templates/prompt-template.md`](../templates/prompt-template.md)

## Index

| Prompt | Module | Principle | Chapter | Phase | Status |
|---|---|---|---|---|---|
| _none yet_ | | | | | |

<!-- Add a row when a prompt lands. Sort by module, then by phase. -->
