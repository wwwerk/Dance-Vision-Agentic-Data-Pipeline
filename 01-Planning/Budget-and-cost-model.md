---
project: dance-vision-agentic-data-pipeline
type: planning
status: draft
---

# Budget and cost model

## Initial spending rules

- Set a monthly experimental ceiling before provisioning persistent services.
- Set a per-GPU-run ceiling before submitting each batch.
- Use only selected clips until actual cost per source-minute is measured.
- Record estimated and actual costs for every cloud run.
- Destroy GPU workers after output upload and validation.

## Cost ledger

| Date | Run / service | Category | Estimate | Actual | Notes |
|---|---|---|---:|---:|---|
| | | GPU | | | |
| | | VPS | | | |
| | | LLM/API | | | |
| | | Storage/egress | | | |
| | | Annotation | | | |

## Cost metrics

- GPU dollars per source-video minute
- GPU dollars per processed clip
- GPU dollars per useful annotation minute
- LLM/API dollars per accepted code change or planning run
- Annotation minutes per video minute
- Annotation minutes saved by prelabeling

## Approval thresholds

Document thresholds before execution:

- Jobs below: `$___` may run after routine checklist approval.
- Jobs above: `$___` require written review in the task note.
- Any release/publication: explicit rights and privacy review.
