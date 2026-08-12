# Prompt - first screen from a specification

Read docs/superpowers/specs/NNN-<feature-name>.md (and the backend handoff if any).

Create the first version of the screen:

- respect .claude/rules/design-ux.md and .claude/rules/accessibility.md;
- include loading, empty and error states - the screen is not finished without them;
- consume the generated API client only (never hand-written calls);
- run tests and lint, show the real output.

Then stop. I will look at the running application - the first render is the first
design review, and we iterate from there.
