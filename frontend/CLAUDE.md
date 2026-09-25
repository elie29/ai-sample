# Frontend - CLAUDE.md

Angular single-page application. This file is the entry point the AI reads every session. 

It stays **concise**: details live in focused rule files loaded on demand.

## What this project is

The user interface of a sample enterprise asset platform. Replace this paragraph with a short, precise description of YOUR application and its users.

## Plan State Continuity

Work in progress is tracked in `docs/superpowers/plans/`.
**The plan file, not the chat, is the source of truth.** The conversation may be cleared at any moment — not only at the end of a step — and anything that exists only in the chat is lost when it is.

### Required plan header

Every plan in `docs/superpowers/plans/` opens with this block, above the goal:

```text
> **Status:** in progress | blocked | done
> **Resume at:** Task {n} — {what to actually do next, one line}
> **Last updated:** {YYYY-MM-DD} · {commit sha, or `uncommitted`}
```

`Resume at` is authoritative and is **not** "the first unchecked box" — it is where work actually restarts, which may be mid-task, a rework of an already-checked box, or a verification step.

### Required task index

Right after the header, before the goal, every plan carries a `## Tasks` section: one checkbox per task, in order, `- [ ] Task {n} — {title}`. It is the at-a-glance progress view; the detailed steps stay in each task's own section. A task is checked here only when all of its steps are.

### Before handing control back — every turn, not just at the end of a step

Write the plan file **first**, then reply. The reply is an echo of what was written, nothing more: no state that appears in the chat may be absent from the plan.

1. **Check off what is done** — `- [x] Task 3 — 2026-08-11 · c370994`, with the date and the commit sha, or `uncommitted` when the change is still in the working tree — in the task's own steps and in the `## Tasks` index.
2. **Update `Resume at`** to the real next step, and refresh `Last updated`.
3. **Append every decision made in conversation** to a `## Decisions` section — one line each, with date and reason. A decision that lives only in the chat did not happen.
4. **Record any pending blocker** in a `## Blockers` section — what is blocked, what unblocks it, who owns it. Delete the entry when it clears.

Never end a turn that changed state — code, decision, or blocker — without this write.

### Closing a plan

When the last task is checked, set `Status:` to `done` in the same write. That task's line and `Last updated` carry the date alone — `- [x] Task 12 — 2026-08-11` — since the closing commit cannot name itself and a `done` plan is never resumed; `git log -1 -- <plan>` finds it. `Resume at` reads `— (nothing; every task is checked)`.

### On resume

1. Read the plan in `docs/superpowers/plans/` whose `Status:` is `in progress`.
2. **Reconcile every `uncommitted` marker.** The owner commits between turns, so each one is presumed stale: find the commit that carries the task's change (`git log -- <the files the task names>`) and write its sha in the task's steps, in the `## Tasks` index and in `Last updated`. Done when no `uncommitted` remains except on a change `git status` still shows.
3. Announce the step named in `Resume at` **before** writing anything.
4. Start there — not at the first unchecked box.
5. Ask which plan to pick up **only** when the in-progress plan is `done` and other plans are waiting. Otherwise resume the in-progress one without asking.

`superpowers:writing-plans` generates the plan body; this header, the task index and these two sections are added on top of whatever it produces.

## Change request

Before making any changes:

* Respect all project rules, conventions, and available skills.
* Use the **Superpowers** plugin and respect the process (brainstorm, design, plan, tdd, review, etc..).
* **Do not invent** requirements, behaviors, APIs, data models, or implementation details. If anything is unclear or missing, stop and ask me specific questions before proceeding.
* If additional context or files are required, tell me exactly what you need.

## Code design

Code you write or change respects the **SOLID** principles (single responsibility, open/closed, Liskov substitution, interface segregation, dependency inversion) and uses established **Design Patterns** (GoF and idiomatic equivalents) where they fit the problem. Pick a pattern because the code needs it now, and name it in the design or review when you apply one. When the existing code departs from these principles, point it out and ask before refactoring beyond the change's scope.

## Non-negotiable rules

- The OpenAPI contract is the source of truth for API consumption. Generated client code is never manually edited.
- The design system rules apply to every screen. No ad-hoc styling.
- Accessibility is part of every feature, not a final phase.
- Every task ends with a verification command (tests, lint, build). Never claim "it should work" - run it.
- Never commit. The human commits.
- One task, one component when possible. Ask before widening a change.

## Detailed rules (load only when relevant)

| Topic | File |
| --- | --- |
| Architecture and state | .claude/rules/architecture.md |
| API consumption | .claude/rules/api.md |
| Design system and UX | .claude/rules/design-ux.md |
| Accessibility | .claude/rules/accessibility.md |
| Testing | .claude/rules/testing.md |
| Naming conventions | .claude/rules/naming.md |

## Workflow

business idea -> specification (docs/superpowers/specs/) -> the security-review skill -> first screen -> look at the running application -> accessibility review -> adjust -> repeat.

The running application is the maquette. The browser is the feedback loop.

Specs and plans are written by the superpowers plugin skills and validated by the human before the next step - see docs/superpowers/README.md.

The state of the work lives in those files, not in the conversation.

Reusable prompts live in docs/prompts/ - use them instead of improvising.

## Commands

- Install: `npm ci`
- Dev server: `npm start`
- Tests: `npm test`
- Lint: `npm run lint`
- Production build: `npm run build`
