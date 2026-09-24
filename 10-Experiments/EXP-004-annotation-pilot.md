---
id: EXP-004
project: dance-vision-agentic-data-pipeline
type: experiment
status: planned
dataset_version: pilot-v0
tags:
  - experiment
  - annotation
  - CVAT
---

# EXP-004 Annotation pilot

## Question

Do MMPose/tracking prelabels reduce annotation time while preserving or improving label quality for selected human-movement clips?

## Design

- Select representative clips with easy, moderate, and high occlusion.
- Annotate a small matched sample with prelabels.
- If practical, compare against a no-prelabel or minimally assisted condition.
- Record time, correction type, ambiguity rate, and annotator feedback.

## Metrics

- Minutes of annotation per video minute
- Corrections per frame/person
- Track repairs
- Keypoint repairs
- Visibility/occlusion label effort
- Unresolved/adjudicated intervals
