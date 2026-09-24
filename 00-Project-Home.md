---
project: dance-vision-agentic-data-pipeline
status: active
started: 2026-09-23
target-first-milestone: 2026-12-22
owner: Me
tags:
  - project/dance-vision
  - project/agentic-ai
  - project/computer-vision
  - project/dataset-engineering
---

# Dance Vision Agentic Data Pipeline

## Project statement

Build a low-cost, reproducible, human-governed pipeline that converts selected video from a large Backblaze B2 archive into structured computer-vision datasets for human movement analysis.

The first target dataset is an occlusion-aware, multi-person 2D pose-tracking benchmark drawn from dance, contact improvisation, performance, and yoga footage.

The project also develops practical skill in agentic coding, Python data engineering, cloud/VPS orchestration, ephemeral GPU compute, video processing, CV inference, annotation, dataset governance, and technical communication.

## First measurable deliverable

```text
B2 source video
  → manifest entry
  → selected short clip
  → ffprobe metadata
  → proxy or working clip
  → MMPose plus tracking baseline
  → JSON and overlay output
  → B2 artifact upload
  → human-reviewed QA report
```

## Current phase

[[01-Roadmap#Phase 1 — Foundation and inventory]]

## Current milestone

**M1: End-to-end technical vertical slice**

Target: 2026-10-20

## Current next actions

- [ ] [[T-001 Create Git repository and baseline project README]]
- [ ] [[T-002 Create B2 storage-layout document and artifact naming policy]]
- [ ] [[T-003 Define video, clip, run, and consent metadata schemas]]
- [ ] [[T-004 Inventory 20 source videos using ffprobe metadata extraction]]
- [ ] [[T-005 Select 20 representative candidate clips]]

## Dashboards

- [[01-Roadmap]]
- [[02-Backlog]]
- [[03-Decisions]]
- [[04-Risks-and-Governance]]
- [[10-Experiments/Experiment-index]]
- [[12-Portfolio/Case-study-outline]]

## Principles

1. Raw masters are immutable.
2. Every derived artifact is traceable to a source video and pipeline run.
3. LLMs propose plans; deterministic Python tools execute costly or destructive work.
4. Humans approve rights-sensitive, cost-sensitive, and publication-sensitive actions.
5. No broad archive sweep until cost-per-video-minute and failure modes are measured.
6. Start with small, difficult, consent-cleared, well-documented clips.
7. Maintain reproducibility through manifests, versioned outputs, tests, and Git.
8. Keep public and restricted material clearly separated.
