---
id: T-022
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M1
area: storage
created: 2026-09-23
estimate_hours: 6
tags:
  - task
  - B2
  - security
  - milestone/M1
---

# T-022 Build B2 download helper with allowlisted source prefixes

## Outcome

A tested storage helper retrieves only manifest-approved objects from allowlisted B2 prefixes and writes them to a defined scratch location.

## Acceptance criteria

- [ ] Source key is validated against manifest
- [ ] Prefix allowlist rejects arbitrary bucket paths
- [ ] Credentials are environment-injected, not hard-coded
- [ ] Download result records checksum/size when feasible
- [ ] Dry-run mode makes no network request
- [ ] Tests mock B2 client behavior

## Linked notes

- [[B2-transfer-workflow]]
- [[B2-layout]]
- [[Security-and-access]]
