---
name: jbeat-setup
classification: capability
classification-reason: "One-time initial setup command for the jbeat-conventions plugin. Writes the required entries into the user's ~/.claude/settings.json."
deprecation-risk: none
description: |
  Run once after installing jbeat-conventions to configure Claude Code automatically.
  Creates ~/.claude/settings.json if absent, adds missing entries if needed, keeps existing entries untouched.
  Triggers: jbeat setup, jbeat init, jbeat install, 초기 설정, 세팅, setup
argument-hint: "(no argument needed)"
user-invocable: true
allowed-tools:
  - Read
  - Edit
  - Write
  - Bash
---

# Jbeat Conventions — Setup

Configures `~/.claude/settings.json` for the jbeat-conventions plugin.

---

## Step 1 — Resolve path

```bash
echo "$HOME/.claude/settings.json"
```

---

## Step 2 — Read settings.json

Try to read `~/.claude/settings.json`.

- File does not exist → go to Step 3A
- File exists → go to Step 3B

---

## Step 3A — File does not exist: create it

Write `~/.claude/settings.json` with the following content:

```json
{
  "enabledPlugins": {
    "jbeat-conventions@jbeat-plugins": true
  },
  "extraKnownMarketplaces": {
    "jbeat-plugins": {
      "source": {
        "source": "github",
        "repo": "jbeat30/jbeat-conventions"
      }
    }
  }
}
```

Then go to Step 4 (newly configured).

---

## Step 3B — File exists: check entries

Check for both of the following:

**A.** `enabledPlugins` contains `"jbeat-conventions@jbeat-plugins": true`

**B.** `extraKnownMarketplaces` contains `"jbeat-plugins"` with:
```json
{
  "source": {
    "source": "github",
    "repo": "jbeat30/jbeat-conventions"
  }
}
```

- Both present → go to Step 5 (already configured)
- One or both missing → add only the missing entries using Edit, preserve all existing keys → go to Step 4

---

## Step 4 — Report: newly configured

Run this Bash command first:
```bash
printf '\033[32mSUCCESS!\033[0m\n'
```

Then output:

```
jbeat-conventions 설정이 완료되었습니다.

사용 가능한 명령어:
  /jbeat-conventions  — 컨벤션 적용
  /jbeat-apply        — 모든 컨벤션 파일 로드
```

---

## Step 5 — Report: already configured

Output:

```
이미 설정되어 있습니다. 바로 사용하셔도 됩니다.

사용 가능한 명령어:
  /jbeat-conventions  — 컨벤션 적용
  /jbeat-apply        — 모든 컨벤션 파일 로드
```
