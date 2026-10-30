<!-- jbeat-conventions:start -->
## Jbeat conventions

For implementation, debugging, code review, refactoring, software-change planning,
and project documentation, source comments, commits, or PRs, invoke the installed
`jbeat-conventions:jbeat-apply` skill using the Skill tool before task actions.
The user does not need to type a skill command for each request. This requirement
does not apply to unrelated conversation or imply authorization to commit or publish.

- Inspect applicable local instructions, reuse valid choices for the same topic
  and paths, and ask the user only when requirements cannot both be satisfied.
- Keep changes within the requested scope and preserve unaffected behavior.
- Respond in the user's language. Under the Jbeat choice, short Korean source
  comments use concise noun endings instead of `~입니다` or `~합니다`.
- Do not use middle dots as prose separators or unnecessary decorative dashes.
  Preserve required syntax, identifiers, quotations, and other documented exceptions.
- Before finishing, review the actual changed artifacts against applicable rules
  and choices, correct in-scope violations, and report only verification performed.

If the skill is unavailable, disclose the missing connection rather than claiming
the detailed conventions were loaded. Do not guess versioned plugin-cache paths.
<!-- jbeat-conventions:end -->
