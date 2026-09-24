---
id: EXP-005
project: dance-vision-agentic-data-pipeline
type: experiment
status: future
dataset_version: gold-v0.1
tags:
  - experiment
  - fine-tuning
---

# EXP-005 Fine-tuning

## Question

Does fine-tuning on a reviewed, occlusion-heavy human-movement dataset improve held-out performance over the pretrained baseline?

## Prerequisites

- Gold dataset v0.1
- Validated session-level splits
- Locked test labels
- Reproducible baseline
- Sufficient annotation quality

## Compare

- Generic baseline
- Fine-tuned model
- Visible-joint performance
- Occluded-joint performance
- Tracking/identity performance where applicable
- Runtime and cost

## Decision rule

Only claim improvement if it is measured on held-out data and supported by qualitative inspection.
