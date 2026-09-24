---
project: dance-vision-agentic-data-pipeline
type: annotation-schema
status: draft
---

# Annotation schema

## Core fields per person per frame

```json
{
  "clip_id": "ci_0142_0008",
  "frame_index": 186,
  "person_track_id": "P03",
  "bbox_xywh": [421, 164, 316, 694],
  "keypoints_coco17": ["x", "y", "visibility", "..."],
  "track_state": "active",
  "visibility_summary": "partially_occluded",
  "occlusion_type": "inter_person",
  "occluded_by_track_ids": ["P07"],
  "identity_confidence": 0.82,
  "annotation_confidence": "medium",
  "review_status": "reviewed",
  "event_flags": ["contact", "possible_identity_switch"]
}
```

## COCO-style visibility baseline

- `0`: not labelled
- `1`: labelled but not visible / occluded
- `2`: labelled and visible

## Additional project fields

- `track_state`: active, absent, ended, identity_uncertain
- `occlusion_type`: none, self, inter_person, object, unknown
- `truncation`: none, partial, full
- `annotation_confidence`: high, medium, low
- `review_status`: prelabel, reviewed, adjudicated, rejected

## Principle

Uncertainty is data. Do not invent joint positions or person identity where an annotator cannot make a defensible judgment.
