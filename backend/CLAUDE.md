# Backend - CLAUDE.md

REST API backend (Java / Spring Boot, hexagonal architecture). This file is the
entry point the AI reads every session. It stays **concise**: details live in
focused rule files loaded on demand.

## What this project is

A sample enterprise API managing business assets, with role-based access control,
audited data changes and a generated API layer. Replace this paragraph with a short,
precise description of YOUR system and its purpose.

## Non-negotiable rules

- The OpenAPI contract is the source of truth for the API. Generated code is never manually edited.
- Authorization is enforced at the service layer, never only in controllers.
- Every task ends with a verification command. Never claim "it should work" - run it.
- Never commit. The human commits.
- One task, one scope. Ask before widening a change.

## Plan State Continuity

Work in progress is tracked in `docs/superpowers/plans/`. **The plan file, not the chat, is the
source of truth.** The conversation may be cleared at any moment — not only at the end of a step —
and anything that exists only in the chat is lost when it is.

### Required plan header

Every plan in `docs/superpowers/plans/` opens with this block, above the goal:

```text
> **Status:** in progress | blocked | done
> **Resume at:** Task {n} — {what to actually do next, one line}
> **Last updated:** {YYYY-MM-DD} · {commit sha, or `uncommitted`}
```

`Resume at` is authoritative and is **not** "the first unchecked box" — it is where work actually
restarts, which may be mid-task, a rework of an already-checked box, or a verification step.

### At the end of every turn

Write the plan file **first, before replying**, then reply. The reply is an echo of what was written, nothing more: no state that appears in the chat may be absent from the plan.

1. **Check off what is done** — `- [x] Task 3 — 2026-08-11 · c370994`, with the date and the
   commit sha, or `uncommitted` when the change is still in the working tree.
2. **Update `Resume at`** to the real next step, and refresh `Last updated`.
3. **Append every decision made in conversation** to a `## Decisions` section — one line each,
   with date and reason. A decision that lives only in the chat did not happen.
4. **Record any pending blocker** in a `## Blockers` section — what is blocked, what unblocks it,
   who owns it. Delete the entry when it clears.

Never end a turn that changed state — code, decision, or blocker — without this write.

### On resume

1. Read the plan in `docs/superpowers/plans/` whose `Status:` is `in progress`.
2. Announce the step named in `Resume at` **before** writing anything.
3. Start there — not at the first unchecked box.
4. Ask which plan to pick up **only** when the in-progress plan is `done` and other plans are
   waiting. Otherwise resume the in-progress one without asking.

`superpowers:writing-plans` generates the plan body; this header and these two sections are added
on top of whatever it produces.

## Detailed rules (load only when relevant)

| Topic | File |
| --- | --- |
| Architecture and layers | .claude/rules/architecture.md |
| Security | .claude/rules/security.md |
| Testing | .claude/rules/testing.md |
| Database and migrations | .claude/rules/database.md |
| API contract (OpenAPI) | .claude/rules/api-contract.md |
| Naming conventions | .claude/rules/naming.md |

## Workflow

business need -> specification (docs/superpowers/specs/) -> invariants -> the security-review skill ->
adjust specification -> execution plan (docs/superpowers/plans/) -> implement small task ->
verify -> human review -> human commit.

Specs and plans are written by the superpowers plugin skills (brainstorming, then
writing-plans) and validated by the human at each step - see docs/superpowers/README.md.

The state of the work lives in those files, not in the conversation: status, current task,
open questions and blockers are updated in the file as they change, so a session with no
chat history can resume the work.
A decision that lives only in the chat did not happen: record it in docs/decisions/.
Reusable prompts live in docs/prompts/ - use them instead of improvising.

## Commands

- Build: `./mvnw clean verify`
- Unit tests: `./mvnw test`
- Single test class: `./mvnw test -Dtest=ClassName`
- Verification of a task: defined in the task's plan file BEFORE execution.
