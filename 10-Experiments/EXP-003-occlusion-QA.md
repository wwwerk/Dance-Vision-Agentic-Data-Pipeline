---
id: EXP-003
project: dance-vision-agentic-data-pipeline
type: experiment
status: planned
dataset_version: clips-v0
tags:
  - experiment
  - occlusion
  - QA
---

# EXP-003 Occlusion QA signals

## Question

Which automated metrics best identify intervals needing human review for occlusion, missed detections, and probable identity swaps?

## Candidate signals

- Low keypoint confidence
- Bounding-box overlap
- Detection disappearance/reappearance
- Track fragmentation
- Abrupt skeleton displacement
- Limb-length inconsistency
- Person-count changes
- Model disagreement

## Evaluation

Create a manually reviewed sample of flagged and unflagged intervals. Measure the fraction of flagged intervals that actually need correction and the fraction of serious errors that were caught.
