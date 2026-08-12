---
name: security-review
description: Design-time security review. Attack a specification and its invariants from a security perspective, before any implementation.
---

# security-review - design-time security review

Run this on a specification BEFORE implementation, not on the code after.

Read the specification and invariants I point you to (docs/superpowers/specs/...). Then:

1. **Attack the access rules.** Which role can now see or do something it could not
   before? Which existing rule could this feature accidentally bypass?
2. **Attack the siblings.** If a visibility or authorization rule is enforced on one
   route family, list every other family and surface (REST, MCP, mirrors) that must
   enforce the same rule, and check whether the specification says so.
3. **Attack the data.** What sensitive data can appear in responses, errors, logs or
   exports? What does the migration expose or leave behind?
4. **Attack the session.** What happens to a user mid-session when a permission is
   revoked or a resource becomes hidden? What was selected before, is it still valid?
5. **Attack the inputs.** Which values cross a trust boundary, and which shared
   schema validates them? Point out any constraint duplicated per route.

Output format:
- A numbered list of findings, most severe first.
- For each finding: the scenario, the impact, and the invariant that is missing or ambiguous.
- End with the security questions the specification does not answer.

Do NOT propose implementation. Do NOT compliment the design. If you find nothing,
say what you tried and where the specification was too vague to attack.
