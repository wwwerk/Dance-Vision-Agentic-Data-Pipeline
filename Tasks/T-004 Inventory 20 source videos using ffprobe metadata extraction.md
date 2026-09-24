---
id: T-004
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M0
area: inventory
created: 2026-09-23
estimate_hours: 4
tags:
  - task
  - ffmpeg
  - milestone/M0
---

# T-004 Inventory 20 source videos using ffprobe metadata extraction

## Outcome

A first Parquet/CSV manifest contains technical metadata and basic governance status for 20 representative source recordings.

## Acceptance criteria

- [ ] Each record has stable source ID and B2 key or local source location
- [ ] Duration, frame rate, resolution, codec, and audio fields are populated where available
- [ ] Rights/consent status is recorded or marked review-required
- [ ] Errors are logged without halting the entire batch
- [ ] Result is queryable in DuckDB or a spreadsheet

## Linked notes

- [[FFprobe-and-inventory]]
- [[Archive-inventory-notes]]
- [[Source-video-metadata-schema]]
