---
project: dance-vision-agentic-data-pipeline
type: runbook
---

# Pipeline runbook

## Preflight

- [ ] Clip IDs are valid and rights status permits the planned action
- [ ] Source paths and output prefix are allowlisted
- [ ] Cost estimate is recorded
- [ ] GPU model, maximum duration, and maximum spend are set
- [ ] Container/model/code versions are pinned
- [ ] B2 credentials are scoped and available only in runtime environment
- [ ] Dry-run passes on the same manifest

## Execute

- [ ] Download selected inputs to worker scratch disk
- [ ] Validate input checksum/metadata
- [ ] Run detector, pose, tracker, and QA stages
- [ ] Render overlay preview
- [ ] Validate artifact schema and expected file list
- [ ] Upload output and run manifest
- [ ] Confirm upload integrity
- [ ] Terminate worker

## Post-run

- [ ] Record actual cost and runtime
- [ ] Review top QA failures and overlay samples
- [ ] Update experiment note
- [ ] Update task evidence
- [ ] Create follow-up tasks for observed failure modes
