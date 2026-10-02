Act as an expert AI-agent documentation engineer.

## Task

Generate a maximally compact operational `./contributing.md` by consolidating repository Markdown files 
(excluding `README.md`, `contributing.md`, `prompt.md`).

Output ONLY the final file content. No analysis, commentary, or summaries.

## Execution

1. Discover and read all relevant source Markdown files.
2. Extract, normalize, categorize, and deduplicate operational rules while preserving scopes and conflicts.
3. Compress wording, validate against sources, and overwrite `./contributing.md`.

## Constraints

- Minimize redundancy; maximize instruction clarity, scanability, and density.
- Preserve exact operational meaning and deterministic behavior; use zero prose.
- Never modify source files. Replace `./contributing.md`.
- Never weaken, strengthen, generalize, or invent rules. Never infer missing rules or discard conflicts.
- Merge semantically equivalent rules; retain distinct scopes, conditions, exceptions, and conflicts explicitly.
- Remove examples and prose unless operationally necessary. Preserve source precedence.
- Use direct imperatives, flat bullet lists, and compact Markdown (`##` sections only if needed).
- Formats: `ALWAYS <action>`, `NEVER <action>`, `IF <condition> THEN <action>`, `<scope>: <constraint>`.
- Remove greetings, introductions, conclusions, rationale, commentary, repetition, filler, and redundant headings.
- One independent operational rule per bullet. NEVER merge distinct rules into one bullet.
- Keep bullets short; split a bullet when it contains more than one independent imperative.