---
name: design-feature
description: "Define software features from raw requirements or user problems. Use for functional requirements, user stories, acceptance criteria, technical specifications, and implementation plans."
---

# design-feature

## Goal

Define the smallest useful feature that solves an identified user problem.

## Scope

Cover discovery, feasibility, requirements, risks, and planning. A design request produces a specification; implement only when requested.

## Workflow

1. Identify the problem, target users, current workaround, and concrete value. Resolve unclear problem statements before inventing functionality.
2. Define the smallest useful release. Separate essential requirements from deferred options; identify technical, time, and resource constraints.
3. Write concise user stories and observable acceptance criteria with explicit pass/fail outcomes.
4. Describe main flows, relevant error and boundary states, permissions, data needs, and affected interfaces.
5. Assess impact on existing functionality, dependencies, technical debt, and worst-case failures.
6. When requested, order implementation by dependencies and tie each step to acceptance criteria.

## Rules

- Prefer the simplest viable solution within the user's constraints.
- Remove marginal requirements that delay the useful release; record consequential tradeoffs.
- Use concrete behavior and user outcomes rather than business jargon.
- Distinguish confirmed requirements, assumptions, and unresolved product decisions.

## Verification

- Check every requirement against the identified problem and release scope.
- Confirm acceptance criteria are observable, unambiguous, and cover significant failure paths.
- Check feasibility and compatibility with existing contracts; flag risks without presenting assumptions as facts.

## Output

Return problem, users, scope, functional requirements or stories, acceptance criteria, risks, and open questions. Include a technical specification or implementation sequence only when requested.
