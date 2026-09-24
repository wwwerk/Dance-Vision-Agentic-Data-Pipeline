---
project: dance-vision-agentic-data-pipeline
type: decision-index
tags:
  - project/decisions
---

# Architecture decision log

| ID | Decision | Status | Date | Summary |
|---|---|---|---|---|
| ADR-001 | Use Markdown-first vault for project knowledge | Accepted | 2026-09-23 | Obsidian/Logseq remain portable source of project truth |
| ADR-002 | Keep raw video masters immutable in B2 | Accepted | 2026-09-23 | Derived data goes to versioned prefixes |
| ADR-003 | Separate LLM planning from deterministic execution | Accepted | 2026-09-23 | Agents propose; validated tools and flows execute |
| ADR-004 | Use ephemeral GPU workers for pose inference | Proposed | 2026-09-23 | Avoid idle GPU costs |
| ADR-005 | Begin with PydanticAI and Prefect before LangGraph | Proposed | 2026-09-23 | Start with bounded typed agent plus durable flow |
| ADR-006 | Use session-level data splits | Proposed | 2026-09-23 | Reduce performer/session leakage |
| ADR-007 | CVAT as initial annotation system | Proposed | 2026-09-23 | Open-source and compatible with manual review workflow |

## Open decisions

- [ ] Select primary coding-agent interface: Aider, Continue, Roo Code, OpenHands, or a combination
- [ ] Select VPS provider and region
- [ ] Select temporary GPU provider and baseline GPU class
- [ ] Select initial human detector and MMPose checkpoint
- [ ] Decide whether CVAT runs locally or on a VPS
- [ ] Define consent threshold for internal-only versus publishable dataset material
- [ ] Select experiment tracking tool: MLflow, Weights & Biases, or plain files first
