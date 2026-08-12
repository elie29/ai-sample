# Prompt - write a cross-repository handoff

The backend part of feature NNN is implemented. Write a handoff document for the
frontend repository: docs/superpowers/specs/NNN-<feature-name>-handoff.md

Include:

- what changed in the OpenAPI contract (endpoints, schemas, constraints);
- the invariants the frontend must respect (visibility rules, roles);
- what the backend does NOT validate (UX-only validation the frontend may add);
- verification: how the frontend can prove the integration works.

Write it for an AI session that has never seen this conversation.
