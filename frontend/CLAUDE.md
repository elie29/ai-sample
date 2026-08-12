# Frontend - CLAUDE.md

Angular single-page application. This file is the entry point the AI reads every
session. It stays **concise**: details live in focused rule files loaded on demand.

## What this project is

The user interface of a sample enterprise asset platform. Replace this paragraph
with a short, precise description of YOUR application and its users.

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

business idea -> specification (docs/superpowers/specs/) -> the security-review skill -> first screen ->
look at the running application -> accessibility review -> adjust -> repeat.

The running application is the maquette. The browser is the feedback loop.

Specs and plans are written by the superpowers plugin skills and validated by the human
before the next step - see docs/superpowers/README.md. The state of the work lives
in those files, not in the conversation.
Reusable prompts live in docs/prompts/ - use them instead of improvising.

## Commands

- Install: `npm ci`
- Dev server: `npm start`
- Tests: `npm test`
- Lint: `npm run lint`
- Production build: `npm run build`
