# AI-Assisted Engineering Template

This repository contains no business logic. It is the **skeleton** you can copy into
your own backend and frontend repositories to work with an AI assistant (Claude Code
or similar) in a disciplined way.

## The article series behind this template

This project is the companion of my two-part series
**"AI Writes the Code. So What Is the Engineer's Job Now?"**, based on a real
two-month enterprise project built with this exact structure:

- [Part 1 - The story](https://medium.com/@elie29/ai-writes-the-code-so-what-is-the-engineers-job-now-79fa3fdf1b88): one developer, two repositories, and the
  bugs an adversarial AI review found before a single line of code.
- Part 2 - The method (coming soon): the living specification - why the code
  is no longer the source of truth, and what that changes for every role in the SDLC.

The articles explain the *why* behind every folder in this repository.

## The core ideas

1. **The specification is the source of truth.** The invariants are the contract.
   The code is an implementation of that contract.
2. **`CLAUDE.md` stays concise.** It describes the project, states the
   non-negotiable rules, and points to focused rule files. The AI loads a detailed
   rule file only when it works on that topic.
3. **Rules describe the project. Skills and agents perform actions.** Do not mix them.
   Place each skill at the right level: a skill specific to the project lives in the
   repository (`.claude/skills/`); a skill that is repeatable across projects (like an
   adversarial design review) lives at the account level (`~/.claude/skills/`), so you
   do not duplicate it in every repository.
4. **Every non-trivial feature gets a specification (design) and an execution plan**
   (docs/superpowers/). Both are written by the **superpowers plugin skills** and
   **validated by the human** before the next step. The state of the work lives in those
   files, not in the conversation: a session can be stopped, cleared or restarted at any
   moment without losing anything. A decision that lives only in the chat did not happen.
5. **Prompts are project assets.** Reusable prompts live in docs/prompts/, are
   versioned with the code and improved after every use.
6. **Verification is part of development.** Every task has a verification command,
   and the expected result is written before the command is executed.

## Structure

```text
ai-sample/
├── README.md                         <- you are here
├── backend/
│   ├── CLAUDE.md                     <- concise entry point, read by the AI every session
│   ├── .claude/
│   │   ├── rules/                    <- architecture, security, testing, database, api-contract, naming
│   │   └── skills/                   <- security-review (design-time), security-audit (audit-and-fix)
│   └── docs/
│       ├── superpowers/
│       │   ├── README.md             <- how specs and plans are produced and validated
│       │   ├── specs/                <- one specification per feature (NNN-feature-name.md)
│       │   └── plans/                <- one execution plan per feature (NNN-feature-name.md)
│       ├── prompts/                  <- create-spec, implement-task, migration-review, handoff
│       └── decisions/                <- decision-template.md + one record per decision
└── frontend/
    ├── CLAUDE.md
    ├── .claude/
    │   ├── rules/                    <- architecture, design-ux, accessibility, api, testing, naming
    │   └── skills/                   <- security-review, accessibility-audit
    └── docs/
        ├── superpowers/
        │   ├── README.md             <- the same loop, adapted to the UI feedback cycle
        │   ├── specs/                <- one specification per feature (NNN-feature-name.md)
        │   └── plans/                <- one execution plan per feature (NNN-feature-name.md)
        ├── prompts/                  <- new-screen, contract-update, implement-task, accessibility-review
        └── decisions/                <- same template as the backend
```

Every `superpowers/`, `specs/`, `plans/` and `prompts/` folder carries its own `README.md`
stating the naming convention and which skill produces the files it contains. The two
sides mirror each other, so `backend/` and `frontend/` can be copied independently into
separate repositories.

## How to use it

1. Copy the structure into your repositories.
2. Rewrite every rule file for **your** project. A generic rule produces generic code.
3. Before implementing any feature: write the specification, define the invariants,
   then run an adversarial design review against it - for example the `security-review`
   skill included here, or the [grill-me](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md) skill created by Matt Pocock.
4. Drive implementation with the reusable prompts in docs/prompts/, one task at a time.
5. Keep tasks small: one task, one file when possible, one verification, then review.
6. Keep the human responsible for commits.

## License

MIT - use it freely.
