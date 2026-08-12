---
name: security-audit
description: Audit-and-fix loop for backend security. Audit broadly, fix narrowly, re-audit.
---

# Security audit skill

Perform this loop. Never skip the re-audit.

1. **Audit** (broad): authentication and token handling, authorization on every
   inbound surface (REST, MCP, mirrors), SQL injection, input validation against the
   contract, CORS, sensitive data in responses and logs, secrets, dependencies, migrations.
2. **Prioritize**: list findings by severity with the concrete scenario.
3. **Ask**: present findings to the human. The human decides what is fixed now,
   later, or accepted as a risk. Record the decision in docs/decisions/.
4. **Fix** (narrow): one finding, one file when possible, with a test proving the fix.
5. **Re-audit**: verify the fix and check for regressions.

A fix that has not been verified is not a fix. It is a claim.
