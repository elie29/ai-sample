# Architecture rules

## Style

Hexagonal architecture (ports and adapters).

- `domain/` - business model and invariants. No framework dependency.
- `application/` - use cases / application services. Authorization decisions live here.
- `adapters/in/` - REST controllers and other inbound surfaces (e.g. MCP). Thin: no business logic.
- `adapters/out/` - persistence, external clients.

## Rules

- All inbound surfaces (REST, MCP, read-only mirror) call the same application services.
  A security decision is made once, at the service layer.
- Controllers map DTOs and delegate. Any `if` about business state in a controller is a smell.
- The domain never imports Spring, JPA or web classes.
- New architectural decisions are recorded in docs/decisions/ with the rejected alternatives.

## Verification

An architecture check must fail the build when a forbidden dependency direction is
introduced (e.g. ArchUnit tests). Run it as part of `./mvnw verify`.
