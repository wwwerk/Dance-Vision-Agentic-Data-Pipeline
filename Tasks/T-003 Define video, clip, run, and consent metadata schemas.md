---
id: T-003
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M0
area: schemas
created: 2026-09-23
estimate_hours: 4
tags:
  - task
  - milestone/M0
  - dataset
---

# T-003 Define video, clip, run, and consent metadata schemas

## Outcome

Versioned Pydantic or JSON-schema models exist for source video, clip manifest, pipeline run, and rights/consent records.

## Acceptance criteria

- [ ] Required fields are defined
- [ ] IDs and lineage fields are consistent across schemas
- [ ] Rights and consent state is explicit
- [ ] Example valid and invalid fixtures exist
- [ ] Schema changes are versioned and documented

## Linked notes

- [[Source-video-metadata-schema]]
- [[Clip-manifest-schema]]
- [[Rights-consent-policy]]
- [[Agent-tool-contracts]]
