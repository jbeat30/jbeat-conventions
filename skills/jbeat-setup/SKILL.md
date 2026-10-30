---
name: jbeat-setup
description: >-
  Connect the installed Jbeat conventions to this project's CLAUDE.md or AGENTS.md
  so normal engineering requests use the apply skill. Run once per project, or
  use status/remove to inspect or remove only the managed connection block.
  Does not toggle plugin activation or edit global settings.
disable-model-invocation: true
argument-hint: "[status|remove]"
user-invocable: true
---

# Connect Jbeat Conventions

This is a prompt-driven setup skill. It has no bundled executable or hook.
Invoking setup authorizes a narrow project-instruction connection, not replacement
of local policies, global settings, plugin installation, or repository-wide cleanup.

## Inspect before editing

1. Respond in the user's language. Read the installed apply skill at
   `../jbeat-apply/SKILL.md` and its language, writing, and project-rule-resolution
   references, resolving paths from this skill's directory. Read
   [project-instructions.md](references/project-instructions.md) as the connection template.
2. Identify the current project root from the working context and repository.
   Ask if ambiguous. Inspect supplied ancestor instructions and existing project
   `CLAUDE.md`, `.claude/CLAUDE.md`, `CLAUDE.local.md`, `AGENTS.md`, and
   `.claude/AGENTS.md` where relevant. Do not inspect unrelated projects or home
   settings. Check only current-scope guidance needed for choosing a loaded file.
3. For a new or updated connection, verify that the installed
   `jbeat-conventions:jbeat-apply` skill is available.
   Source code in an arbitrary checkout is not proof of installation. If unavailable,
   explain installation/reload steps and do not write a nonworking connection.
4. Prefer an existing project CLAUDE.md that the host loads. If there is only an
   AGENTS.md, use it when the host/version/settings load it. Do not assume both
   filenames always load. If loading is uncertain or multiple destinations have
   different scopes, explain and ask which loaded file to use. Do not create a
   competing instruction file that hides an existing one.
5. For a connection request, if neither file exists, ask whether to create
   CLAUDE.md or AGENTS.md, explaining
   Claude Code compatibility. For older or uncertain Claude Code environments,
   recommend CLAUDE.md. Respect a destination the user already specified.
   Global installation does not authorize editing global instructions; this setup
   defaults to the current project only.

For status/remove with no existing target, report that no connection exists;
do not ask which file to create. Determine the requested action before inspecting
destinations so read-only or removal requests never enter the creation flow.

## Select the action

- No argument: add or update the connection in the selected instruction file.
- `status`: inspect only. Report target, block presence, apply-skill availability,
  and any uncertainty about instruction loading. Create or change nothing.
- `remove`: remove only an intact Jbeat-managed block, preserving everything else.
  If no block exists, report that fact without creating a file or deleting one.
- Legacy `on`/`off`: explain that setup now connects project instructions, not
  plugin activation. Direct activation management to `/plugin`. Do not silently
  reinterpret these arguments or change any files. Ask which new action is wanted.
- Unknown or contradictory actions: clarify before any write.

For status/remove, missing apply-skill availability is a reportable condition,
not a reason to prevent inspection or removal of an old connection.

## Preview and apply narrowly

Use the template's exact start/end markers to identify ownership. Preserve its
installed skill identifier and meaning; adapt prose to the instruction file's
language. Reuse the existing document language rather than translating its other
sections. Compare applicable local requirements before introducing any conflicting
Jbeat summary, and resolve actual conflicts with the user first. Adapt selected
summary rules to valid user choices rather than reintroducing an overridden rule.
When resolving a setup conflict, include the selected topic, source, and path
scope in the previewed managed block so the agreed connection is understandable
in future sessions. Persist only choices authorized for this connection; do not
silently turn a prior session-only choice into a permanent project policy.

Show the target path and the proposed managed-block change before writing. A
clear setup request already authorizes this narrow addition/update; do not ask
for redundant approval once destination and any actual conflicts are resolved.
Do not interpret an existing marker block as proof that its current text is safe
to overwrite: preserve user customizations, and ask if replacing them is needed.

- Append one block when absent. On repeat runs, update the existing block in place
  only if necessary. If already equivalent, leave the file unchanged.
- If markers are duplicated, unbalanced, or ambiguously nested, explain the issue
  and ask before editing. Never remove arbitrary text based on a guessed boundary.
- Preserve all other instructions, file language, encoding, and line endings.
  Do not replace the entire file, create duplicate sections, edit plugin caches,
  or change enabledPlugins, marketplaces, permissions, hooks, or global settings.
- Treat read/access failures as errors, not missing files. Re-read before writing
  if concurrent changes are possible, and preserve them.
- After writing, re-read to verify a single intact block (or its absence on remove)
  and preservation of surrounding content. Do not delete the file when removing
  its block, even if the block was its only content.

## Report

Report the changed path, action, and verified outcome in the user's language.
After connecting, explain that future normal work requests are instructed to use
Jbeat without a per-task command; a fresh session should load the connection.
Distinguish verified file content from actual host loading and model compliance.
Do not claim every task is guaranteed to obey the conventions.

Removing the block stops this persistent connection, not plugin availability or
all possible automatic skill selection. The apply skill can still be selected or
invoked while the plugin is enabled. Already-loaded instructions remain in the
current context; use a fresh session after removal. Changes to repository
instruction files may be shared with collaborators if committed; do not commit
or push unless the user requested it.
