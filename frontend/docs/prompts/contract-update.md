# Prompt - apply an API contract change

The OpenAPI contract changed: <paste the handoff or describe the change>.

1. Regenerate the API client. Never edit generated code.
2. Let the compiler list every impacted call site; walk through them one by one.
3. Update view models and components only where the compiler or tests force it.
4. Run tests and lint, show the real output.
5. List any behavior question the contract does not answer - do not guess.
