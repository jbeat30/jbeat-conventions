# jbeat-conventions

Jbeat 엔지니어링 컨벤션을 Claude Code 플러그인으로 패키징한 저장소입니다.
구현, 리뷰, 리팩토링, 디버깅, 플래닝 전반에 걸쳐 일관된 컨벤션을 적용합니다.

## 다루는 범위

- 변경 범위 제어 및 최소 안전 변경 원칙
- 기존 동작과 계약 보존
- 네이밍 및 주석 컨벤션
- 회귀 위험 인식
- 정직한 검증과 보고

## 설치

```
/plugin marketplace add jbeat30/jbeat-plugins
/plugin install jbeat-conventions@jbeat-plugins
```

마켓플레이스 `jbeat-plugins`는 [jbeat30/jbeat-plugins](https://github.com/jbeat30/jbeat-plugins)에서 관리

기존에 `jbeat30/jbeat-conventions`로 등록한 환경은 재등록 필요

```
/plugin marketplace remove jbeat-plugins
/plugin marketplace add jbeat30/jbeat-plugins
```

## 업데이트

```bash
claude plugins update jbeat-conventions@jbeat-plugins
```

## 명령어

```
/jbeat-setup   # 자동 모드 — 컨벤션 자동 활성화 on/off 토글
/jbeat-apply   # 수동 모드 — 모든 컨벤션을 명시적으로 즉시 적용
```

## 컨벤션 가이드

상세 내용은 [CONVENTIONS.md](CONVENTIONS.md)를 참고하세요.

| 파일 | 내용 |
|------|------|
| `references/core-rules.md` | 개발 철학, 변경 원칙, 에러 처리, 구조 |
| `references/naming-conventions.md` | 변수, 상수, 모듈 네이밍 규칙 |
| `references/comment-conventions.md` | 주석 작성 기준과 스타일 |
| `references/language-conventions.md` | 언어 정책 (기본 한국어) |
| `references/quality-checklist.md` | 작업 전 확인 사항과 최종 자가 점검 |
| `references/reporting-format.md` | 결과 보고서 및 검증 요약 형식 |
| `references/tooling-verification.md` | context7(최신 문서), chrome-devtools(화면 검증) 사용 규칙 |
| `references/commit-conventions.md` | 커밋·PR 제목 형식, 문자 규칙, 본문 구성, AI 첨부 문구 금지 |

## 선택 사항: MCP 도구

`tooling-verification.md`는 아래 MCP가 설치된 경우에만 적용되며, 이 플러그인은 MCP를 설치하거나 설정하지 않습니다.
도구가 없으면 공식 문서 등으로 대체하고, 확인하지 못한 항목은 미검증으로 보고합니다.

```bash
claude mcp add context7 -- npx -y @upstash/context7-mcp
claude mcp add chrome-devtools -- npx -y chrome-devtools-mcp@latest
```

- context7은 외부 서비스이므로 쿼리에 시크릿이나 내부 코드를 넣지 않습니다.
- chrome-devtools는 localhost, 개발·스테이징 환경에서만 사용하며 개인 로그인 프로필은 사용하지 않습니다.

## 버전·브랜치 관리

- 버전은 [Semantic Versioning](https://semver.org/lang/ko/)을 따르며 태그는 `vX.Y.Z` 입니다. 릴리즈는 [Releases](https://github.com/jbeat30/jbeat-conventions/releases)에서 확인합니다.
- `main` 에는 `release/vX.Y.Z`, `hotfix/vX.Y.Z` 만 PR 할 수 있고, 작업은 `feature/vX.Y.Z` 로 PR 합니다.
- 상세 흐름(작업·릴리즈·핫픽스·백머지)은 [.github/BRANCH_STRATEGY.md](.github/BRANCH_STRATEGY.md)를 참고하세요.
