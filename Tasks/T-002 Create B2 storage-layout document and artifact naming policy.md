---
id: T-002
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M0
area: storage
created: 2026-09-23
estimate_hours: 2
tags:
  - task
  - B2
  - milestone/M0
---

# T-002 Create B2 storage-layout document and artifact naming policy

## Outcome

A documented B2 prefix structure and naming policy separates raw sources, manifests, working files, inference outputs, annotations, and releases.

## Acceptance criteria

- [ ] Raw prefix is explicitly immutable to ordinary workers
- [ ] Derived artifact prefixes include versioning strategy
- [ ] Scratch retention policy is described
- [ ] Naming includes stable IDs and source lineage
- [ ] Read/write credential scopes are documented

## Linked notes

- [[B2-layout]]
- [[Data-architecture]]
- [[B2-transfer-workflow]]
