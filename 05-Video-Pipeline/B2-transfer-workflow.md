---
project: dance-vision-agentic-data-pipeline
type: runbook
---

# B2 transfer workflow

## Core principle

Transfer selected working clips and durable outputs, not the full raw archive, unless a measured and approved batch requires more.

## Standard flow

```text
Read manifest
  → validate source and permission status
  → download selected clip or source file to worker scratch disk
  → process
  → validate outputs
  → upload to versioned B2 output prefix
  → write run manifest
  → remove temporary local worker data
```

## Safety checks

- Read/write B2 prefixes are allowlisted.
- Raw source prefix cannot be written by normal workers.
- Output prefix includes run/model version.
- Upload completion and checksum are verified before GPU worker termination.
- Retention policy distinguishes scratch from durable artifacts.
