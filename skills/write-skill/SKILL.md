---
name: write-skill
description: "Create or update self-contained project skills. Use when writing skill instructions, normalizing their structure, naming skills, or evaluating their behavior."
---

# write-skill

## Goal

Encode a reusable task with precise activation criteria, operational instructions, and an observable completion condition.

## Scope

- Apply to new and edited skill definitions in this project.
- Store each skill in `skills/<verb-object>/SKILL.md`; the directory contains only this self-contained file.
- Keep all instructions and necessary examples inside that file. Project source, manifests, and task inputs remain valid material to inspect.

## Workflow

1. Extract purpose, activation conditions, inputs, expected output, constraints, and completion criteria from the request and existing context. Ask only for missing information that materially changes the result.
2. Choose an English imperative verb followed by its object in lowercase kebab-case: `write-markdown`, `design-api`, `test-browser`. Add object qualifiers only when needed, such as `write-github-actions`. Avoid noun-first names, versions, and numeric suffixes.
3. Match directory name, YAML `name`, and H1 exactly. Name the instruction file `SKILL.md`. Use required frontmatter fields `name` and `description`; preserve additional metadata only when it has a concrete supported purpose.
4. Write a concise description stating capability and when it applies. Add exclusions only to prevent likely misrouting.
5. Use these exact H2 sections, in this order; use H3 or lower for task-specific subdivisions:

| Section | Content |
| --- | --- |
| Goal | Observable result the skill should produce |
| Scope | Applicable work, inputs, boundaries, and relevant modes |
| Workflow | Steps and decision criteria for completing the task |
| Rules | Non-obvious constraints and reasons where useful |
| Verification | Evidence and checks needed to establish completion |
| Output | Deliverable format, required evidence, and limitations |

6. Consolidate duplicate rules and inline necessary knowledge from existing resources. Remove activation-time dependencies on sibling skills, references, scripts, templates, or metadata files bundled with the skill.
7. Review realistic requests that should and should not activate the skill. For substantial behavioral changes, use small representative examples and compare observable outcomes; expand evaluation only when warranted.

## Rules

- Keep each skill concise and self-contained. Aim for roughly 50–200 lines; retain necessary details rather than padding short skills or cutting critical constraints to meet a quota.
- Include only guidance that changes decisions or improves results. Remove generic advice, motivational prose, repeated rules, and copied manuals.
- Use imperative, content-only English. Preserve commands, useful examples, concrete values, exceptions, and non-obvious rationale.
- Do not create skill-owned `references/`, `scripts/`, `assets/`, or `agents/` files. Inline essential snippets and templates; use internal anchors when navigation helps.
- Do not require reading or invoking another skill to complete this one. Describe the necessary behavior locally.
- Keep external documentation optional background, not required instructions. Reading target-project instructions and task inputs is allowed.
- Preserve user intent, authorization, and scope. Do not impose approval, installation, publication, delegation, or benchmark workflows unless the task requires them.
- If consolidation reveals distinct capabilities, give each a meaningful verb-object name; avoid `-2` or `-v2` alternatives.

## Verification

- Confirm valid YAML frontmatter with nonempty `name` and `description`.
- Confirm directory name, `name`, and H1 agree and follow verb-object kebab-case; confirm the only skill file is `SKILL.md`.
- Confirm all six H2 sections appear once, in order, with meaningful content.
- Confirm no required instructions or helper files remain outside the skill; check internal anchors and code fences.
- Check positive and near-miss activation examples; verify workflow completion and stated limits.
- For migrations, compare against original instructions: retain meaningful constraints, examples, and exceptions; remove only duplication, obsolete dependencies, or contradicted conventions.

## Output

Return the skill file or requested edit, with a concise account of changes and validation. Report unresolved assumptions or behavioral checks that were not run.
