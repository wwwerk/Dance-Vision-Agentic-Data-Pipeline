---
project: dance-vision-agentic-data-pipeline
type: schema
---

# Source video metadata schema

## Required fields

```text
source_video_id
b2_key
source_project_id
session_id
capture_date
duration_seconds
frame_rate
width
height
codec
audio_present
camera_id
multicam_group_id
rights_status
consent_status
privacy_risk
technical_quality
checksum
```

## Suggested derived fields

```text
mean_person_count
crowd_density_score
motion_energy
blur_score
lighting_variation
pose_detection_rate
tracking_fragmentation_score
occlusion_score
recommended_sampling_priority
```

## Notes

- Store tabular manifests as Parquet where practical.
- Keep raw source facts separate from model-derived estimates.
- Never overwrite source metadata silently; preserve provenance and update history.
