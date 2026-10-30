# Branch strategy and release guide

[한국어](BRANCH_STRATEGY.md) | [English](BRANCH_STRATEGY.en.md)

This guide describes branch strategy, PR rules, and release management for the
personal `jbeat-conventions` repository. It does not set rules for users' projects.

## 1. Overview

Normal changes follow this sequence:

```text
work branch → feature/vX.Y.Z → release/vX.Y.Z → main
```

Squash work branches into feature branches. Use merge commits for subsequent
stages. Urgent fixes use `hotfix/vX.Y.Z` created from `main`, with a PR directly
back to `main`. Automated backmerge PRs bring released changes into active higher
version feature and release branches.

## 2. Branch types

| Branch | Example or format | Purpose | Created from |
|---|---|---|---|
| `main` | Fixed name | Released code | Not applicable |
| `release/vX.Y.Z` | `release/v1.3.0` | Release preparation | `main` |
| `feature/vX.Y.Z` | `feature/v1.3.0` | Integration for a version | `main` |
| Work branch | `feat/`, `fix/`, `refactor/`, `chore/`, `docs/`, `test/`, `style/`, `perf/`, `ci/`, `build/` | Individual change | `feature/vX.Y.Z` |
| `hotfix/vX.Y.Z` | `hotfix/v1.2.1` | Urgent fix | `main` |

Versions use `v` followed by three numeric components, such as `v1.3.0`, and follow
[Semantic Versioning](https://semver.org/).

- MAJOR: changes that break existing usage, such as convention structure or skill names.
- MINOR: compatible additions to rules or skills.
- PATCH: typo and wording changes or compatible bug fixes.

Release tags use the same format, such as `v1.3.0`.

## 3. PR rules

| Direction | Merge method |
|---|---|
| Work branch → `feature/vX.Y.Z` | Squash |
| `feature/vX.Y.Z` → matching `release/vX.Y.Z` | Merge commit |
| `release/vX.Y.Z` → `main` | Merge commit |
| `hotfix/vX.Y.Z` → `main` | Merge commit |
| `main` → `feature/*` or `release/*` for backmerge | Merge commit; no squash |

No review approvals are required for this personal repository. Rules still apply
without owner bypass. Every PR must pass `branch-policy / check`, which checks
branch direction, PR and commit title format, AI attribution text, and matching
`plugin.json` versions for release or hotfix PRs into `main`.

Changes to `main`, `release/*`, and `feature/*` require PRs. Force pushes and
deletion are prohibited. Direct pushes to `hotfix/*` are allowed, but force pushes
are not. Merged work branches are deleted automatically.

## 4. Workflow

### 4.1 Start a new version

```bash
git fetch origin
git switch -c feature/v1.3.0 origin/main
git push -u origin feature/v1.3.0
```

### 4.2 Normal work

```bash
git switch -c feat/login-page feature/v1.3.0
# Make changes and commit.
git push -u origin feat/login-page
```

Open `feat/login-page` → `feature/v1.3.0` and use **Squash and merge**.

### 4.3 Release

1. Through a work-branch PR into `feature/v1.3.0`, set `.claude-plugin/plugin.json` version to `1.3.0`.
2. Create the release branch:

   ```bash
   git fetch origin
   git switch -c release/v1.3.0 origin/main
   git push -u origin release/v1.3.0
   ```

3. Open `feature/v1.3.0` → `release/v1.3.0` and use **Create a merge commit**.
4. Open `release/v1.3.0` → `main` and use **Create a merge commit**.
5. After the merge, `publish-release` creates the `v1.3.0` tag and GitHub release with generated notes.
6. Update an installation using `claude plugin update jbeat-conventions@jbeat-plugins`.

### 4.4 Hotfix

```bash
git fetch origin
git switch -c hotfix/v1.2.1 origin/main
# Apply the fix, set plugin.json version to 1.2.1, and commit.
git push -u origin hotfix/v1.2.1
```

1. Open `hotfix/v1.2.1` → `main` and use **Create a merge commit**.
2. `publish-release` creates the tag and release.
3. Backmerge PRs from `main` into active higher version `feature/v*` and `release/v*` branches open automatically. Merge them using **Create a merge commit**.

## 5. Backmerge

Bring fixes already released on `main` into ongoing feature and release branches.
Otherwise later releases can reintroduce fixed bugs or encounter conflicts.

Merge automatic PRs with merge commits, not squash. If a PR conflicts, resolve it
locally:

```bash
git fetch origin
git switch -c chore/back-merge-v1.2.1 origin/feature/v1.3.0
git merge origin/main
# Resolve conflicts and commit.
git push -u origin chore/back-merge-v1.2.1
```

Close the automatic PR and open `chore/back-merge-v1.2.1` → `feature/v1.3.0`.
Use **Create a merge commit**.

## 6. Rulesets

Ruleset sources are in [`rulesets/`](rulesets). To create rulesets:

```bash
for f in .github/rulesets/*.json; do
  gh api -X POST repos/jbeat30/jbeat-conventions/rulesets --input "$f"
done
```

For existing rulesets, obtain IDs with
`gh api repos/jbeat30/jbeat-conventions/rulesets` and update using
`-X PUT .../rulesets/<id>`.

| Rule | Target | Requirements |
|---|---|---|
| `main` | Default branch | PR, merge commits only, required `branch-policy / check`, no force pushes or deletion |
| `release` | `release/v*` | PR, merge commits only, required `branch-policy / check`, no force pushes or deletion |
| `feature` | `feature/v*` | PR, squash or merge, required `branch-policy / check`, no force pushes or deletion |
| `hotfix` | `hotfix/v*` | No force pushes; direct pushes allowed |

## 7. Commit and PR conventions

```text
type(scope): Korean description
```

Examples: `feat: 툴링 검증 컨벤션 추가`, `fix(naming): 예시 오타 수정`,
`release: v1.3.0`.

Allowed types: `feat`, `fix`, `refactor`, `perf`, `style`, `docs`, `test`, `chore`,
`ci`, `build`, `revert`, `release`. Descriptions use concise Korean noun endings
such as `추가`, `구현`, or `수정`, with no final period. PR titles use the same
format. Work PR titles become commit messages through squash merging.

This is a contribution requirement for this repository, not a requirement imposed
by the installed skill on English projects.

Use the [PR template](pull_request_template.md) sections: `## 개요` (overview),
`## 변경 사항` (changes), `## 검증` (verification), and `## 참고` (notes).
Do not include AI attribution text such as `Co-Authored-By: Claude …` or
`Generated with …` in commits or PRs.

[README](../README.en.md) | [Convention guide](../CONVENTIONS.en.md)
