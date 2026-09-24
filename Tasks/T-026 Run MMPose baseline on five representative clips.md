---
id: T-026
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M1
area: inference
created: 2026-09-23
estimate_hours: 5
depends_on:
  - T-025
tags:
  - task
  - MMPose
  - GPU
  - milestone/M1
---

# T-026 Run MMPose baseline on five representative clips

## Outcome

Five selected clips produce pose JSON, overlay videos, run manifests, and an initial qualitative error log.

## Acceptance criteria

- [ ] All clips are rights-cleared for internal processing
- [ ] Each output references the source clip and run ID
- [ ] Overlay videos are rendered and reviewed
- [ ] Major failure categories are recorded
- [ ] GPU time and cost are logged
- [ ] Artifacts are uploaded and verified before worker termination

## Linked notes

- [[EXP-001-pose-baseline]]
- [[MMPose-baseline]]
- [[Pipeline-runbook]]
