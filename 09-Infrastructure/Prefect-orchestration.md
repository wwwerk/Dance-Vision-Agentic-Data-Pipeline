---
project: dance-vision-agentic-data-pipeline
type: infrastructure
---

# Prefect orchestration

## Role

Prefect runs deterministic Python workflows with retries, logs, state, and scheduling.

## Initial flows

```text
inventory_flow
clip_selection_flow
gpu_inference_flow
annotation_export_flow
dataset_validation_flow
benchmark_flow
```

## Rules

- Retry only idempotent operations where safe.
- Tag runs with a batch ID and dataset/pipeline version.
- Keep a dry-run path using fixtures/local outputs.
- Store run manifests and artifacts in versioned locations.
- Do not allow an LLM to alter an approved flow payload after human approval.

## First vertical flow

```text
manifest row
  → source validation
  → selected clip acquisition
  → ffprobe/proxy
  → inference
  → tracker/QA
  → output validation
  → B2 upload
  → run record
```
