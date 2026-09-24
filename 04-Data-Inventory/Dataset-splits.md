---
project: dance-vision-agentic-data-pipeline
type: dataset-design
---

# Dataset splits

## Rule

Split by source session, event, or performer grouping—not by random frames.

## Why

Adjacent clips, the same choreography, the same venue, or repeated performers can create leakage. Random frame splits make a model appear better by placing nearly identical visual material in train and test.

## Proposed split types

- Train: sessions used for fitting models.
- Validation: distinct sessions used for parameter selection and debugging.
- Test: held-out sessions not inspected during model iteration.
- Occlusion stress test: dense contact, crossings, floor work, lifts, severe overlap.
- Generalization test: different venue, camera, lighting, or performer group.

## Validation checks

- No source session appears in more than one split.
- No duplicated or near-duplicate clip crosses split boundaries.
- Performer overlap is documented and minimized when possible.
- Test labels remain locked during iterative development.
