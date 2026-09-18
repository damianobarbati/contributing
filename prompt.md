Act as an expert AI-agent documentation engineer.

## Objective

Generate a maximally compact, operational `./CONTRIBUTING.md` for an AI coding agent by consolidating the repository's relevant Markdown instruction files.

Optimize for:

* Minimum token consumption.
* Maximum instruction density.
* Exact preservation of operational meaning.
* Deterministic agent behavior.
* Zero unnecessary prose.

## Source Discovery

* Recursively scan the current workspace for relevant `*.md` files containing repository instructions, development rules, workflows, conventions, architecture constraints, testing requirements, tooling instructions, or agent guidance.
* EXCLUDE `./CONTRIBUTING.md` from source inputs.
* Ignore Markdown files that contain no operationally relevant instructions.
* Read every selected source file completely before producing the final result.
* NEVER modify, rename, move, or delete any source file.

## Target File

* ALWAYS recreate `./CONTRIBUTING.md` from scratch.
* ALWAYS overwrite any existing `./CONTRIBUTING.md`.
* NEVER preserve previous `./CONTRIBUTING.md` content unless the same information is present in another selected source file.
* `./CONTRIBUTING.md` is the only file you may write.

## Semantic Preservation

* Preserve every instruction that can affect agent behavior, implementation, architecture, testing, tooling, workflow, repository safety, or output correctness.
* Preserve all conditions, exceptions, scopes, priorities, prohibitions, and required sequences.
* NEVER weaken a rule.
* NEVER strengthen a rule beyond its original scope.
* NEVER generalize a scoped rule into a repository-wide rule unless the sources explicitly make it repository-wide.
* NEVER invent requirements, conventions, recommendations, or best practices.
* NEVER infer missing rules from common practice.
* NEVER silently discard conflicting instructions.

## Deduplication

* Merge rules only when they are semantically equivalent.
* Prefer one canonical rule over repeated variants.
* IF two rules overlap but differ in scope, condition, exception, or strength THEN preserve those differences explicitly.
* IF one rule is strictly more specific than another THEN retain the minimum wording needed to preserve both scopes.
* Remove examples only when removing them does not change or clarify required behavior.
* Remove explanatory prose only when it carries no operational constraint.

## Conflict Handling

* IF two source rules conflict but apply to different scopes THEN encode both scopes explicitly.
* IF two source rules conflict and no source-defined precedence resolves the conflict THEN preserve the conflict explicitly in the shortest possible form.
* NEVER choose one conflicting rule arbitrarily.
* Preserve any source-defined precedence, priority, override, or exception relationship exactly.

## Exact Preservation

NEVER alter syntax-critical content, including:

* Terminal commands.
* Shell fragments.
* Code snippets.
* File paths.
* Directory paths.
* URLs.
* Environment-variable names.
* Identifiers.
* Package names.
* Configuration keys.
* CLI flags.
* Version numbers or constraints.
* Glob patterns.
* Regular expressions.
* Literal values.
* Required filenames.

When exact text is operationally significant, preserve it byte-for-byte where practical.

## Compression Rules

* Use the shortest wording that preserves full operational meaning.
* Prefer direct imperatives.
* Prefer flat bullet lists.
* Remove greetings, introductions, conclusions, rationale, commentary, repetition, and conversational filler.
* Remove redundant headings.
* Combine closely related rules when doing so does not reduce precision.
* Do not repeat the same rule in multiple sections.
* Avoid verbose prose when a deterministic constraint is sufficient.

Prefer forms such as:

* `ALWAYS <action>`
* `NEVER <action>`
* `IF <condition> THEN <action>`
* `IF <condition> THEN <action>; OTHERWISE <action>`
* `<scope>: <constraint>`

## Structure

Use compact Markdown with descriptive `##` sections only when needed.

Possible sections include:

* `## Architecture`
* `## Code`
* `## Testing`
* `## Tooling`
* `## Git`
* `## Files`
* `## Security`
* `## Workflow`
* `## Agent Behavior`

Create only sections supported by source content.

Do not create empty sections.

## Validation

Before writing the file, verify:

1. Every operationally relevant source rule is represented.
2. No rule changed meaning.
3. No scoped rule became global accidentally.
4. No condition, exception, precedence rule, or prohibition was lost.
5. No new repository rule was invented.
6. No semantic duplication remains.
7. All syntax-critical commands, paths, literals, and code remain intact.
8. The result cannot be shortened further without losing operational meaning.

## Execution

1. Discover relevant source Markdown files.
2. Read all selected files completely.
3. Extract operational rules.
4. Normalize and categorize them.
5. Deduplicate semantically equivalent rules.
6. Preserve scopes, exceptions, conflicts, and precedence.
7. Compress wording without changing meaning.
8. Validate the result against all source instructions.
9. Overwrite `./CONTRIBUTING.md` with the final consolidated content.

## Output Constraint

* Write the final result to `./CONTRIBUTING.md`.
* Return only the exact content written to `./CONTRIBUTING.md`.
* Do not return analysis, commentary, summaries, explanations, source lists, or change logs.