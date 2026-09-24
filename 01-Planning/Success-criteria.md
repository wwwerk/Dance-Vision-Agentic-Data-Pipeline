---
project: dance-vision-agentic-data-pipeline
type: planning
---

# Success criteria

## Technical

- A selected source clip can be traced through inventory, clip extraction, inference, QA, and B2 output upload.
- Every pipeline run has source IDs, configuration, code version, environment/container version, timing, and cost fields.
- The first pose/tracking baseline generates usable prelabels for human review.
- Annotation exports are validated and can be converted to a documented dataset format.
- Train, validation, and test splits avoid obvious session or performer leakage.

## Agentic automation

- A coding-agent workflow contributes to code, tests, docs, and review without replacing human engineering judgment.
- A bounded runtime agent creates a validated batch plan from read-only manifests and inference metrics.
- Human approval is required for GPU submission, irreversible actions, and external release.
- Deterministic workflows—not agents—perform B2 writes, GPU execution, data conversion, and validation.

## Data and governance

- Each selected source session has documented rights and consent status.
- Prelabels, reviewed labels, and released labels are stored separately.
- The project can demonstrate results without exposing restricted media.

## Portfolio

- Repository has clear setup, architecture, tests, and examples.
- Case study describes implementation, tradeoffs, cost, governance, and measured results.
- Demo uses cleared footage, redacted imagery, skeleton renders, or synthetic data.
