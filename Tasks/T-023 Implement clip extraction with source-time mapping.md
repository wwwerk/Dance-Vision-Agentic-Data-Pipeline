---
id: T-023
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M1
area: media
created: 2026-09-23
estimate_hours: 6
tags:
  - task
  - ffmpeg
  - milestone/M1
---

# T-023 Implement clip extraction with source-time mapping

## Outcome

A reliable clip-extraction utility creates selected derivatives while retaining source ID, start/end time, frame mapping, transformation configuration, and checksum.

## Acceptance criteria

- [ ] Source time range is validated against video duration
- [ ] Stream-copy and re-encode behavior are documented
- [ ] Clip manifest is updated or produced atomically
- [ ] Output naming uses stable `clip_id`
- [ ] Tests cover invalid and boundary time ranges

## Linked notes

- [[Clip-extraction]]
- [[Clip-manifest-schema]]
