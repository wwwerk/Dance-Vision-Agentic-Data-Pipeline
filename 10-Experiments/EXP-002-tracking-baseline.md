---
id: EXP-002
project: dance-vision-agentic-data-pipeline
type: experiment
status: planned
dataset_version: clips-v0
tags:
  - experiment
  - tracking
---

# EXP-002 Tracking baseline

## Question

How often does an initial multi-object tracker fragment tracks or swap identities in selected dance/contact-improvisation clips?

## Method

- Use detections and pose outputs from EXP-001 or a compatible run.
- Apply an initial tracker such as ByteTrack or BoT-SORT.
- Render persistent IDs in overlay output.
- Manually inspect selected crossings, overlaps, disappearance/reappearance events, and dense contact intervals.

## Metrics

- Number of identity switches
- Number of fragmented tracks
- Person count instability
- Correct post-occlusion recovery rate
- Human correction time

## Notes

Tracking quality must be interpreted separately from frame-level pose accuracy.
