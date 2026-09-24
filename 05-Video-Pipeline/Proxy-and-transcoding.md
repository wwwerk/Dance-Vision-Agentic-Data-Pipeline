---
project: dance-vision-agentic-data-pipeline
type: runbook
---

# Proxy and transcoding

## Goal

Create stable, compact working derivatives for review and annotation while preserving source lineage.

## Example proxy command

```bash
ffmpeg -i input.mov \
  -vf "scale=-2:720,fps=15" \
  -c:v libx264 -crf 20 -preset medium \
  -c:a aac -b:a 128k \
  proxy_720p_15fps.mp4
```

## Guidance

- Use 10–15 fps proxies for triage and many review tasks.
- Retain 24–30 fps or source-frame-rate clips for motion-sensitive gold annotation when necessary.
- Record crop, rotation, scaling, frame-rate, codec, and source-time mapping in metadata.
- Do not assume a review proxy is appropriate as the model-training input.

## Output convention

Each derived file must include or reference its `clip_id`, pipeline version, and transformation manifest.
