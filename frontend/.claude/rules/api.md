# API consumption rules

- The API client is generated from the shared OpenAPI contract. Generated code is
  NEVER manually edited.
- On contract change: regenerate, then let the compiler show every impacted call site.
- Error handling is centralized (interceptor): authentication expiry, permission
  errors and validation errors each have ONE consistent UX.
- Do not shape backend data in components; map DTOs to view models in one place per feature.
