---
project: dance-vision-agentic-data-pipeline
type: storage-design
---

# B2 layout

```text
b2://dance-archive/
  raw/
    source_project/
      camera_a/
      camera_b/

  manifests/
    video_inventory.parquet
    clips_manifest.parquet
    rights_and_consent.parquet
    checksums.parquet

  proxies/
    source_project/
      video_id/
        proxy_720p.mp4
        contact_sheet.jpg

  clips/
    split_v1/
      clip_id/
        video.mp4
        clip_metadata.json

  inference/
    pose_baseline_v1/
      clip_id/
        detections.jsonl
        keypoints.jsonl
        tracks.jsonl
        review_candidates.jsonl
        overlay_preview.mp4
        run_manifest.json

  annotations/
    schema_v1/
      prelabels/
      reviewed/
      gold/
      adjudicated/

  datasets/
    dance-occlusion-v1/
      train/
      validation/
      test/
      dataset_card.md
      licenses/
      checksums/
```

## Policies

- `raw/` is immutable to normal pipeline workers.
- Each run writes to a versioned output prefix.
- Scratch artifacts should have a retention plan and should not share a prefix with durable outputs.
- Use manifests, not object tags alone, for rich searchable metadata.
