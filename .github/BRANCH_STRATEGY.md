# 브랜치 전략 & 릴리즈 가이드

[한국어](BRANCH_STRATEGY.md) | [English](BRANCH_STRATEGY.en.md)

jbeat-conventions 개인 레포의 브랜치 전략, PR 규칙, 버전과 릴리즈 관리 방법입니다.

## 1. 한눈에 보기

```
main ◀── release/v1.3.0 ◀── feature/v1.3.0 ◀── feat/login-page
  │          (Merge)            (Merge)      ◀── fix/login-api   (Squash)
  │
  └──▶ hotfix/v1.2.1 ──▶ main   (main 에서 바로 따서 바로 PR)
                          │
                          └──▶ 백머지 PR (main → 진행 중인 feature/release, 자동 생성)
```

## 2. 브랜치 종류

| 브랜치 | 형식 | 역할 | 어디서 만드나 |
|---|---|---|---|
| `main` | 고정 | 배포된 코드 | - |
| `release/vX.Y.Z` | `release/v1.3.0` | 배포 준비 브랜치 | `main` |
| `feature/vX.Y.Z` | `feature/v1.3.0` | 해당 버전의 개발 통합 브랜치 | `main` |
| 작업 브랜치 | `feat/…`, `fix/…`, `refactor/…`, `chore/…`, `docs/…`, `test/…`, `style/…`, `perf/…`, `ci/…`, `build/…` | 실제 작업 단위 | `feature/vX.Y.Z` |
| `hotfix/vX.Y.Z` | `hotfix/v1.2.1` | 긴급 수정 | `main` |

- 버전은 항상 `v` + 숫자 3자리(`v1.3.0`) 형식이며 [Semantic Versioning](https://semver.org/lang/ko/)을 따릅니다.
  - MAJOR: 기존 사용 방식을 깨는 변경 (예: 컨벤션 파일 구조와 스킬 이름 변경)
  - MINOR: 하위 호환되는 규칙과 스킬 추가
  - PATCH: 오타와 문구 수정, 하위 호환 버그 수정
- 배포 태그도 `v1.3.0` 입니다.

## 3. PR 규칙

| PR 방향 | 머지 방식 |
|---|---|
| 작업 브랜치 → `feature/vX.Y.Z` | **Squash** |
| `feature/vX.Y.Z` → `release/vX.Y.Z` (같은 버전) | **Merge commit** |
| `release/vX.Y.Z` → `main` | **Merge commit** |
| `hotfix/vX.Y.Z` → `main` | **Merge commit** |
| `main` → `feature/*`, `release/*` (백머지) | **Merge commit** (Squash 금지) |

- 개인 레포라 리뷰 승인은 요구하지 않습니다(승인 0명). 대신 Owner 우회 없이 모든 규칙을 똑같이 적용합니다.
- 모든 PR은 필수 검사 `branch-policy / check` 를 통과해야 합니다.
  - PR 방향, PR과 커밋 제목 형식, AI 첨부 문구, `release`/`hotfix` → `main` 시 `plugin.json` 버전 일치를 검사합니다.
- `main`, `release/*`, `feature/*` 는 PR로만 변경하고 force push와 삭제를 금지합니다. `hotfix/*` 는 직접 push 가능하며 force push 만 금지합니다.
- 머지된 작업 브랜치는 자동 삭제됩니다.

## 4. 작업 흐름

### 4-1. 새 버전 개발 시작

```bash
git fetch origin
git switch -c feature/v1.3.0 origin/main
git push -u origin feature/v1.3.0
```

### 4-2. 일반 작업

```bash
git switch -c feat/login-page feature/v1.3.0
# 작업 & 커밋
git push -u origin feat/login-page
```
→ PR: `feat/login-page` → `feature/v1.3.0`, **Squash and merge**

### 4-3. 릴리즈

1. `feature/v1.3.0` 에서 `.claude-plugin/plugin.json` 의 `version` 을 `1.3.0` 으로 올립니다. (작업 브랜치 → feature PR)
2. `release/v1.3.0` 브랜치를 만듭니다.
   ```bash
   git fetch origin
   git switch -c release/v1.3.0 origin/main
   git push -u origin release/v1.3.0
   ```
3. PR: `feature/v1.3.0` → `release/v1.3.0`, **Create a merge commit**
4. PR: `release/v1.3.0` → `main`, **Create a merge commit**
5. `main` 머지 즉시 `publish-release` 워크플로가 `v1.3.0` 태그와 GitHub 릴리즈(자동 생성 노트)를 만듭니다.
6. 설치한 환경에서는 `claude plugin update jbeat-conventions@jbeat-plugins` 로 업데이트합니다.

### 4-4. 핫픽스

```bash
git fetch origin
git switch -c hotfix/v1.2.1 origin/main
# 수정 & plugin.json version 을 1.2.1 로 변경 & 커밋
git push -u origin hotfix/v1.2.1
```
1. PR: `hotfix/v1.2.1` → `main`, **Create a merge commit**
2. `publish-release` 가 `v1.2.1` 태그와 릴리즈를 자동 생성합니다.
3. **백머지**: 머지 즉시 개발 중인 더 높은 버전의 `feature/v*`, `release/v*` 로 가는 `main → …` PR 이 자동으로 열립니다. **Create a merge commit** 으로 머지하세요.

## 5. 백머지

`main` 에 먼저 들어간 수정(핫픽스)을 진행 중인 `feature/*`, `release/*` 에 반영하는 것입니다. 안 하면 다음 릴리즈에서 고친 버그가 되살아나거나 충돌이 납니다.

- 자동 PR 은 **Merge commit** 으로 머지합니다. (Squash 하면 나중에 충돌)
- 자동 PR 에 충돌이 있으면 로컬에서 해결합니다.
  ```bash
  git fetch origin
  git switch -c chore/back-merge-v1.2.1 origin/feature/v1.3.0
  git merge origin/main      # 충돌 해결 후 commit
  git push -u origin chore/back-merge-v1.2.1
  ```
  자동 PR 은 닫고 `chore/back-merge-v1.2.1` → `feature/v1.3.0` 을 **Merge commit** 으로 머지합니다.

## 6. 룰셋 적용

룰셋 원본은 [`rulesets/`](rulesets) 에 있습니다. 새로 적용하거나 갱신할 때:

```bash
for f in .github/rulesets/*.json; do
  gh api -X POST repos/jbeat30/jbeat-conventions/rulesets --input "$f"
done
```
이미 있는 룰셋은 `gh api repos/jbeat30/jbeat-conventions/rulesets` 로 id 를 확인하고 `-X PUT .../rulesets/<id>` 로 갱신합니다.

| 룰 이름 | 대상 | 내용 |
|---|---|---|
| `main` | 기본 브랜치 | PR 필수, Merge commit 만, `branch-policy / check` 필수, force push와 삭제 금지 |
| `release` | `release/v*` | PR 필수, Merge commit 만, `branch-policy / check` 필수, force push와 삭제 금지 |
| `feature` | `feature/v*` | PR 필수, Squash와 Merge 허용, `branch-policy / check` 필수, force push와 삭제 금지 |
| `hotfix` | `hotfix/v*` | force push 금지 (직접 push 는 허용) |

## 7. 커밋과 PR 컨벤션

```
<타입>(<범위>): <한국어 설명>
```

- 예: `feat: 툴링 검증 컨벤션 추가`, `fix(naming): 예시 오타 수정`, `release: v1.3.0`
- 타입: `feat` `fix` `refactor` `perf` `style` `docs` `test` `chore` `ci` `build` `revert` `release`
- 설명은 한국어, 명사형 종결(`추가`, `구현`, `수정`), 마침표 없음
- PR 제목도 같은 형식입니다. 작업 → feature 는 Squash 라 PR 제목이 그대로 커밋 메시지가 됩니다.
- PR 본문: `## 개요` / `## 변경 사항` / `## 검증` / `## 참고`
- **AI 첨부 문구 금지**: `Co-Authored-By: Claude …`, `Generated with …` 등을 커밋과 PR 에 넣지 않습니다.
