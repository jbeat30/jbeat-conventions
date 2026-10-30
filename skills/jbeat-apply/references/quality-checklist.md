# Quality Checklist

Use relevant questions for implementation, debugging, refactoring, and code review.
Plans and document-only work do not require code checks unless their outcome depends
on them. This operationalizes [core-rules.md](core-rules.md), without universal steps.

## Before changing code

- What outcome is requested, and what surrounding behavior must remain stable?
- Which local rules apply? Are actual conflicts unresolved under
  [project-rule-resolution.md](project-rule-resolution.md)?
- Which normal/failure paths, callers, trust boundaries, or order-sensitive behavior
  could the change affect?
- Does uncertain third-party usage need
  [tooling-verification.md](tooling-verification.md)?
- Which existing checks can establish the intended result?

## Review the change

- Is each changed area necessary to complete the task?
- Are guards, failure handling, types, and meaningful ordering preserved or changed
  intentionally with a clear reason?
- If logic was shared or removed, do callers actually have the same contract?
- Do changed user messages describe the actual failure without internal diagnostics?
  Do changed comments explain useful intent?
- Does the change respect supported languages and tools without imposing frontend rules?

## Verify proportionally

- Run relevant available checks: focused tests, static/type analysis, lint, build,
  or runtime reproduction. Select by behavior and repository requirements rather
  than a fixed list for every language.
- For behavior fixes, exercise relevant normal and failure cases when feasible.
  Prefer existing checks; add tests when they meaningfully protect behavior rather
  than mirror implementation or prose.
- Distinguish pre-existing failures from new failures using evidence. Do not label
  failures pre-existing without a basis.
- Stop expanding successful verification unless edits, failures, or remaining risk
  justify it. Report evidence through [reporting-format.md](reporting-format.md).
