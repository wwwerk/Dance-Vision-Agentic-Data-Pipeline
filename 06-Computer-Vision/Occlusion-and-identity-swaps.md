---
project: dance-vision-agentic-data-pipeline
type: cv-design
---

# Occlusion and identity swaps

## Occlusion states

| State | Meaning | Annotation action |
|---|---|---|
| Visible | Joint is observable | Record coordinate as visible |
| Occluded but inferable | Hidden but plausible location can be inferred | Record coordinate as occluded |
| Not annotatable | Location cannot be reliably inferred | Mark unlabelled/absent |
| Truncated | Outside image bounds | Mark truncated; coordinate usually absent |
| Low quality | Blur/darkness/compression prevents reliable judgment | Flag quality issue |
| Identity uncertain | Person continuity cannot be verified | Send to review/adjudication |

## Automated review signals

- Sudden track appearance-embedding changes
- High bounding-box overlap
- Missing detection followed by nearby reappearance
- Abrupt skeleton displacement
- Implausible limb-length changes
- Detector count instability
- Disagreement between models
- Low confidence on torso/hip/shoulder landmarks

## Rule

A system should flag ambiguity for review. It should not hallucinate high-confidence identity continuity through an unresolved overlap.
