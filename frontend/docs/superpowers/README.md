# Specs and plans

The files in `specs/` and `plans/` are not hand-written prose and not chat exports.
They are produced by the **superpowers plugin skills**, and each one is **validated by
the human** before the next step starts. The AI writes the file; the human approves it.

## Who produces what, and who validates it

| Step | Skill | Output | Human gate |
| --- | --- | --- | --- |
| Design | `superpowers:brainstorming` | `specs/NNN-feature-name.md` | approves the design, then reviews the written spec |
| Planning | `superpowers:writing-plans` | `plans/NNN-feature-name.md` | reviews the tasks and their verification commands |
| Execution | `superpowers:executing-plans` or `superpowers:subagent-driven-development` | ticks tasks in the plan file | looks at the running application, then commits |

Between design and planning, run an adversarial design review on the spec (the
`security-review` skill in `.claude/skills/`). Its output goes back into the spec file,
not into the chat. Accessibility is reviewed inside the loop, on the running screen
(the `accessibility-audit` skill), not as a final phase.

The plugin's default file names are date-based (`YYYY-MM-DD-<topic>-design.md`,
`YYYY-MM-DD-<feature-name>.md`). This project overrides that with `NNN-feature-name.md`,
a user preference the skills accept. One number per feature, shared by its spec, its plan
and its decision records - and shared with the backend when the feature spans both.

## The state lives in these files, not in the conversation

The conversation is disposable. A context window gets compacted, truncated, restarted or
simply lost, and it is never reviewable by a colleague. The files are the memory.

- Status, current task, open questions, blockers, decisions taken during execution:
  written in the file, updated the moment they change.
- Anything the human validated: written in the file before implementation continues.
- A fresh session with zero chat history must be able to resume the work by reading
  `specs/` and `plans/` alone. If it cannot, the file is incomplete.

A decision, a constraint or an approval that exists only in the chat did not happen.

## Rules

- The specification is the source of truth. If the code must change, change the spec
  first, then let the AI realign the code.
- A screen without its loading, empty and error states is not specified.
- The running application is the maquette: a task is not done until it has been looked
  at in the browser.
- The plan file, not the chat, holds progress. Tick a task only after its verification
  command has actually been run.
- Important decisions are copied to `docs/decisions/` with their rejected alternatives.
