---
project: dance-vision-agentic-data-pipeline
type: cv-design
---

# QA heuristics

## Purpose

Reduce manual review by surfacing frames and intervals likely to contain model failures.

## Initial flags

- `low_pose_confidence`
- `missing_person_after_presence`
- `track_fragmentation`
- `suspected_identity_switch`
- `high_inter_person_overlap`
- `implausible_joint_velocity`
- `implausible_limb_length`
- `person_count_change`
- `left_right_swap_suspected`
- `blur_or_low_visibility`

## Review output

Each flag should include:

```text
clip_id
frame_index or time range
track_ids involved
score
triggering measurements
model/pipeline version
review status
reviewer decision
```

## Validation

Measure precision of each flag type: how many flagged intervals actually required human correction? Remove low-value flags that create excessive review noise.
