# Behavior validation scenarios

[한국어](behavior-validation.md) | [English](behavior-validation.en.md)

These maintenance scenarios distinguish static review from actual agent execution
after documentation changes. This is not a rule file read on every skill use.
Expected outcomes below are not passing test records. For actual runs, record the
request, relevant instructions, tools and versions, result, and unverified scope.
Use isolated temporary projects. Do not change user settings or live services.

## Rule selection

| Project conditions and request | Behavior to observe |
|---|---|
| No project rules; small bug fix | Apply relevant shared rules without unnecessary choice questions |
| Project rules cover deployment only; documentation task | Do not ask about unrelated rules or deploy |
| Both sources prohibit unrelated refactoring | Apply the common requirement without duplicate questions |
| Project requires policy rationale comments | Satisfy together with shared comment guidance |
| Project requires English comments; Korean request adds comments | Explain conflict sources and differences; wait for a choice before changes |
| User chooses project rules in that conflict | English comments, Korean explanation, no repeated question on the same topic |
| A new directory introduces another conflict | Ask only about the new topic; retain existing choices |
| Conversation language changes after a comment-language choice | Respond in the new request language; retain the valid comment-language choice |
| A choice covers one path; work moves elsewhere | Compare the new path's rules without extending the prior choice arbitrarily |
| User does not answer a conflict question | Hold dependent changes; independent investigation can continue |
| Choosing Jbeat conflicts with an existing linter | Explain configuration effects and required scope; do not disable the linter |

## Language, writing, and environments

| Request | Behavior to observe |
|---|---|
| English request | English progress and final responses |
| Korean request to edit an English README | Korean explanation; preserve English in the document |
| Write documentation, comments, reviews, commits, and PRs | No middle-dot separators or unnecessary dashes |
| Include Markdown lists, `--help`, URLs, negative numbers, and quotations | Preserve necessary syntax and original text |
| Modify a Python function | Do not require JS syntax, JSDoc, console, or browser inspection |
| Modify a simple, obvious JS/TS function | Do not add meaningless documentation blocks |
| Similar classification code at different trust boundaries | Do not merge solely because names look similar |
| Project uses i18n and a dedicated logger | Do not require a single error-constants file or introduce console logging |
| Context7 unavailable; official documentation available | Use alternative evidence; tool absence alone is not a verification gap |
| Tests fail to run or no execution environment exists | Distinguish failures and gaps; do not weaken checks or claim a pass |

## Initial setup and project connection

| Environment and request | Behavior to observe |
|---|---|
| Existing `CLAUDE.md` and other user instructions | Preserve language and instructions; add one connection block |
| Only `AGENTS.md` exists | Confirm host loading; do not arbitrarily create a competing file |
| Both instruction files exist | Check actual loading and scope; avoid duplicate connections |
| No instruction file exists | Ask whether to create `CLAUDE.md` or `AGENTS.md` |
| Repeat setup with an equivalent connection | No duplication or unnecessary edits |
| User customized the managed block | Preserve surrounding content; ask if overwriting is needed |
| Duplicate or damaged markers | Do not guess boundaries and overwrite or delete content |
| `setup status` with no file | Report no connection without creating a file |
| `setup remove` | Remove only the managed block; preserve the file and remaining content |
| File access fails | Report the error rather than assuming absence |
| Legacy `on/off` arguments | Explain changed command meaning without editing settings |
| Setup after global installation | Target only the current project; do not change home instructions or settings |
| Apply skill unavailable | Explain installation/loading before a new connection; existing inspection and removal remain possible |
| Normal request in a fresh session after connection | Check instruction loading and actual skill use |
| Fresh session after connection removal | Distinguish removal of the persistent connection from skill availability |
| Explicit apply invocation or `all` | Resolve the current installation; do not execute conditional rules unconditionally |

## Before completion

New comments are in scope even if the implementation request did not explicitly
ask for comments. Under selected Jbeat rules, concise Korean comments use noun
endings, while English and exact quotations follow their language and preservation
rules. Inspect shell edits as well as changes made through editing tools. Do not
blindly replace punctuation or add unnecessary comments just to satisfy a rule.

## Verification levels

1. Static review: check reference links, applicability conditions, meaning across documents, manifests, and skill format.
2. Isolated execution: use fresh sessions and temporary projects to inspect files before and after setup, tool calls, and results.
3. Actual project checks: verify against the user's host version, instruction loading, and relevant tools.

Static review alone does not establish automatic activation, connection file
changes, or passing all behavior scenarios. This repository is prompt-based and
provides no separate runtime code or hook tests.

## Current verification scope

The October 30, 2026 transition to a prompt-based structure was reviewed statically
through source and documentation. Previous hook script tests cover a removed
implementation and are not evidence for the current approach. Actual model
execution, setup file changes and repeated runs, and skill use in fresh sessions
remain unverified.

Before release, at least check instruction preservation, duplicate prevention on
repeat runs, conflict choices, and normal requests in fresh sessions in an isolated
environment. An earlier model execution attempt received no response because of
account usage limits. The structural transition does not claim passing model runs.

Historical static results for that transition: 16 Markdown files and 63 local
links had no missing targets. Skill headers, connection template markers, JSON,
and whitespace were checked. Manifest validation passed, with warnings about
ignored existing interface fields and missing optional icons. These counts describe
that review, not the expanded documentation set in later versions.

[Convention guide](../CONVENTIONS.en.md) | [README](../README.en.md)
