---
project: dance-vision-agentic-data-pipeline
type: risk-register
tags:
  - governance
  - risks
---

# Risks and governance register

## Risk scale

| Level | Meaning |
|---|---|
| Low | Little impact; easy recovery |
| Medium | Delays a milestone or creates rework |
| High | Can cause data loss, privacy harm, unexpected cost, or invalidate results |
| Critical | Legal, ethical, financial, or irreversible harm |

## Active risks

| ID | Risk | Level | Mitigation | Owner | Status |
|---|---|---|---|---|---|
| R-001 | Footage used without ML/data permission | Critical | Maintain source-session rights ledger; use only cleared clips | Me | Open |
| R-002 | Performer privacy or sensitive context exposure | Critical | Restrict access; use de-identified/skeleton output for demos | Me | Open |
| R-003 | GPU worker runs unattended and exceeds budget | High | Per-job cap, auto-termination, approval gate, budget alerts | Me | Open |
| R-004 | B2 source or derived data overwritten/deleted | High | Immutable raw prefix, allowlisted writes, versioned output paths | Me | Open |
| R-005 | Dataset train/test leakage by session or performer | High | Session-level split manifest and validation tests | Me | Open |
| R-006 | Annotation ambiguity leads to inconsistent labels | High | SOP, gold examples, review queue, adjudication | Me | Open |
| R-007 | Model outputs are mistaken for ground truth | High | Separate prelabels from reviewed labels in schema and UI | Me | Open |
| R-008 | Coding agent gains unrestricted credentials | High | Scoped credentials, sandbox, branch protection, no generic shell tool | Me | Open |
| R-009 | Open-source license incompatibility | Medium | Track model/tool licenses before release | Me | Open |
| R-010 | Project scope becomes too broad | High | Enforce time-boxed milestones and vertical-slice-first rule | Me | Open |

## Non-negotiable controls

- [ ] Raw B2 source objects are never overwritten by pipeline code
- [ ] B2 writes use approved project prefixes only
- [ ] GPU jobs have maximum duration and maximum spend
- [ ] GPU jobs upload outputs before termination
- [ ] Agent plans require schema validation
- [ ] Human approval is required before GPU submission
- [ ] Human approval is required before publication or external sharing
- [ ] Every released artifact can be traced to source session and consent status
- [ ] Secrets are absent from Git history, notes, screenshots, and public reports
- [ ] Ground truth and model predictions are stored separately
