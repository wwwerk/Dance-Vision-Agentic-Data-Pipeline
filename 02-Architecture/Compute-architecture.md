---
project: dance-vision-agentic-data-pipeline
type: architecture
---

# Compute architecture

## Local MacBook Pro

Use for Git, editing, terminal control, manifests, light CPU work, review, and local SSD caching. Do not depend on it for sustained modern GPU inference.

## Persistent VPS

Use for orchestration, metadata catalog, LiteLLM gateway, PydanticAI/LangGraph services, scheduled jobs, optional CPU-only CVAT, and Git/CI support.

Suggested initial range:

```text
2–4 vCPU
8 GB RAM preferred
80–160 GB SSD
Ubuntu LTS or Debian
Docker Compose
```

## Ephemeral GPU worker

Use for MMPose, tracking, overlay rendering, and optional model training. Prefer 16 GB VRAM minimum for initial experiments; use 24 GB when batch size, resolution, or fine-tuning requires it.

## Cost controls

- Process selected clips, not the full archive.
- Use local scratch disk on the GPU worker.
- Upload durable results before termination.
- Apply job maximum duration and spend caps.
- Terminate workers immediately after artifact validation.
- Record estimated and actual cost in each run manifest.
