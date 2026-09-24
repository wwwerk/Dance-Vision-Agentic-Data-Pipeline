---
project: dance-vision-agentic-data-pipeline
type: architecture
---

# Annotation architecture

## Workflow

```text
Selected clip
  → model prelabel: person boxes, keypoints, tracks, confidence
  → automated QA flags: occlusion, identity risk, low confidence
  → CVAT import
  → human correction and visibility/uncertainty labels
  → adjudication of difficult intervals
  → validated reviewed export
  → versioned gold dataset
```

## Annotation priorities

1. Correct person existence and persistent identity.
2. Correct major skeletal structure and contact-relevant keypoints.
3. Add keypoint visibility, occlusion, truncation, and uncertainty.
4. Mark probable ID-swap intervals or unresolved identity ambiguity.
5. Validate export before including labels in a training/evaluation set.

## Rule

A prelabel is never ground truth. Prelabels, reviewed labels, and gold labels use separate paths and explicit status fields.
