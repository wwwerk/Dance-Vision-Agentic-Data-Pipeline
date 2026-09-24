---
id: EXP-001
project: dance-vision-agentic-data-pipeline
type: experiment
status: planned
dataset_version: clips-v0
model_version: TBD
pipeline_version: TBD
hardware: TBD
cost_usd: TBD
tags:
  - experiment
  - MMPose
  - milestone/M1
---

# EXP-001 Baseline pose estimation

## Question

Can a pretrained multi-person 2D pose baseline produce useful first-pass skeletons on a representative selection of human-movement clips, including difficult contact/occlusion conditions?

## Hypothesis

The baseline will work acceptably for isolated or moderately separated dancers but show missed persons, incorrect joints, and unstable identities in dense physical contact and severe occlusion.

## Dataset

- Dataset version: `clips-v0`
- Planned clips: 5–10 representative short clips
- Rights classification: cleared internal only unless otherwise documented
- Conditions: solo, duet, group, contact, floor work, variable lighting

## Method

- Detector: TBD
- Pose model: MMPose/RTMPose candidate
- Tracking: not primary in this experiment
- Output: keypoints JSON plus overlay video
- Hardware: temporary GPU worker
- Code commit: TBD

## Metrics

| Metric | Value | Notes |
|---|---:|---|
| Person detection rate | | |
| Mean pose confidence | | |
| Missed-person intervals | | |
| Major keypoint failures | | |
| Runtime per video-minute | | |
| Cost per video-minute | | |

## Qualitative findings

- Best example:
- Worst example:
- Failure patterns:

## Decision

- [ ] Continue this model/configuration
- [ ] Change input resolution
- [ ] Compare another pose model
- [ ] Add detector/tracker refinement
