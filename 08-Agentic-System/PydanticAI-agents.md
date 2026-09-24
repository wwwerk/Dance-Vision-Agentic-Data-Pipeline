---
project: dance-vision-agentic-data-pipeline
type: agent-design
status: draft
---

# PydanticAI agents

## First runtime agent

**Archive Curator and Batch Planner**

The agent reads manifests, rights records, model metrics, annotation capacity, and budget constraints. It recommends a bounded next batch for human approval.

## Agent output

```python
class ClipRecommendation(BaseModel):
    clip_id: str
    source_video_id: str
    start_seconds: float
    end_seconds: float
    priority: str
    rationale: list[str]
    expected_occlusion_level: str
    rights_status: str
    estimated_gpu_minutes: float
    expected_annotation_value: float
    risks: list[str]

class BatchPlan(BaseModel):
    batch_id: str
    objective: str
    max_estimated_cost_usd: float
    selected_clips: list[ClipRecommendation]
    exclusions: list[str]
    required_human_approvals: list[str]
    execution_constraints: list[str]
```

## Success criteria

- Output validates against schema.
- Every selected clip exists in the manifest.
- Rights and budget checks run independently in Python.
- Agent rationale is evidence-linked, not invented.
- Plan can be approved, rejected, or edited by a human.
