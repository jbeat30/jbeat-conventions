# Commit and PR Conventions

Use Korean by default. Applies to commit messages, PR titles, and PR bodies.

## Title

- Format: `type: Korean noun-ending description`, for example `feat: 로그인 화면 추가`.
- Types: `feat`, `fix`, `refactor`, `perf`, `style`, `docs`, `test`, `chore`, `ci`, `build`, `revert`, `release`.
- End with a noun form (`추가`, `수정`, `정리`, `제거`). Avoid sentence endings such as `~합니다`, `~했습니다`.
- Do not end the title with a period.
- Describe the purpose and result of the change, not the files touched.

## Characters

- Do not use the middle dot (`·`) or dashes (`-`, `–`, `—`) as separators in titles or body text.
- Use commas, `와/과`, or a numbered list instead.
- Hyphens inside identifiers, paths, branch names, and command flags are kept as written.

## Body

- PR body order: 개요, 변경 사항, 검증, 참고.
- Keep each part short. Use a numbered list for multiple items.
- Verification states what was actually run and its result. Write items that were not run as unverified.

## AI Attribution

- Do not add AI generated phrases or signatures to commits and PRs, such as `Generated with ...` or a `Co-Authored-By` trailer naming an AI tool.
- This applies to every commit type, including `chore` and `docs`.
- A repository may allow an exception in its own contribution guide. That exception is the repository's policy, not part of these conventions.

## Commit Units

- One commit per meaningful unit of change. Do not squash unrelated changes into one commit.
- Do not mix formatting-only changes with behavior changes.
