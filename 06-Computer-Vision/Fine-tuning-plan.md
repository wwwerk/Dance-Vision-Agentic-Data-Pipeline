---
project: dance-vision-agentic-data-pipeline
type: cv-plan
status: future
---

# Fine-tuning plan

## Prerequisite

Do not fine-tune until the gold annotations, split policy, export format, and evaluation harness are sufficiently stable.

## First fine-tuning question

Does a model adapted to a small, reviewed, occlusion-heavy dance subset improve held-out pose accuracy and/or identity continuity relative to an off-the-shelf baseline?

## Requirements

- Session-separated train/validation/test split
- Frozen final test set
- Baseline checkpoint and configuration
- Training configuration and random seed
- Versioned labels and dataset manifest
- Checkpoint upload and restart strategy
- Cost and runtime log
- Qualitative error review in addition to metrics

## Output

A reproducible comparison report, not merely a trained checkpoint.
