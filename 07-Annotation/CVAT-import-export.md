---
project: dance-vision-agentic-data-pipeline
type: runbook
---

# CVAT import/export

## Import

- Upload selected proxy/video and retain `clip_id`.
- Import model prelabels only into a distinct prelabel layer/status.
- Record model, checkpoint, and pipeline run ID associated with the prelabels.

## Review

- Correct tracks before detailed joints.
- Use keyframes where motion is nonlinear.
- Mark uncertainty rather than overriding ambiguity with false precision.

## Export

- Export reviewed labels to a versioned location.
- Validate against schema before dataset inclusion.
- Preserve a raw export and a normalized project export.
- Store source `clip_id`, annotation version, reviewer, and review status.

## Validation checklist

- [ ] Every frame annotation references a valid clip
- [ ] Track IDs are nonempty and valid
- [ ] Keypoint arrays have expected length
- [ ] Visibility values are allowed
- [ ] No invalid frame indexes
- [ ] Source and annotation versions are recorded
