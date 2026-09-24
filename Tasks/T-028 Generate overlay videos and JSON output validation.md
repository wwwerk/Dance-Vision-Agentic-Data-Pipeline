---
id: T-028
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M1
area: qa
created: 2026-09-23
estimate_hours: 5
tags:
  - task
  - QA
  - milestone/M1
---

# T-028 Generate overlay videos and JSON output validation

## Outcome

Inference output is made inspectable through overlays and blocked from downstream use if schema/lineage checks fail.

## Acceptance criteria

- [ ] Overlay includes pose, track ID, and optional confidence/flag display
- [ ] JSON schema validation runs automatically
- [ ] Invalid frame indexes, missing IDs, malformed keypoints, and missing run metadata fail validation
- [ ] Validation report is stored with results

## Linked notes

- [[QA-heuristics]]
- [[Pipeline-runbook]]
- [[Agent-tool-contracts]]
