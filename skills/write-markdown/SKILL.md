---
name: write-markdown
description: "Write concise Markdown instructions and documentation for AI agents. Apply to newly created or edited .md content, including skills and project rules; exclude README.md."
---

# write-markdown

## Goal

Produce content-only Markdown that preserves meaning, concrete details, and navigation.

## Scope

- Apply only to Markdown content being created or edited, except `README.md`.
- Leave surrounding content outside the requested change untouched.
- For skill definitions, use the self-contained structure specified below.

## Workflow

1. Lead with the rule, outcome, or required action. Keep rationale adjacent when it explains scope or a non-obvious constraint.
2. Replace verbose prose with direct sentences or imperative fragments where meaning survives.
3. Use lists or tables for commands, paths, options, and comparisons; retain headings for navigation.
4. For project skills, use `skills/<verb-object>/SKILL.md`, with directory name matching YAML `name` and H1. Include `name` and `description` frontmatter, then H2 sections `Goal`, `Scope`, `Workflow`, `Rules`, `Verification`, `Output`, in that order. Keep instructions and examples inline; require no companion files or sibling skills.
5. Re-read the result for lost conditions, exceptions, or intent.

## Rules

- Remove emojis, badges, motivational lines, empty introductory headings, hedging, repeated titles, and conclusions that only repeat earlier content.
- Avoid a table of contents for short documents, excessive emphasis, and decorative horizontal rules.
- Preserve commands, code, useful examples, concrete values, paths, flags, edge cases, and caveats. Drop duplicate examples only when they add no information.
- Preserve explanations that change how a rule is applied. Compression must not change meaning, scope, or conditions.
- Keep structured tables and valid heading hierarchy.

Example:

```text
Before: In order to run the checks, you should first configure the environment variables.
After: Configure environment variables before running checks.
```

## Verification

- Remove lines that add no information.
- Restore details whose removal changes meaning or applicability.
- Confirm valid Markdown, intact code fences, and working links or anchors.

## Output

Return or save the requested Markdown content in its requested destination. Summarize material changes when editing files.
