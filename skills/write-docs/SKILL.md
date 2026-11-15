---
name: write-docs
description: "Create, review, and reorganize technical documentation using Diátaxis to match reader needs. Use for tutorials, how-to guides, API and configuration references, conceptual explanations, and documentation structure; exclude ordinary prose and code changes."
---

# write-docs

## Goal

Produce accurate technical documentation that helps the intended reader learn, complete a task, look up facts, or understand a concept.

## Scope

- Apply to new documentation, requested edits, documentation reviews, and information architecture changes.
- Use project instructions, existing documentation, source code, configuration, tests, and relevant authoritative documentation as inputs.
- Match the depth of work to the request. Review-only requests produce findings; small corrections do not require restructuring the documentation system.

## Workflow

1. Inspect project instructions, existing documentation, and the implementation or other authoritative sources relevant to the request. Identify conventions, terminology, supported versions, and the requested destination.
2. Derive the audience, reader goal, prerequisites, and expected result from the request and available context. Ask only for missing information that materially changes the result.
3. Choose the dominant documentation type using the table below. Preserve useful existing structure; use Diátaxis to resolve reader needs rather than impose four separate documents on every request.
4. Draft or revise within the requested scope. State prerequisites and expected results for procedures, use consistent terminology, and link to existing reference or explanation pages when readers need more detail.
5. Verify technical claims and examples against the relevant sources. Resolve discrepancies where evidence permits; identify unresolved conflicts or unavailable evidence instead of inventing behavior.
6. Check the document for its intended reader, then deliver the requested artifact or review with verification results and remaining limitations.

### Documentation types

| Reader need | Type | Structure and writing pattern | Review criteria |
| --- | --- | --- | --- |
| Learn by doing for the first time | Tutorial | Task title such as "Build your first X"; goal, prerequisites, numbered steps, observable checkpoints, final outcome. Keep explanation focused on completing the learning exercise. | Include the instructions a beginner needs from setup through the final result. |
| Complete a known task | How-to guide | Task title such as "Configure X"; goal, assumptions, steps, expected result. Assume baseline knowledge and include relevant alternatives or conditions. | Cover the stated task and the conditions that change its procedure. |
| Look up technical facts | Reference | Name the subject, such as "Configuration options"; use consistent entries with applicable fields such as name, type, default, constraints, description, and example. | Make entries easy to locate and reconcile their facts with the documented version. |
| Understand a concept or rationale | Explanation | Concept title such as "How X works"; context, core concepts, rationale, alternatives, and trade-offs. | Explain the relationships and reasons without turning the page into a procedure or exhaustive specification. |

## Rules

- Give each page a dominant purpose. Allow brief context, examples, or reference details needed to use it; split or cross-link substantial material serving a different reader need when the requested scope permits.
- Preserve existing navigation, headings, language, and terminology unless changing them is necessary for the task. Avoid unrelated rewrites and new pages that duplicate existing material.
- Ground commands, API signatures, parameters, defaults, paths, and version claims in inspected sources. Distinguish current implementation from intended or proposed behavior when they differ.
- Do not invent outputs, supported features, compatibility guarantees, or design rationale. State assumptions and unresolved gaps explicitly.
- Use runnable examples with concrete values where practical. Mark placeholders and explain required substitutions; keep secrets out of examples.
- Keep code snippets as concise as possible while preserving correctness and the details needed to understand them. Use `ofetch` for examples that make fetch calls.
- Run examples or documentation checks when available, safe, and relevant. Do not execute destructive or external mutations merely to validate a procedure; report what was checked by inspection instead.
- Keep instructions and necessary examples self-contained. Link to supporting documentation without making readers discover missing procedural steps elsewhere.
- Treat reader comprehension and ease of lookup as review goals. Do not claim measured usability or successful execution without evidence.

## Verification

- Confirm that the document serves the intended audience and dominant reader need using the type-specific review criteria.
- Compare changed technical details with source code, configuration, tests, or authoritative documentation for the relevant version.
- Check command order, prerequisites, substitutions, and expected outcomes. Run applicable examples or available documentation checks; distinguish execution from static inspection.
- Check Markdown structure, code fences, internal links, anchors, and changed navigation. Verify external links when relevant and accessible; report any that could not be checked.
- Re-read for omitted conditions, inconsistent terminology, duplicated content, and edits outside the requested scope.

## Output

Return or save documentation at the requested destination. For edits, summarize material changes; for reviews, provide actionable findings with locations and reader impact.

Report checks performed, assumptions, unresolved source conflicts, and any examples or links that remain unverified. Do not present editorial review as user testing.
