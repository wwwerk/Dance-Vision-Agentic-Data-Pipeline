---
project: dance-vision-agentic-data-pipeline
type: architecture
status: draft
---

# Agent architecture

## Layer 1: Coding agent

Aider, Continue, Roo Code, or remote OpenHands assists with bounded development tasks: planning, implementation, tests, review, documentation, and refactoring. Git remains the source of truth.

## Layer 2: Runtime planning agent

A PydanticAI agent reads approved manifests and metrics, then proposes a typed `BatchPlan`.

The agent may:

- Select candidate clips from approved metadata
- Explain sampling rationale
- Estimate expected GPU time
- Identify missing metadata or rights blockers
- Propose annotation priority

The agent may not:

- Delete B2 data
- Change consent status
- Submit GPU jobs without approval
- Edit ground-truth labels
- Publish artifacts

## Layer 3: Deterministic execution

Prefect flows execute B2 download, media preparation, inference, upload, validation, and notification based on an approved plan.

## Future: Durable graph

LangGraph may manage stateful review loops after the Prefect/PydanticAI baseline is stable.

## Related notes

- [[PydanticAI-agents]]
- [[Agent-tool-contracts]]
- [[Human-approval-gates]]
- [[Prefect-orchestration]]
