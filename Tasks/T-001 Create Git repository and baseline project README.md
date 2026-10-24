---
id: T-001
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M0
area: foundation
created: 2026-09-23
estimate_hours: 2
tags:
  - task
  - milestone/M0
---

# T-001 Create Git repository and baseline project README

## Outcome

A private Git repository exists for code, infrastructure, schemas, tests, and public-safe documentation. The Obsidian vault may live alongside it or in a dedicated documentation directory, depending on preferred Git workflow.

## Acceptance criteria

- [x] Repository initialized with a clear name
- [ ] README explains project purpose and first vertical slice
- [ ] `.gitignore` excludes `.env`, credentials, large local media, cache, and build artifacts
- [ ] `.env.example` lists variable names only
- [ ] License decision is recorded
- [ ] Initial commit exists

## Evidence

- Repository URL or local path: https://github.com/wwwerk/dance-vision
- Documentation (Obsidian): https://github.com/wwwerk/wwwerk-dance-vision-archive
- Initial commit: https://github.com/wwwerk/dance-vision/commit/6d27a4429fc6a0ab07fdc36ecd703d9fef4b5779

## Linked notes

- [[Project-charter]]
- [[Security-and-access]]
- [[Public-repository-plan]]
