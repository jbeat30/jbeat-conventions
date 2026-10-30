# Language Conventions

## Conversation

- Respond in the language of the user's current request, including progress,
  questions, activation messages, and final reports. An explicitly requested
  response language takes precedence.
- For mixed-language input, use the main natural-language request. For code-only
  or ambiguous input, use recent conversation language. Ask only when ambiguity
  materially affects the deliverable.
- Do not default to Korean solely because Jbeat originated in Korean.

## Project artifacts

- First reuse any valid artifact-language choice for the current topic and paths
  under [project-rule-resolution.md](project-rule-resolution.md). Apply the
  following defaults only when no such choice exists. A change of conversation
  language alone does not invalidate an artifact-language choice.
- For new documents, comments, commits, and PRs without an established artifact
  language, Jbeat proposes the user's language. Compare explicit project language
  requirements before adopting that proposal; do not silently select either source.
- Preserve an existing document's or surrounding comments' language unless
  translation is requested. Conversation language alone does not request translation.
- If an explicit project language requirement conflicts with the language Jbeat
  proposes for new text, follow
  [project-rule-resolution.md](project-rule-resolution.md) before writing it.
  An existing document's language is context, not itself a conflict.
- Preserve identifiers, filenames, external fields, contracts, commands, and exact
  quotations. Language choice does not authorize renaming them.
- Korean noun endings suit concise Korean labels and comments, not every language.
