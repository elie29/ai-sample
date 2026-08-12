# Specifications

One file per feature: `NNN-feature-name.md`. One number per feature, shared by its
specification, its plan and its decision records.

These files are created by the `superpowers:brainstorming` skill and validated by the
human before any plan is written - see docs/superpowers/README.md for the full loop.
The skill produces the structure; there is no template file to copy. A specification is
not ready for review until it states explicitly:

- the business need, in business vocabulary;
- the affected domains, routes and data;
- the invariants, numbered - the contract the code must satisfy;
- what is out of scope.

The specification is the source of truth, and it holds the state of the feature:
status, open questions and decisions live here, not in the conversation.

Run the security-review skill on the invariants before any implementation.
