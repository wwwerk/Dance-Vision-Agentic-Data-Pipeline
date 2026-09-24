---
id: T-027
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P1
milestone: M1
area: tracking
created: 2026-09-23
estimate_hours: 6
depends_on:
  - T-026
tags:
  - task
  - tracking
  - milestone/M1
---

# T-027 Add ByteTrack or BoT-SORT baseline

## Outcome

A baseline tracker produces persistent person IDs and visual overlays for selected clips.

## Acceptance criteria

- [ ] Track output schema includes stable IDs and frame/time associations
- [ ] Overlay displays IDs for visual inspection
- [ ] Fragmentation and suspected switches are recorded
- [ ] Result is linked to detector/pose model versions
- [ ] A small manual review establishes first error categories

## Linked notes

- [[Detection-and-tracking]]
- [[EXP-002-tracking-baseline]]
