# Core Rules

## Scope and intent

- Solve the requested problem with a small, traceable, sufficient change. Fewest
  changed lines is not the goal if the fix remains incomplete.
- Preserve behavior, contracts, data flow, and user experience outside the
  requested change. A requested behavior change is allowed; identify its impact.
- Keep unrelated renaming, file movement, dependency replacement, configuration
  changes, and cleanup outside the task.
- Inspect existing patterns and applicable rules. Resolve actual conflicts through
  [project-rule-resolution.md](project-rule-resolution.md).
- State consequential assumptions. Proceed with reasonable implementation choices;
  ask when missing information materially changes the required result.
- Activation does not authorize rewriting project rules, changing permissions,
  committing, pushing, merging, releasing, or deploying. Follow the user's actual
  authorization, including authorization already given.

## Structure and abstraction

- Favor readable, traceable code with visible inputs, outputs, and side effects.
- Keep responsibilities clear without fragmenting straightforward logic.
- Abstract when repeated policy and maintenance cost justify it. Similar syntax
  alone is insufficient. Compare inputs, outputs, failure meaning, trust boundaries,
  and callers before sharing or removing implementations.
- Preserve meaningful execution and initialization order. Review dependency
  direction and hidden coupling before moving code or changing module boundaries.
- Share classification policy for the same responsibility and contract. Different
  runtimes or trust boundaries may need separate adapters and independent
  validation. Do not require exactly one function per concept.
- Remove dead code only when actual usage and data flow establish unreachability
  and removal belongs to this change. Do not add guards for confirmed impossible states.

## Failures and diagnostics

- Preserve useful guards, fallback behavior, and failure information unless the
  change justifies altering them. Handle relevant external input and failures
  without speculative defensive scaffolding.
- Never hide errors or weaken types, lint, tests, or build checks merely to appear
  successful. Do not silence type errors with unjustified assertions or unsafe types.
- Keep diagnostic context useful without exposing secrets, credentials, or customer
  data in code, logs, reports, or external queries.
- When user-facing messages exist, describe the actual failed operation and a useful
  next step. Keep internal diagnostics out of the user interface.
- Reuse existing localization or message management. Group messages by meaning where
  useful; do not force every domain into one constants file.
- Use the project's logger and severity policy. In JS without one, console methods
  are possible examples, not mandatory tools.
- HTML messages apply only to existing HTML rendering surfaces. Do not introduce
  HTML insertion to format errors. Preserve escaping and sanitization; prefer
  normal framework text and layout mechanisms.

## Evidence

Distinguish facts, assumptions, and unverified conclusions. Verification depends
on affected behavior and available project tools. Execution and reporting criteria
live in [quality-checklist.md](quality-checklist.md) and
[reporting-format.md](reporting-format.md).
