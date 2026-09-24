---
project: dance-vision-agentic-data-pipeline
type: charter
status: active
---

# Project charter

## Purpose

Create a reproducible, privacy- and rights-aware pipeline for building useful human-movement datasets from a large video archive. The first dataset emphasizes multi-person movement, occlusion, temporal identity, and annotation quality.

## Scope

### In scope

- Video inventory and selective sampling from Backblaze B2
- FFprobe/FFmpeg processing, clip extraction, proxies, and manifests
- 2D multi-person pose estimation, tracking, overlays, and QA signals
- Human annotation and review using CVAT or equivalent tooling
- Dataset schemas, validation, documentation, rights tracking, and model evaluation
- Agentic planning with strict validation and human approval

### Out of scope for the first release

- Processing the whole archive
- Publishing any footage without explicit rights review
- Full 3D reconstruction
- Fully autonomous label correction
- General-purpose action recognition or generative choreography systems
- Permanent GPU infrastructure

## Success criteria

See [[Success-criteria]].

## Constraints

- Local computer is an older Intel MacBook Pro on macOS 11.7.
- Raw archive is stored primarily in Backblaze B2.
- GPU computing should be temporary, capped, and low-cost.
- The project must preserve a path toward a public portfolio without exposing restricted media.
- The stack should teach agentic coding and automation, not hide the underlying engineering.
