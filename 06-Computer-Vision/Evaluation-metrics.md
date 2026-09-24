---
project: dance-vision-agentic-data-pipeline
type: evaluation
---

# Evaluation metrics

## Pose

- Keypoint accuracy using appropriate pose metric
- Visible-joint accuracy
- Occluded-but-labelled joint accuracy
- Per-joint error profile

## Detection

- Person detection precision and recall
- Missed persons
- Duplicate detections

## Tracking

- IDF1 or similar identity metric
- HOTA/MOTA where appropriate
- Identity switches
- Track fragmentation
- Occlusion recovery correctness

## Temporal quality

- Skeleton jitter
- Implausible limb-length variance
- Implausible velocity/acceleration

## Human utility

- Annotation time per video minute
- Prelabel correction time versus no-prelabel time
- Review precision of automated QA flags
- Cost per useful reviewed minute
