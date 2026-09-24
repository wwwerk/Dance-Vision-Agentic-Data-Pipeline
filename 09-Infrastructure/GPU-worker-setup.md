---
project: dance-vision-agentic-data-pipeline
type: infrastructure
status: draft
---

# GPU worker setup

## Role

Temporary, disposable worker for selected video batches: MMPose, detection, tracking, QA, rendering overlays, and optional fine-tuning.

## Worker lifecycle

```text
Provision
  → authenticate with scoped credentials
  → pull pinned container image
  → download selected manifest and inputs
  → process to local scratch disk
  → validate outputs
  → upload artifacts and run manifest
  → confirm upload
  → terminate
```

## Required runtime fields

- Provider and instance ID
- GPU model and VRAM
- CPU/RAM/disk specification
- Image digest
- CUDA/PyTorch/MMPose versions
- Model checkpoint
- Input clip IDs
- Start/end time
- Estimated and actual cost
- B2 output prefix

## Safety

- Use a maximum duration.
- Use maximum spend if provider supports it.
- Do not retain raw source longer than required.
- Do not bake secrets into images.
- Persist checkpoints/output before interruption risk.
