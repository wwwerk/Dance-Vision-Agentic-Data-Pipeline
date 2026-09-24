# Prompt library

## Coding-agent implementation prompt

```text
Read the linked specification and relevant architecture notes. Do not edit code yet.
Produce a phased implementation plan that identifies files to add/change,
assumptions, test strategy, dry-run behavior, failure modes, and security risks.
```

## Coding-agent implementation prompt

```text
Implement only the approved vertical slice. Requirements:
- Python 3.12
- Pydantic v2 models
- pytest tests
- structured JSON logs
- --dry-run support
- no cloud writes during tests
- update README/runbook
Run tests and report changed files plus unresolved issues.
```

## Review prompt

```text
Review this change as a skeptical data/ML infrastructure engineer.
Identify data loss risks, credential exposure, nondeterminism, missing tests,
source-lineage gaps, cost risks, and conflicts with project governance.
Do not modify files.
```

## Runtime batch-planning prompt requirements

- Return only structured output matching `BatchPlan`.
- Cite manifest fields and available metrics for every selection rationale.
- Do not infer rights status beyond supplied records.
- Do not propose a plan exceeding stated budget or annotation capacity.
- Mark missing information explicitly.
