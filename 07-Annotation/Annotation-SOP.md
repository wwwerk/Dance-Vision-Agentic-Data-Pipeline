---
project: dance-vision-agentic-data-pipeline
type: annotation-sop
status: draft
---

# Annotation standard operating procedure

## Order of work

1. Confirm clip and source/rights status.
2. Correct person existence and persistent track identities.
3. Correct torso and major limb keypoints.
4. Correct remaining keypoints where useful and reliable.
5. Assign visible, occluded, truncated, or unlabelled states per joint.
6. Record contact, occlusion, identity uncertainty, and QA flags.
7. Escalate difficult overlaps to the adjudication queue.
8. Export only after review status is complete.

## Occluded joints

- Label as **occluded** only when a reasonable location can be inferred from visible anatomy and nearby frames.
- Label as **unlabelled** when location is genuinely unknowable.
- Do not convert uncertainty into a guessed coordinate merely to complete a skeleton.

## Identity continuity

- Preserve track identity through a short overlap only when continuity is defensible.
- Mark `identity_uncertain` if a swap cannot be resolved.
- Do not silently merge two people into one track because the model did so.

## Keyframe guidance

Add keyframes at contact transitions, occlusion starts/ends, crossings, sudden direction changes, visible drift, reappearance, and any time interpolation becomes implausible.
