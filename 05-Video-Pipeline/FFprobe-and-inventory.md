---
project: dance-vision-agentic-data-pipeline
type: runbook
---

# FFprobe and inventory

## Goal

Extract reliable container and stream metadata before downloading or processing large portions of the archive.

## Example inspection command

```bash
ffprobe -v error -show_format -show_streams input.mov
```

## Inventory flow

```text
B2 object listing
  → selected source object
  → ffprobe metadata extraction
  → Pydantic validation
  → Parquet / DuckDB manifest
  → screening and clip selection
```

## Required output fields

- Video duration
- Frame rate
- Resolution
- Codec
- Audio availability
- Source checksum or object ETag where appropriate
- Source B2 key
- Scan date and extraction tool version

## Tests

- Fixture media with known metadata
- Missing stream metadata
- Variable frame rate source
- Corrupt or unavailable file
- Duplicate source ID
