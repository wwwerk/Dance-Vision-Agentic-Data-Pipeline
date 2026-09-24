---
project: dance-vision-agentic-data-pipeline
type: roadmap
status: active
tags:
  - project/dance-vision
  - project/roadmap
---

# Roadmap

## Milestone summary

| ID | Milestone | Target | Status | Definition of done |
|---|---|---:|---|---|
| M0 | Project foundation | 2026-10-06 | Planned | Repository, vault, governance baseline, budget ceiling |
| M1 | Technical vertical slice | 2026-10-20 | Planned | B2 clip to MMPose/tracking output and B2 result upload |
| M2 | Annotation pilot | 2026-11-10 | Planned | Annotation schema, SOP, CVAT pilot, reviewed sample |
| M3 | Gold-set v0.1 | 2026-12-08 | Planned | Small reviewed benchmark split with QA and documentation |
| M4 | Agentic workflow v0.1 | 2026-12-22 | Planned | Planning agent plus human approval and Prefect execution |
| M5 | Portfolio case study | 2027-01-19 | Planned | Public technical write-up, approved demo, reproducible repo |

## Phase 1 — Foundation and inventory

**Time box:** Weeks 1–2  
**Target milestone:** M0

### Objectives

- Establish project repository, note system, and naming conventions.
- Define B2 object layout and immutable raw-source policy.
- Define source-video metadata and rights/consent records.
- Select a small representative sample for initial testing.
- Set up a lightweight agentic coding workflow compatible with macOS 11.7.
- Establish a maximum monthly experimental spend.

### Exit criteria

- [ ] Git repository exists with README, `.gitignore`, license decision, and environment template
- [x] Obsidian/Logseq vault structure is usable
- [ ] B2 source, derived, annotation, and release prefixes are documented
- [ ] Metadata schemas exist for videos, clips, runs, and consent status
- [ ] At least 20 representative clips are identified in a manifest
- [ ] No restricted source is used without documented review
- [ ] Aider, Continue, Roo Code, or remote OpenHands workflow is tested on the repository
- [ ] Monthly compute and API spend cap is defined

## Phase 2 — Deterministic video pipeline

**Time box:** Weeks 3–4  
**Target milestone:** M1

### Objectives

- Build the smallest reliable B2-to-results processing loop.
- Generate metadata, selected clips, proxies, pose outputs, tracks, overlays, and run records.
- Establish dry-run and local-fixture modes before cloud execution.
- Measure cost and throughput on a small sample.

### Exit criteria

- [ ] `ffprobe` metadata extraction works on a fixture and selected real clips
- [ ] Clip manifest records source timing and source-to-derivative relationship
- [ ] One MMPose baseline runs on a temporary GPU worker
- [ ] One tracking baseline produces persistent IDs
- [ ] Outputs include JSON, overlay MP4, metrics, logs, and a run manifest
- [ ] Results upload to a versioned B2 prefix
- [ ] Every run has a cost estimate and actual-cost field
- [ ] Pipeline has a dry-run mode and tested failure handling

## Phase 3 — Annotation pilot

**Time box:** Weeks 5–7  
**Target milestone:** M2

### Objectives

- Define an annotation ontology for pose, tracks, visibility, occlusion, and uncertainty.
- Test CVAT or an equivalent annotation platform.
- Determine what prelabels can be imported and corrected efficiently.
- Validate that annotation instructions produce consistent judgments.

### Exit criteria

- [ ] Annotation schema v1 is frozen for the pilot
- [ ] Visibility definitions distinguish visible, occluded, truncated, and unlabelled joints
- [ ] Identity uncertainty and probable identity-swap states are captured
- [ ] CVAT task import/export works on prelabelled clips
- [ ] At least 10–30 minutes of pilot material is reviewed
- [ ] Annotation SOP is revised based on real ambiguity
- [ ] A small inter-annotator agreement sample is completed if a second reviewer is available

## Phase 4 — Gold dataset v0.1

**Time box:** Weeks 8–10  
**Target milestone:** M3

### Objectives

- Build a small, difficult, consent-cleared benchmark set.
- Separate train, validation, and test sessions without leakage.
- Add data validation and quality checks.
- Document provenance, limitations, and intended use.

### Exit criteria

- [ ] Dataset split is session-based rather than random-frame-based
- [ ] Test material is held out and not used for iterative model tuning
- [ ] Gold annotations are reviewed and versioned
- [ ] COCO-compatible keypoint export plus temporal track metadata exists
- [ ] Dataset validation catches missing IDs, invalid time ranges, malformed joints, and source-link errors
- [ ] Dataset card v0.1 exists
- [ ] Rights, consent, and release restrictions are documented per source session

## Phase 5 — Agentic operations

**Time box:** Weeks 11–12  
**Target milestone:** M4

### Objectives

- Introduce a bounded dataset-curation agent.
- Make human approval explicit before cloud spend or sensitive operations.
- Use Prefect for deterministic execution and Pydantic validation for agent plans.
- Add an audit trail covering prompt, plan, approval, job, and output.

### Exit criteria

- [ ] Archive Curator agent returns a validated `BatchPlan`
- [ ] Agent has read-only access to manifests and metrics
- [ ] Cost estimate is independently recalculated in Python
- [ ] Human approval is required before GPU job submission
- [ ] Prefect flow records job state, retries, logs, and artifacts
- [ ] Agent cannot delete B2 objects or silently change labels
- [ ] Prompt, model, tools, inputs, outputs, and approvals are logged

## Phase 6 — Evaluation and portfolio

**Time box:** Weeks 13–16  
**Target milestone:** M5

### Objectives

- Compare a pretrained baseline against the project’s adapted data workflow.
- Package the technical story for employers without exposing restricted footage.
- Publish code, schemas, selected synthetic samples, and methods where permitted.

### Exit criteria

- [ ] At least one benchmark comparison is complete
- [ ] Failure taxonomy and qualitative examples are documented
- [ ] Cost per processed video-minute is reported
- [ ] Annotation time savings from prelabels are estimated or measured
- [ ] Case study includes architecture, governance, metrics, and lessons learned
- [ ] Public repository contains no secrets or restricted footage
- [ ] Demo uses approved footage, redacted imagery, skeleton renderings, or synthetic examples only
