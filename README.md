# Vibe APOSD

**A Socratic course on software design for the age of AI-generated code.**

Textbook: *A Philosophy of Software Design*, 2nd edition, by John Ousterhout.
22 chapters, 7 modules, one case study per module built from live AI agent output.

---

## Why this course exists

Ousterhout's central claim is not about typing. It is this: the greatest limitation on
building software is **our ability to understand the systems we create**. Complexity is
defined structurally — anything about a system's shape that makes it hard to understand
and to modify.

Now look at what an AI coding agent changes, and what it leaves untouched:

| | Before agents | With agents |
|---|---|---|
| Cost of **producing** code | High | Near zero |
| Cost of **understanding** code | High | **Unchanged** |
| What limits complexity growth | Your typing speed, your patience | **Nothing** |

The friction that used to slow complexity down was never a design safeguard — it was an
accident. Remove it and complexity accumulates at the speed you can type prompts.

The book already gives us the precise vocabulary for this, in Chapter 3. Ousterhout
separates **tactical** programming (optimize for getting this working now) from
**strategic** programming (invest in a design that stays workable). His *tactical tornado*
is the developer who ships impressively fast and leaves a wake of wreckage for everyone
else to live in.

> An AI coding agent is a tactical programmer by construction. It optimizes for the prompt
> in front of it, it has no stake in next quarter's maintenance burden, and it never gets
> tired. If you do not supply the strategic intent, no one does.

So the human's job moves. Less producing code, more **specifying constraints and reviewing
structure**. APOSD is the vocabulary for both halves of that job. That is why this book,
and why now.

## Why Socratic, and not a checklist

There is a strong temptation to skip to the answer: extract Ousterhout's principles into a
bullet list, paste it into a system prompt, ship it. People try this. It does not work.

The list is not the skill. The skill is *recognizing* a shallow module, a leaked
abstraction, or an information-free comment when it is on your screen at 11pm and it
passes all the tests. Recognition does not transfer by assertion. It transfers by being
asked the right question at the moment you are about to be wrong.

So this course never opens with a conclusion. It opens with a scenario you already have
opinions about, keeps asking until your answer either breaks or holds for a reason you can
state out loud, and only then sends you to the text to find out whether Ousterhout agrees.

## The lesson loop

Every module runs the same six phases.

| Phase | What happens | Artifact produced |
|---|---|---|
| 1. **Intuition** | Teacher poses a concrete scenario. You answer from experience. No reading yet. | `socratic-log.md` |
| 2. **Probe** | Follow-ups until your intuition breaks, or holds for a stated reason. | `socratic-log.md` |
| 3. **Grounding** | You find the argument in the chapter and state the principle in your own words. | `socratic-log.md` |
| 4. **Generate** | You prompt an AI agent for a real task, deliberately **without** design constraints. Keep the raw output. | `case-study/*/before/` |
| 5. **Review & Refactor** | Apply the module's principle. Critique first, then rewrite. Record the delta. | `case-study/*/after/`, `findings.md` |
| 6. **Extract** | Distill what you had to tell the agent into a reusable constraint. | `prompts/` |

**The rule that makes phase 4 worth anything:** the agent must produce its *honest
default*. If you smuggle design guidance into the generation prompt, the case study stops
being evidence and becomes a demonstration. Generate carelessly on purpose. That is the
experiment.

Full mechanics, including the definition of done, are in [modules/README.md](modules/README.md).

## Curriculum

| Module | Chapters | Core question | The vibe coding failure it addresses |
|---|---|---|---|
| [M0 — Complexity](modules/m0-complexity/) | 1–3 | Where does complexity come from, and why isn't "it works" a finish line? | Generated code passes tests on day 1 and is unmodifiable by day 30 |
| [M1 — Deep Modules](modules/m1-deep-modules/) | 4–6 | What makes a module deep, and what belongs behind the interface? | Defining a module boundary *before* the agent writes anything |
| [M2 — Abstraction & Layers](modules/m2-abstraction-layers/) | 7–9 | Who absorbs the complexity, and should this be one thing or two? | Agents emit flat one-shot functions and pass-through methods |
| [M3 — Design Process](modules/m3-design-process/) | 10–11 | Can you delete a bug class by redefining the semantics? | Forcing design before code, in the prompt |
| [M4 — Comments & Naming](modules/m4-naming-comments/) | 12–15 | What must a comment carry that the code cannot? | Comments that restate the code line by line |
| [M5 — Consistency & Modification](modules/m5-consistency-maintenance/) | 16–18 | How do you change a system without degrading its design? | The riskiest agent operation: editing code it did not write |
| [M6 — Trends & Tradeoffs](modules/m6-trends-tradeoffs/) | 19–22 | Ousterhout grades agile, TDD, and design patterns. Now grade vibe coding. | Knowing when to let the agent run, and when to stop it |

Detailed chapter-by-chapter breakdown and the reasoning behind this grouping:
[CURRICULUM.md](CURRICULUM.md).

## Repository layout

```
.
├── README.md          You are here — thesis, method, curriculum
├── CLAUDE.md          Operating instructions for the AI agent acting as teacher
├── CURRICULUM.md      22 chapters mapped to 7 modules, with grouping rationale
├── modules/           One directory per module; identical interface, different content
│   └── mN-name/
│       ├── README.md       Chapters, core question, learning objectives, exercise brief
│       ├── socratic-log.md The dialogue, distilled into teaching material
│       └── case-study/     AI-generated code, the critique, and the refactor
│           ├── python/
│           └── typescript/
├── prompts/           Design-constraint prompt templates extracted from the modules
├── templates/         Blank forms for logs, case studies, and prompts
└── reference/          Chapter index into the textbook; the review checklist we build
```

Every module directory exposes the same three-part interface and hides its own mess
behind it. That is Chapters 4 and 5 applied to a filesystem — a course about information
hiding has no standing to be organized badly.

## How to use this repository

**To take the course yourself.** Clone it, open it in an agentic coding tool that reads
project instructions ([Claude Code](https://claude.com/claude-code), or any tool that
honors `CLAUDE.md` / `AGENTS.md`), and say *"start M0"*. The agent picks up the teacher
role, the hard rules, and the six-phase loop from [CLAUDE.md](CLAUDE.md). Work through
modules in order — later modules assume the vocabulary built in earlier ones.

**To read a completed run.** The `socratic-log.md` files *are* the course. Read them as
transcripts of reasoning, not as documentation. The case studies are the evidence that the
reasoning survived contact with real code.

**To harvest the useful bits.** `prompts/` and `reference/review-checklist.md` are the
portable output. They are deliberately written last, because a constraint you have not
personally watched fail is a superstition.

## Case study conventions

Each case study ships in both **Python** and **TypeScript**. The two languages are not
translations of each other — they are a controlled comparison. A dynamic language exposes
interface complexity nakedly, with no compiler to intercept it. A static language makes
some complexity visible in a signature and hides other complexity inside the type system.
Watching the same design failure land differently in each is part of the lesson.

## Textbook and attribution

*A Philosophy of Software Design*, 2nd edition — John Ousterhout, Yaknyam Press.

The community translation project publishes both languages side by side, so the course works
whichever you read in:

- **English:** <https://yingang.github.io/aposd2e-zh/en/>
- **中文:** <https://yingang.github.io/aposd2e-zh/>
- **All 22 chapters indexed, with each one's role in this course:**
  [reference/aposd-map.md](reference/aposd-map.md)

This repository **cites and argues with** the book. It does not reproduce it. There is no
substitute for reading the original, and the original is short. Buy it.

## Language policy

All committed material is in **English**, so it is useful to as many people as possible.
Lessons themselves can be conducted in any language — the log records the *reasoning*, not
the transcript. Technical terms stay in English everywhere.

## Progress

| Module | Socratic log | Case study | Prompts extracted |
|---|---|---|---|
| M0 — Complexity | Not started | Not started | — |
| M1 — Deep Modules | Not started | Not started | — |
| M2 — Abstraction & Layers | Not started | Not started | — |
| M3 — Design Process | Not started | Not started | — |
| M4 — Comments & Naming | Not started | Not started | — |
| M5 — Consistency & Modification | Not started | Not started | — |
| M6 — Trends & Tradeoffs | Not started | Not started | — |

## License

Course material in this repository: [MIT](LICENSE). The textbook is not ours and is not
included here.
