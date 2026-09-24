---
project: dance-vision-agentic-data-pipeline
type: agent-design
---

# Agent tool contracts

## Principle

Do not give a runtime LLM generic shell, arbitrary SSH, unrestricted B2, or unrestricted deletion tools. Expose small, typed, allowlisted operations.

## Example allowed tools

```text
inspect_manifest()
sample_candidate_clips()
estimate_gpu_cost()
create_run_plan()
get_job_status()
validate_inference_outputs()
summarize_failure_clusters()
prepare_annotation_review_queue()
build_dataset_release_report()
```

## Example typed request

```python
class SubmitInferenceJobRequest(BaseModel):
    batch_id: str
    clip_ids: list[str]
    model_version: str
    gpu_type: str
    max_cost_usd: float
    output_prefix: str
    dry_run: bool = True
```

## Required validation

- Clip IDs exist and are rights-cleared for the intended action.
- Output prefix is approved and versioned.
- Cost is independently calculated outside the LLM.
- GPU type and container image are allowed values.
- No raw-data write/delete operation is possible through ordinary tools.
- Human approval is recorded before a real submission.
