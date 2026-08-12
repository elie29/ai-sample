# Database and migration rules

- Every migration is written for BOTH PostgreSQL and H2, and tested on both.
- A migration that copies year-scoped or hierarchical data must copy ALL tables of
  the relationship, not just the first one (verify against the actual queries that
  join them - the half-fix looks finished).
- Migrations on audited tables: decide explicitly whether audit triggers stay
  enabled. Document the decision in docs/decisions/.
- Rollback strategy documented per migration. Expand/contract only when the
  deployment model actually requires it (single-artefact deployments usually do not).
- Schema changes start in the specification, never directly in a migration file.
