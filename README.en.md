# jbeat-conventions

[한국어](README.md) | [English](README.en.md)

**A collection of engineering convention skills for Claude Code that helps AI stay within the requested scope, preserve existing behavior, and report only what it has verified.**

Install the plugin and connect it once in each project. Then request work as usual, without entering an apply command for every task.

Use it when a small bug fix turns into unrelated restructuring, or when an assistant reports passing tests it never ran. The conventions started with frontend work, but separate shared principles from conditional guidance so they can be used across languages and frameworks.

[Quick start](#quick-start) | [Usage](#usage) | [Convention guide](#convention-guide) | [Contributing](#contributing)

## What does it help with?

- Focus on the requested problem and avoid unrelated renaming, file moves, or dependency replacements.
- Preserve unaffected behavior and contracts, considering relevant success and failure paths.
- Show the sources and differences when project rules actually conflict, and ask the user to choose.
- Explain intent and constraints in code comments, and keep prose consistent.
- Respond in the user's language and preserve existing document languages unless translation is requested.
- Review changed artifacts against applicable rules before finishing, distinguishing actual verification from material gaps.

The rules and procedures are Markdown prompts. There are no bundled runtime scripts, hooks, or Node.js dependencies. They do not replace linters or tests, or guarantee complete model compliance.

## Quick start

The project connection workflow below applies to **2.0.0 and later**. Check [Releases](https://github.com/jbeat30/jbeat-conventions/releases) for published versions.

### 1. Install

In a Claude Code conversation, register the marketplace and install the plugin:

```text
/plugin marketplace add jbeat30/jbeat-plugins
/plugin install jbeat-conventions@jbeat-plugins
```

Choose user scope for personal use across projects, project scope to share with repository collaborators, or local scope for personal use in the current project. Reload or restart as instructed after installation.

### 2. Connect your project

Run once in each project:

```text
/jbeat-conventions:jbeat-setup
```

Setup adds a short Jbeat connection block to an existing `CLAUDE.md` or an `AGENTS.md` that the host loads. If neither exists, it asks which file to create. Existing content is preserved, and actual conflicts with project rules are resolved through user choices.

Installation scope and project connection are separate. Even with a user-wide installation, connect each project individually. Setup does not change global settings or plugin activation. It shows the proposed path and content, and does not duplicate the block when run again.

| State | Usage |
|---|---|
| Plugin installed | Skills can be selected by relevance or invoked explicitly |
| Plugin installed and project connected | Project instructions direct relevant work to the apply skill; request work normally |

For ongoing use, complete the project connection. Preview the [connection block template](skills/jbeat-setup/references/project-instructions.md) before setup.

### 3. Request work normally

Start a fresh conversation after connecting, then make a normal request:

```text
Fix the login error and check the relevant failure paths.
```

```text
Review this patch.
```

Project instructions direct relevant work to the installed apply skill. You do not need to enter `/jbeat-conventions:jbeat-apply` every time. MCP tools are optional.

## Usage

### Scope and language support

The skill reads relevant references for implementation, debugging, review, refactoring, planning, project documentation, comments, commits, and PRs. It does not impose development procedures on unrelated conversation or require browser inspection and JS/TS documentation practices in other environments.

English requests receive English progress messages, questions, and final reports. An explicit response-language request takes precedence. Existing documents and surrounding comments retain their language unless translation is requested. For new artifacts without an established language, Jbeat proposes the user's language and compares explicit project requirements before adopting it. Actual conflicts require a user choice.

Korean noun endings apply to concise Korean comments and labels, not English prose. English comments and commit descriptions follow natural English conventions. Language selection does not authorize renaming identifiers, files, commands, or external contract fields. See the [language policy](skills/jbeat-apply/references/language-conventions.md).

### Expected behavior

These are intended behaviors guided by the conventions. Assess actual results using the changed artifacts and verification evidence.

| Request or situation | Expected behavior |
|---|---|
| Bug fix | Focus on necessary code and relevant paths; avoid unrelated restructuring |
| Comments added during implementation | Explain necessary reasons and constraints in the appropriate artifact language |
| Documents, review comments, commits, and PRs | Avoid middle dots as separators and unnecessary dashes; preserve required syntax and original text |
| English request | Respond in English while independently preserving existing file languages |
| Conflicting project rules | Ask before affected changes; do not ask about unrelated or compatible rules |
| Verification cannot run | State why it was not run and identify material gaps; do not report a pass |

### Existing project rules

The skill checks applicable instruction files, contribution guides, path-specific rules, templates, and relevant tool settings. Valid prior choices for the same topic and scope are reused before comparing remaining requirements.

| Relationship | Behavior |
|---|---|
| Unrelated rules | Apply each within its scope |
| Identical or compatible rules | Apply together without asking |
| Requirements that cannot both be satisfied | Explain sources and differences, then wait for the user's choice |

Users can choose project rules, Jbeat rules, or resolve individual items. The same choice is not repeatedly requested within its valid project and session scope. New conflicts or material rule changes may require a new choice. Choosing a rule does not authorize unrelated edits or tool-setting changes, and cannot override higher-priority instructions or enforced permissions.

### Inspect or remove the connection

```text
/jbeat-conventions:jbeat-setup status
```

This checks the target instruction file and connection block without changing files. To remove the connection:

```text
/jbeat-conventions:jbeat-setup remove
```

Only the Jbeat-managed block is removed; existing instructions are preserved. This does not uninstall or disable the plugin. Installed skills may still be selected by relevance or invoked explicitly. Already-loaded instructions remain in the current conversation, so check in a fresh session.

Project instruction files can be shared with collaborators when committed. Setup does not automatically commit or push changes.

### Optional explicit invocation

To use the skill for a particular task without a persistent connection, or invoke it directly:

```text
/jbeat-conventions:jbeat-apply Review this patch.
```

To read every reference, pass `all`. Conditional rules remain conditional even when all references are loaded.

```text
/jbeat-conventions:jbeat-apply all
```

### If instructions are not loaded

Use `/memory` to check whether Claude Code reads the instruction file. Direct `AGENTS.md` loading depends on the supported version and Project instructions settings. By default, Claude Code reads files such as `CLAUDE.md` in the project path. Do not assume both filenames are always loaded. See the [official instruction documentation](https://code.claude.com/docs/en/memory#agentsmd).

The connection is a persistent instruction to use the skill. It does not load every installed skill's full content at session start. If the skill is unavailable, the instructions require disclosure rather than claims that rules were read or checks performed. Confirm results through project tests and review.

Static review and actual runtime verification are distinguished in the [validation record](docs/behavior-validation.en.md#current-verification-scope).

### Supported development environments

| Shared principles | Applied only when relevant |
|---|---|
| Scope control, contract preservation, abstraction decisions, honest verification | Tests, type checks, and build tools present in the project |
| Intent-focused comments, prose conventions, language policy | Language-specific documentation such as JS/TS JSDoc or TSDoc |
| Checking third-party usage against installed versions | Browser UI verification, UI messages, and JS console examples |

Python, Java, Go, and other projects follow their own syntax and tools. This package targets Claude Code. Other agents require environment-specific installation and skill connections.

## Commands

The plugin includes two skills: `jbeat-setup` for an explicitly requested project connection, and `jbeat-apply` for relevant engineering tasks.

| Command | Purpose |
|---|---|
| `/jbeat-conventions:jbeat-setup` | Connect project instructions once per project |
| `/jbeat-conventions:jbeat-setup status` | Inspect the connection without changes |
| `/jbeat-conventions:jbeat-setup remove` | Remove only the managed connection block |
| `/jbeat-conventions:jbeat-apply` | Optionally invoke the apply skill directly |
| `/jbeat-conventions:jbeat-apply all` | Optionally read all references |

Ordinary work requests do not require a command after connection. Check the current command menu for availability of the shorter `/jbeat-setup` and `/jbeat-apply` names.

In 1.2.0, setup toggled plugin activation. In 2.0.0, it changed to connecting project instructions. Legacy `on/off` arguments explain migration without changing settings. Manage activation through `/plugin`. Old settings are not automatically removed. After updating, restart and connect each project once.

## Updating

Run in a terminal, then restart Claude Code:

```bash
claude plugin update jbeat-conventions@jbeat-plugins
```

You can also update from the Installed screen in `/plugin`. The connection block references the installed skill name rather than a version-specific cache path. Run setup again to refresh the connection template; user customizations are not overwritten arbitrarily.

Check [Releases](https://github.com/jbeat30/jbeat-conventions/releases) for published versions. If you registered the old marketplace address, see the [installation and setup guide](CONVENTIONS.en.md#installation-and-setup).

## Convention guide

The [detailed guide](CONVENTIONS.en.md) explains the workflow and examples, including [conflict resolution](CONVENTIONS.en.md#project-rules-and-user-choices). The following English reference files are the authoritative rules.

| Topic | Reference |
|---|---|
| Core | [Scope, contracts, structure, and error handling](skills/jbeat-apply/references/core-rules.md) |
| Project rules | [Conflict detection, user choices, and scope](skills/jbeat-apply/references/project-rule-resolution.md) |
| Naming | [Roles, units, and external fields](skills/jbeat-apply/references/naming-conventions.md) |
| Writing | [Middle-dot separators, unnecessary dashes, and exceptions](skills/jbeat-apply/references/writing-conventions.md) |
| Comments | [Intent, constraints, and language-specific conditions](skills/jbeat-apply/references/comment-conventions.md) |
| Language | [User-language responses and artifact-language preservation](skills/jbeat-apply/references/language-conventions.md) |
| Quality | [Task-specific checks and proportional verification](skills/jbeat-apply/references/quality-checklist.md) |
| Reporting | [Executed checks and material verification gaps](skills/jbeat-apply/references/reporting-format.md) |
| Third-party tools | [Versions, official evidence, and conditional browser checks](skills/jbeat-apply/references/tooling-verification.md) |
| Commits and PRs | [Titles, bodies, and meaningful change units](skills/jbeat-apply/references/commit-conventions.md) |

## Optional MCP tools

You can start without MCP. These are examples used when relevant and available; the plugin does not install or configure them.

| Example tool | Use | Alternative |
|---|---|---|
| Context7 | Check third-party API and configuration documentation | Official documentation, installed package types and source |
| chrome-devtools | Inspect browser UI and interactions | Other available browser inspection tools |

Install only tools you need:

```bash
claude mcp add context7 -- npx -y @upstash/context7-mcp
claude mcp add chrome-devtools -- npx -y chrome-devtools-mcp@latest
```

These optional examples use Node.js and npx; the convention skills themselves do not require them. Do not send secrets or internal code in external queries, and inspect approved environments. If an alternative method verified something, do not label it unverified solely because an MCP tool was unavailable.

## Contributing

Share missed conflicts, unnecessary questions, and convention omissions with a reproducible request and expected behavior. Review relevant documentation and the [behavior validation scenarios](docs/behavior-validation.en.md) when making changes.

Follow the [contribution and release guide](.github/BRANCH_STRATEGY.en.md). Normal work branches target `feature/vX.Y.Z`, then proceed through the matching release branch before deployment.

## License and references

[MIT License](LICENSE). For Claude Code behavior, see the official [plugin documentation](https://code.claude.com/docs/en/discover-plugins), [skill documentation](https://code.claude.com/docs/en/skills), and [project instruction documentation](https://code.claude.com/docs/en/memory).
