---
name: security-review
description: Design-time security review of a frontend feature specification, before any implementation.
---

# security-review - frontend design-time security review

Run this on a specification BEFORE implementation, not on the code after.

Read the specification I point you to (docs/superpowers/specs/...). Then:

1. **Attack the trust model.** What does this screen assume the backend has already
   verified? The UI must never be the only enforcement of a rule.
2. **Attack the rendering.** Which user-provided or API-provided values reach the
   DOM? Where could unsafe HTML, links or file names be rendered?
3. **Attack the storage.** What ends up in browser storage, URLs or query params?
   Tokens and sensitive identifiers must not.
4. **Attack the session.** What happens on token expiry mid-action? On a permission
   revoked while the screen is open? On a hidden resource still selected?
5. **Attack the errors.** What do error messages reveal about data the user should
   not see?

Output format:
- A numbered list of findings, most severe first.
- For each finding: the scenario, the impact, and the missing acceptance criterion.
- End with the security questions the specification does not answer.

Do NOT propose implementation. If you find nothing, say what you tried and where
the specification was too vague to attack.
