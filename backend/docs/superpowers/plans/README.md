# Plans

One execution plan per feature: `NNN-feature-name.md`, same number as its specification.

Created by the `superpowers:writing-plans` skill from the validated specification and
reviewed by the human before execution - see docs/superpowers/README.md. The skill
produces the structure; there is no template file to copy. Every task in the plan states:

- its scope - the files it is allowed to touch;
- its verification command;
- the expected result of that command, written BEFORE it is run.

The plan file, not the chat, is the source of truth: progress, decisions and blockers are
written here as they happen, so a session with no chat history can resume the work.
Tick a task only after its verification command has actually been run.
