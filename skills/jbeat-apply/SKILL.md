---
name: jbeat-apply
description: >-
  Apply Jbeat engineering conventions when implementing, debugging, reviewing,
  refactoring, planning software changes, or writing project documentation,
  code comments, commits, and PRs. Control scope, preserve unaffected behavior,
  verify third-party usage, and report evidence honestly across languages and
  frameworks. Compare project rules and ask only when requirements conflict.
  Also use for explicit convention requests. Not for unrelated conversation
  or changing plugin settings.
argument-hint: "[all]"
user-invocable: true
---

# Jbeat Conventions

## Apply to the current task

1. Identify the requested outcome, affected paths, language, and runtime. Read
   [core-rules.md](references/core-rules.md),
   [language-conventions.md](references/language-conventions.md), and
   [writing-conventions.md](references/writing-conventions.md).
2. Read the task-specific references below and always read
   [project-rule-resolution.md](references/project-rule-resolution.md).
   Inspect applicable project rules before applying conventions, even when no
   conflict is apparent yet. Reuse valid prior choices for the same topic and
   scope first, then compare remaining requirements. Ask only about unresolved
   conflicts: requirements that cannot both be satisfied. Identical, unrelated,
   and compatible rules need no question.
3. Apply only relevant rules. JS/TS documentation, browser inspection, UI messages,
   and console logging are conditional examples, not universal requirements.
4. Perform the requested work and proportional verification. Before finishing,
   inspect the actual changed code, comments, and prose against the applicable
   conventions and valid user choices; fix established in-scope violations.
   Include shell edits, not just changes made with file-edit tools. Reading rules
   is not evidence that the resulting artifacts comply. Report outcomes and material limits
   using [reporting-format.md](references/reporting-format.md).

## Task-specific references

| Task | Read before applying |
|---|---|
| Code creation, renaming, refactoring | [naming-conventions.md](references/naming-conventions.md) |
| Source comments or API documentation comments, including comments added incidentally during implementation | [comment-conventions.md](references/comment-conventions.md) |
| Implementation, debugging, refactoring, code review | [quality-checklist.md](references/quality-checklist.md) |
| Third-party behavior, uncertain APIs, runtime/UI inspection | [tooling-verification.md](references/tooling-verification.md) |
| Commit messages or PR text | [commit-conventions.md](references/commit-conventions.md) |

For an explicit `all` request, read all references, keeping their applicability
conditions. Loading browser rules does not make browser inspection necessary.
When entering a new task area, read its references and recheck relevant project
rules. Do not scan unrelated areas merely to find conflicts.

## Resources and communication

Resolve references relative to this skill's directory (`${CLAUDE_SKILL_DIR}`).
For a plugin installation, that directory is also
`${CLAUDE_PLUGIN_ROOT}/skills/jbeat-apply`. Never select the first matching cached
installation. If resources cannot be resolved, disclose what was not loaded.

When invoked explicitly without a work request, briefly state references read
and unresolved conflicts in the user's language. During automatic use, proceed
without repetitive activation announcements. Loading rules does not prove future
compliance or authorize unrelated actions.
