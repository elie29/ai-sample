# Frontend architecture rules

- Standalone components; smart/dumb separation: pages orchestrate, components present.
- One feature = one folder: components, services, models, tests together.
- State: keep it local when possible; a shared store only for genuinely shared state
  (current user, selected period). Document any new store slice in a decision record.
- No business rules in the frontend. The backend decides; the frontend displays.
  Duplicated validation is allowed only for UX, and the contract stays authoritative.
- Routing guards handle access, but the UI never relies on them alone -
  the backend enforces authorization.
