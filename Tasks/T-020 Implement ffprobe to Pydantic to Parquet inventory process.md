---
id: T-020
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M1
area: inventory
created: 2026-09-23
estimate_hours: 8
depends_on:
  - T-003
  - T-004
tags:
  - task
  - ffmpeg
  - testing
  - milestone/M1
---

# T-020 Implement ffprobe to Pydantic to Parquet inventory process

## Outcome

A tested Python vertical slice reads a defined input list, runs ffprobe, validates metadata with Pydantic, and writes a queryable Parquet inventory manifest.

## Acceptance criteria

- [ ] Supports fixture/local files before B2 integration
- [ ] Uses typed models and structured error records
- [ ] Produces deterministic output schema
- [ ] Unit tests cover normal, missing, and malformed metadata
- [ ] Dry-run behavior is documented
- [ ] Parquet result can be queried with DuckDB

## Linked notes

- [[FFprobe-and-inventory]]
- [[Source-video-metadata-schema]]
- [[Prefect-orchestration]]
