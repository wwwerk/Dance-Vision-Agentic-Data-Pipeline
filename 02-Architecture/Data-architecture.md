---
project: dance-vision-agentic-data-pipeline
type: architecture
---

# Data architecture

## Data layers

1. **Raw masters:** immutable source recordings and original capture metadata.
2. **Inventory records:** technical and rights metadata for videos and sessions.
3. **Working derivatives:** proxies, clips, extracted frames, contact sheets, and temporary artifacts.
4. **Inference artifacts:** detections, keypoints, tracks, QA flags, overlays, and run manifests.
5. **Annotation artifacts:** imported prelabels, reviewed labels, gold labels, and adjudication records.
6. **Dataset releases:** documented, versioned packages with explicit rights/release status.

## Core identifiers

- `source_project_id`
- `source_video_id`
- `session_id`
- `multicam_group_id`
- `clip_id`
- `pipeline_run_id`
- `annotation_version`
- `dataset_version`

## Required lineage

Every derivative must identify:

- Its source video and source time range
- The transformation or extraction configuration
- The pipeline run ID
- The code/container/model version
- Its B2 output prefix
- Rights/consent classification

## Storage policy

See [[B2-layout]] and [[Source-video-metadata-schema]].
