# Prompt - review a migration before it exists

The specification NNN requires a data migration: <describe what moves or changes>.

Before writing it, answer:

1. Which queries actually consume this data? List the real joins.
2. Which related tables must move together so those joins stay complete?
3. What happens to existing rows, defaults and orphans?
4. Are audit triggers involved? Should they stay enabled? Why?
5. Does the deployment model justify expand/contract, or is a direct migration right?

Then propose the migration for BOTH PostgreSQL and H2, with its verification test.
