# Security rules

- Every endpoint requires an explicit authorization rule at the service layer.
  When a new route family is added, verify it applies the SAME visibility rules as
  existing families (this exact gap was found in production - see the article).
- Input validation at the boundary: all path/query/body values validated against the
  OpenAPI contract. Shared constraints live in ONE shared schema, not repeated per route.
- No secrets in the repository. Configuration through environment variables.
- SQL only through parameterized queries / repositories. String concatenation into a query is forbidden.
- Audit log: data-changing operations must remain attributable. Bulk technical
  migrations must not pollute the audit trail (suppress triggers deliberately and document it).
- Dependencies: known-CVE checking is part of the pipeline, not an AI guess.

## Checklist for the security-review skill on any new feature

- Which roles can reach the new endpoints?
- Do sibling route families enforce the same rules?
- What happens with a stale or revoked permission mid-session?
- What data does an error response leak?
