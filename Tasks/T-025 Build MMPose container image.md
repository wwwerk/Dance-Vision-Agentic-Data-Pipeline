---
id: T-025
project: dance-vision-agentic-data-pipeline
type: task
status: backlog
priority: P0
milestone: M1
area: inference
created: 2026-09-23
estimate_hours: 6
depends_on:
  - T-020
  - T-022
tags:
  - task
  - MMPose
  - GPU
  - Docker
  - milestone/M1
---

# T-025 Build MMPose container image

## Outcome

A reproducible Docker image runs selected MMPose inference and tracking jobs on a temporary NVIDIA GPU worker.

## Acceptance criteria

- [ ] Docker image builds from a versioned Dockerfile
- [ ] Python, CUDA, PyTorch, MMPose, FFmpeg, and tracker dependencies are pinned
- [ ] The image runs on one fixture video in a GPU environment
- [ ] The job writes a machine-readable run manifest
- [ ] The job can upload outputs to a restricted B2 project prefix
- [ ] The job has an explicit `--dry-run` mode
- [ ] No B2 secret is baked into the image
- [ ] Image digest or Git commit is recorded in every run

## Risks

- Model-image compatibility or CUDA mismatch
- GPU worker loss before outputs are uploaded
- Inadequate local scratch disk
- Source video transfer dominates run time
- Pose estimator performs poorly on dense contact/occlusion scenes

## Linked notes

- [[MMPose-baseline]]
- [[GPU-worker-setup]]
- [[Docker-images]]
