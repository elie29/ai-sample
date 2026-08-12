# Frontend testing rules

- Every component with logic has a spec file. Presentation-only components need at
  least a render test.
- Test behavior, not implementation: interact via the DOM as a user would.
- Generated tests are reviewed one file at a time - never accept a bulk test dump.
- Contract-dependent code is tested against the generated client types, so a
  contract change breaks tests visibly.
- The expected result of a verification command is written BEFORE running it.
