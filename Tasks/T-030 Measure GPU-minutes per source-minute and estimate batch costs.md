---
id: T-030
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M1
area: cost
created: 2026-09-23
estimate_hours: 2
depends_on:
  - T-026
tags:
  - task
  - cost
  - milestone/M1
---

# T-030 Measure GPU-minutes per source-minute and estimate batch costs

## Outcome

A first evidence-based cost model estimates inference cost for future batches using actual small-batch measurements.

## Acceptance criteria

- [ ] Runtime and cost captured for each clip
- [ ] Input resolution/frame-rate/model configuration recorded
- [ ] Transfer and setup overhead distinguished from inference time where possible
- [ ] Estimate documented for 10 clips, 1 hour, and larger hypothetical batches
- [ ] Recommendation made about GPU provider/instance class for next phase

## Linked notes

- [[Budget-and-cost-model]]
- [[Compute-architecture]]
- [[EXP-001-pose-baseline]]
