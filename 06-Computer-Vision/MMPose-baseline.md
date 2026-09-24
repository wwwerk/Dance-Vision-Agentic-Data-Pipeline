---
project: dance-vision-agentic-data-pipeline
type: cv-plan
status: draft
---

# MMPose baseline

## Initial goal

Run a pretrained multi-person 2D pose baseline on selected clips and evaluate it qualitatively before training anything.

## Baseline outputs

- Person detections/bounding boxes
- Per-person COCO-style keypoints
- Per-keypoint confidence
- Frame timestamps/indexes
- Overlay video
- Model/checkpoint/configuration record

## Evaluation questions

- Does the model detect each person in easy, moderate, and dense scenes?
- Which joints fail most often?
- How does it behave under self-occlusion versus inter-person occlusion?
- Is input resolution adequate?
- Which movement conditions produce implausible skeletons?

## First constraints

- Use selected short clips.
- Save raw model output separately from human-reviewed labels.
- Do not interpret confidence as ground-truth correctness.
- Log exact checkpoint and preprocessing configuration.
