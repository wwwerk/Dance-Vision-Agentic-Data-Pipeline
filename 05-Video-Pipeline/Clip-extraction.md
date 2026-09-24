---
project: dance-vision-agentic-data-pipeline
type: runbook
---

# Clip extraction

## Goal

Turn long recordings into selected short intervals with stable IDs and source-time linkage.

## Example command

```bash
ffmpeg -ss 00:12:30 -i input.mov -t 20 -c copy candidate_clip.mp4
```

## Caution

Stream-copy extraction can cut only on keyframes and may not provide frame-exact boundaries. For frame-accurate annotation clips, re-encode and record the exact frame/time mapping.

## Rules

- Preserve original source video ID.
- Preserve start/end time and start/end frame fields.
- Do not reuse clip IDs.
- Store extraction configuration and resulting checksum.
- Keep rights and consent status inherited from the source session.
