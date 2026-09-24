---
project: dance-vision-agentic-data-pipeline
type: runbook
status: draft
---

# CVAT setup

## Initial deployment choice

Start with either:

- Local Docker-based CVAT on the MacBook for low-volume personal annotation, or
- A CPU-only Linux VPS when local Docker performance or uptime is inadequate.

## Minimum operational needs

- Persistent database and volume backup
- HTTPS/authentication if internet-accessible
- Proxy clips rather than full raw masters
- Clear project/task naming conventions
- Separate prelabel and reviewed export paths

## Project naming

```text
project: dance-occlusion-v0
job: <clip_id>
task: <clip_id>__<annotation-schema-version>
```

## Before creating a task

- [ ] Clip rights status permits annotation
- [ ] Proxy frame rate/resolution documented
- [ ] Source time mapping available
- [ ] Prelabel provenance recorded
- [ ] Annotation schema version selected
