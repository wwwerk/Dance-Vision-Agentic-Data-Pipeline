---
project: dance-vision-agentic-data-pipeline
type: experiment-index
tags:
  - experiments
---

# Experiment index

| ID | Question | Status | Dataset version | Model / pipeline | Result |
|---|---|---|---|---|---|
| EXP-001 | Can baseline MMPose detect bodies in selected contact-improv clips? | Planned | clips-v0 | RTMPose baseline | — |
| EXP-002 | How often does baseline tracking fragment or swap identities? | Planned | clips-v0 | Detector + tracker | — |
| EXP-003 | Which automated signals best find difficult occlusion intervals? | Planned | clips-v0 | QA heuristics | — |
| EXP-004 | Does prelabeling reduce annotation time? | Planned | pilot-v0 | CVAT + prelabels | — |
| EXP-005 | Does fine-tuning improve occluded-joint and identity continuity metrics? | Planned | gold-v0.1 | Fine-tuned pose/tracker | — |

## Experiment principles

1. One clear question per experiment.
2. Use an immutable dataset version and defined split.
3. Log model version, hardware, configuration, time, and cost.
4. Preserve both scalar metrics and qualitative failures.
5. Never tune against the locked final test set.
6. Record negative results; they prevent repeated work.
