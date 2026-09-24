---
project: dance-vision-agentic-data-pipeline
type: agent-design
status: future
---

# LangGraph workflows

## When to add it

Only after the deterministic pipeline and PydanticAI batch plan are stable.

## Candidate workflow

```text
Load manifests and recent metrics
  → coverage analysis
  → candidate-selection agent
  → budget/rights/duplication validation
  → human approval interrupt
  → approved Prefect inference flow
  → collect outputs
  → QA summary agent
  → human annotation-queue approval
  → end
```

## Value

- Durable state across long-running jobs
- Explicit human approval pauses
- Auditability of planning/revision loops
- Clear separation between deterministic nodes and LLM reasoning nodes

## Non-goal

LangGraph is not a replacement for Prefect’s durable media-processing execution or schema validation.
