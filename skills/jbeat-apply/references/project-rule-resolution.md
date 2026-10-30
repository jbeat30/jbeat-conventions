# Project Rule Resolution

## Discover applicable rules

Before applying conventions, inspect host-supplied instructions and relevant
repository guidance such as `CLAUDE.md`, `AGENTS.md`, contribution guides,
path-specific instructions, PR templates, and formatter/linter settings. Respect
file scope and the host's instruction hierarchy. Read enough of the current task's
area to compare requirements; do not crawl the repository or home directory.
Existing code shows practice but is not automatically a binding rule.

## Reuse existing choices before comparing

After identifying the applicable sources, check the conversation for an explicit
choice already made in this project and session. A choice record includes topic,
selected requirement/source, and applicable paths or scope. Reuse it before
calculating fresh defaults, including artifact language. Do not ask again merely
because the user changed conversation language or started another task covered
by that choice. A new explicit instruction can revise the choice.

Check that the relevant rules have not materially changed and the current paths
are covered. Do not extend a path-limited choice to another directory. Compare
only topics without a valid choice, or topics affected by a new conflict or a
material rule change. Record the replacement scope when a choice is revised.

## Compare and ask only for conflicts

| Relationship | Action |
|---|---|
| Unrelated topics | Apply each where relevant |
| Same requirement | Apply once without asking |
| More specific but compatible requirement | Satisfy both without asking |
| Requirements cannot both be satisfied for this task | Ask before the affected action |

For actual conflicts, show the topic, each requirement, project source path and
section, and the effects of each choice. Bundle known conflicts into one concise
question in the user's language. Offer project rules, Jbeat rules, or per-topic
selection. The choice covers conflicting topics only; other rules still apply.

Example: a project requires English comments while Jbeat's applicable fallback
would produce Korean comments. Ask which comment-language convention to use.
A project requiring useful policy comments is compatible with Jbeat and needs
no question. A required PR template can also be compatible with Jbeat's default
body guidance; do not manufacture a conflict where a default permits adaptation.

Wait for an answer before changes dependent on disputed rules. Continue independent
investigation or work. Silence is not a choice. Do not choose either source by
default when a real conflict remains. An explicit choice already given suffices.

## Choice scope and boundaries

- Reuse the choice for the same topics in the same project and session. Ask again
  only for new conflicts, material changes to relevant rules, or a user request.
  If prior choices are unavailable after a context reset, do not invent them.
- Briefly record the topic, selected requirement/source, and applicable paths or
  scope in conversation. Do not persist choices
  or edit instructions/configuration without authorization.
- Choosing a convention does not authorize normalizing unrelated files or changing
  formatter, linter, or CI settings. Explain when the choice would fail existing
  checks and resolve configuration scope before changing those settings.
- Host/system instructions, enforced organizational policies, access controls,
  and tool permissions are not selectable conventions. Explain limits rather than
  offering an option the agent cannot honor. Resolve ordinary project convention
  conflicts within that hierarchy using the user's explicit choice.
