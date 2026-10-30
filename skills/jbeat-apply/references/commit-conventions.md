# Commit and PR Conventions

Apply when writing commit or PR text. Follow
[language-conventions.md](language-conventions.md) for language and
[writing-conventions.md](writing-conventions.md) for punctuation. Resolve actual
conflicts with contribution rules or templates through
[project-rule-resolution.md](project-rule-resolution.md).

## Titles

- Default format: `type: description`, optionally with a meaningful scope such as
  `fix(parser): handle empty input`.
- Types: `feat`, `fix`, `refactor`, `perf`, `style`, `docs`, `test`, `chore`, `ci`,
  `build`, `revert`, `release`.
- Describe purpose and result. Korean descriptions use concise noun endings such
  as `추가`, `수정`, `정리`, `제거`. Other languages use natural conventions.
- Omit a final period in titles. Do not impose Korean on other-language work.

## Bodies and units

- Explain the problem, resulting behavior, and relevant verification. Use the
  repository template when compatible; otherwise a useful default is overview,
  changes, verification, and notes, in the artifact's language.
- Keep sections short and omit empty optional sections. Evidence reporting follows
  [reporting-format.md](reporting-format.md).
- Group commits by meaningful changes. Separate unrelated formatting from behavior;
  do not split inseparable documentation from its behavior mechanically.
- Do not add AI-generated signatures such as `Generated with` phrases or AI
  `Co-Authored-By` trailers. Resolve conflicts if repository rules require attribution.

Writing a message does not authorize creating a commit, publishing a PR, or pushing.
