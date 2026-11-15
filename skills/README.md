# Skills

Each skill defines a reusable task in a self-contained `SKILL.md` file:

```text
skills/
└── <verb-object>/
    └── SKILL.md
```

Skill names use English verb-object kebab-case, such as `design-api` or `test-browser`.   
Skills are defined as single `SKILL.md`, including all necessary instructions and examples.

The directory name, `name` field, and H1 heading must match. Six sections follow, in this order:

| Section | Purpose |
| --- | --- |
| Goal | Expected result |
| Scope | Applicable tasks, inputs, and boundaries |
| Workflow | Steps and decision criteria |
| Rules | Task-specific constraints |
| Verification | Checks that establish completion |
| Output | Deliverables and reporting format |

See [write-skill](write-skill/SKILL.md) for the complete authoring conventions.
