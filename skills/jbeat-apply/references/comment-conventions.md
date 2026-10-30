# Comment Conventions

Use [writing-conventions.md](writing-conventions.md) for punctuation and
[language-conventions.md](language-conventions.md) for language. Review/PR comments
are prose covered by writing rules; the following concerns source code.

## Content and native syntax

- Explain non-obvious reasons, policy, constraints, external contracts, side effects,
  performance tradeoffs, and legacy fallbacks when names and types are insufficient.
- Avoid restating code, speculative notes, stale status, and procedural narration.
  Do not add comments merely to satisfy a count or template.
- Update comments made inaccurate by the requested change.
- Use native comment syntax and project documentation tools. Python docstrings,
  Go comments, and Java documentation are not subject to JS syntax.
- Under the Jbeat choice, short Korean source comments use concise noun endings
  without a final period. Avoid `~입니다`, `~합니다`, `~하고 있습니다`, and redundant
  narration. For example, use `서버 정책에 따른 재시도 횟수 제한`, not a sentence ending
  in `제한합니다`. This is a style requirement for these comments, not a request to
  add comments unnecessarily. Resolve conflicting project requirements before use.
  Other languages, exact quotations, and multi-sentence documentation follow their
  natural punctuation and applicable documentation conventions.

## Conditional JS/TS guidance

Apply only in JS/TS and when compatible with project tooling:

- Prefer JSDoc/TSDoc for public contracts needing explanation of parameters,
  returns, exceptions, side effects, or examples. Do not require blocks for every
  export or tags repeating an obvious type signature.
- Use short `//` comments for non-obvious branch reasons or local context. Trailing
  comments are useful only when the name is insufficient.
- Tooling may require documentation on variables, internal APIs, or file headers.
  Do not prohibit it solely because the symbol is not a public function.
