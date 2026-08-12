# Reusable prompts

A good prompt is a project asset, like a script. These prompts are versioned with
the code, improved after every use, and written against the project's rules and
templates - not generic. Copy, fill the <placeholders>, paste.

## Prompts vs. Skills

**Reusable Prompt** (`.prompt.md`): A saved, parameterized instruction you invoke manually to perform a specific task — like a macro or template. It runs once and produces output (e.g., "generate a spec", "review this PR").

**Skill** (`SKILL.md`): A packaged block of domain knowledge that the *agent* reads to guide its behavior during a task. It's not invoked directly by the user — the agent loads it automatically when the task falls within its domain, then uses those instructions to act more accurately.

In short: a prompt is something **you** trigger; a skill is something the **agent** consults.
