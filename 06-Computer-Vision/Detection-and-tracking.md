---
project: dance-vision-agentic-data-pipeline
type: cv-plan
---

# Detection and tracking

## Pipeline concept

```text
video
  → person detector
  → per-person pose estimator
  → multi-object tracker
  → optional ReID association
  → temporal plausibility checks
  → review candidates
```

## Tracking objectives

- Maintain persistent person IDs across frames.
- Preserve identity through short occlusion intervals when evidence is adequate.
- Flag likely identity switches rather than silently asserting continuity.
- Measure fragmentation, missed tracks, merges, and switches.

## Candidate tools

- Detector compatible with MMPose top-down workflow
- ByteTrack or BoT-SORT for initial multi-object tracking
- Appearance/ReID embedding as a later refinement

## Important limitation

Dense physical contact and merged silhouettes remain a hard problem. The pipeline should expose uncertainty for human review rather than forcing a false deterministic answer.
