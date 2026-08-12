# API contract rules (OpenAPI)

- `openapi.yaml` is the source of truth for the API.
- The backend generates interfaces and DTOs from it. Generated code is NEVER manually edited.
- The frontend consumes the same contract.
- An API change starts by changing the contract, then regenerating, then letting the
  compiler show the impact ("change the contract and see what breaks").
- Shared constraints (e.g. a year/period range) live in ONE shared schema used by
  all routes - never duplicated per route.
- Breaking changes require a decision record in docs/decisions/.
