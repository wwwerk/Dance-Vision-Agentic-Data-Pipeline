---
project: dance-vision-agentic-data-pipeline
type: architecture
status: draft
---

# System architecture

```text
MacBook Pro, macOS 11.7
  ├── Git, SSH, editor, Aider/Continue/Roo Code
  ├── local SSD cache and review workspace
  ├── ffprobe and limited local media preparation
  └── optional local CPU-only CVAT

Linux VPS
  ├── Git checkout and Docker
  ├── LiteLLM gateway or direct provider access
  ├── Prefect orchestration and scheduled CPU work
  ├── optional PydanticAI / LangGraph services
  ├── optional CPU-only CVAT
  └── DuckDB/Parquet catalog and dashboards

Ephemeral GPU worker
  ├── selected B2 clip download
  ├── MMPose + detector + tracker
  ├── QA flags and overlay rendering
  ├── output validation
  ├── upload artifacts to B2
  └── automatic termination

Backblaze B2
  ├── raw masters
  ├── manifests
  ├── working proxies/clips
  ├── inference artifacts
  ├── annotations
  └── released dataset packages
```

## Core rule

LLMs may plan, classify, summarize, and propose. Deterministic, validated Python tools execute data transfer, GPU jobs, transformation, and storage writes.

## Related notes

- [[Data-architecture]]
- [[Agent-architecture]]
- [[Compute-architecture]]
- [[Security-and-access]]
