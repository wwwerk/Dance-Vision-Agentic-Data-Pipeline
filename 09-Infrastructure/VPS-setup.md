---
project: dance-vision-agentic-data-pipeline
type: infrastructure
status: draft
---

# VPS setup

## Role

Persistent low-cost Linux environment for orchestration, coding agents, model routing, metadata jobs, optional CVAT, and remote development.

## Initial specification

```text
2–4 vCPU
8 GB RAM preferred
80–160 GB SSD
Ubuntu LTS or Debian
Docker and Docker Compose
SSH key authentication
Firewall enabled
```

## Services to consider

- Aider or OpenHands CLI
- LiteLLM proxy
- Prefect server/worker
- DuckDB/Parquet job environment
- Optional CVAT CPU-only deployment
- Optional lightweight dashboard

## Hardening checklist

- [ ] Non-root user
- [ ] SSH keys only
- [ ] Password auth disabled
- [ ] Root SSH login disabled
- [ ] Firewall configured
- [ ] Automatic security updates policy chosen
- [ ] Backups for persistent volumes/database
- [ ] Secrets stored outside Git
- [ ] Monitoring for disk, memory, and unexpected cost
