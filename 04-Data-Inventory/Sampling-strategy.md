---
project: dance-vision-agentic-data-pipeline
type: strategy
---

# Sampling strategy

## Principle

Do not label or infer indiscriminately across the archive. Select clips that are representative, legally usable, and informative for the model/annotation problem.

## Stages

1. Broad cataloging: sample sparse frames and technical metadata.
2. Candidate selection: choose short clips across movement and difficulty strata.
3. Baseline inference: locate model failures and high uncertainty.
4. Human annotation: prioritize high-value or difficult clips.
5. Iteration: use reviewed data and metrics to select the next batch.

## Priority signals

- High person-box overlap
- Low keypoint confidence
- Track fragmentation
- Suspected identity switches
- Detector-count instability
- Disagreement between models
- Underrepresented movement/camera/lighting conditions
- Strong rights/consent clarity

## Anti-bias checks

- Do not sample only visually easy or technically clean material.
- Do not use only a small recurring performer group for all splits.
- Document what is absent or underrepresented.
