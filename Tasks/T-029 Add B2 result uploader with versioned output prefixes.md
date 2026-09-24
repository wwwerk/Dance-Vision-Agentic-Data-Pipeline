---
id: T-029
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M1
area: storage
created: 2026-09-23
estimate_hours: 5
tags:
  - task
  - B2
  - milestone/M1
---

# T-029 Add B2 result uploader with versioned output prefixes

## Outcome

Validated derived artifacts upload to a versioned B2 prefix with a run manifest and integrity verification.

## Acceptance criteria

- [ ] Prefix is generated from approved run/model version
- [ ] Raw source prefix cannot be targeted
- [ ] Expected output list is verified after upload
- [ ] Run manifest is uploaded with artifacts
- [ ] Upload failures are retryable/idempotent where safe
- [ ] Scratch location is not removed until output verification passes

## Linked notes

- [[B2-layout]]
- [[B2-transfer-workflow]]
- [[Pipeline-runbook]]
