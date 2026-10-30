# Reporting Format

Follow [language-conventions.md](language-conventions.md) and
[writing-conventions.md](writing-conventions.md). Scale reports to the task;
fixed headings and full checklists are not required for every response.

Include the outcome, meaningful changes, verification actually executed with its
result, material unexecuted verification with reasons, and relevant remaining
risks or unresolved choices. Separate executed and unexecuted checks clearly.

Do not claim type checking, lint, tests, builds, tool calls, runtime behavior, or
future compliance were verified unless evidence supports that exact claim. Source
review differs from execution. A passing build does not establish UI behavior or
every runtime path.

A small edit can need only a short outcome and verification note. Reviews lead
with actionable findings and evidence. Plans distinguish proposals from completed
work. Do not add irrelevant frontend/runtime/order checklist items or imply every
possible unrun check is a defect.

For external documentation, identify source and applicable version. For browser
observations, record a safe URL, viewport, and checked behavior/value. Remove
sensitive query strings or private data from reports.
