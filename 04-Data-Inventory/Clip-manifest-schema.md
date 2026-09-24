---
project: dance-vision-agentic-data-pipeline
type: schema
---

# Clip manifest schema

```text
clip_id
source_video_id
source_b2_key
source_start_seconds
source_end_seconds
source_frame_start
source_frame_end
working_frame_rate
working_width
working_height
proxy_b2_key
working_clip_b2_key
rights_status
consent_status
sampling_stratum
expected_people_range
expected_occlusion_level
selection_rationale
created_by
created_at
pipeline_version
```

## Rules

- `clip_id` is stable and never reused for a different source interval.
- Source time and frame mappings are retained even if a derivative is re-encoded.
- Rights/consent status must be inherited or explicitly overridden with a documented reason.
- A clip cannot enter inference or annotation when its status is `review_required`, `restricted`, or `excluded` unless the workflow supports that exact restriction.
