---
project: dance-vision-agentic-data-pipeline
type: portfolio
status: draft
---

# Case study outline

## Working title

Human-governed agentic data pipeline for occlusion-heavy movement video

## Problem

Large archives of human movement are difficult to turn into useful ML datasets because video is long-form, metadata is incomplete, people overlap, limbs occlude one another, identity continuity is hard, and rights/privacy constraints matter.

## Solution

A hybrid architecture:

- Backblaze B2 for durable archive and artifacts
- Small Linux VPS for orchestration and model routing
- Ephemeral GPU workers for pose/tracking inference
- CVAT for human review
- Prefect for deterministic execution
- PydanticAI/LangGraph-style agentic planning with explicit approval gates
- Typed schemas, manifests, and lineage for reproducibility

## What to show

- Architecture diagram
- B2-to-GPU-to-B2 workflow
- Clip manifest and run-manifest examples
- Pose/tracking overlays using approved or redacted media
- Occlusion/identity QA examples
- Annotation schema and review process
- Cost/performance measurements
- Agent plan → validation → approval → Prefect run sequence
- Governance and privacy controls
- Lessons learned and next steps

## Avoid

- Publishing restricted video
- Claiming model performance without held-out measurement
- Treating prelabels as ground truth
- Overstating agent autonomy
