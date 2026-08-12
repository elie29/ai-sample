# Testing rules

- Aim for test code >= production code on business-critical modules.
- Every bug fix starts with a failing test reproducing the bug.
- Test names describe behavior: `shouldRejectHiddenPeriodForUnauthorizedUser`.
- Integration tests cover: RBAC per role, migrations (on PostgreSQL AND H2),
  contract conformance, and every inbound surface (REST and MCP alike).
- Generated tests are reviewed one file at a time. A broad "generate tests for
  everything" request is forbidden - audit can be broad, writing stays narrow.
- The expected result of a verification command is written BEFORE running it.
