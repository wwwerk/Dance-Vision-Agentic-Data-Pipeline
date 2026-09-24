# Annotator training

## Training goals

- Understand the difference between visible, occluded, truncated, and unlabelled joints.
- Maintain persistent person identities where evidence supports them.
- Escalate ambiguity rather than guessing.
- Use keyframes strategically in fast and contact-heavy motion.
- Distinguish model prelabels from reviewed ground truth.

## Training set

Prepare a small set of examples containing:

- Easy single-person upright movement
- Floor work
- Self-occlusion
- Inter-person overlap
- Full-body disappearance/reappearance
- Fast motion blur
- Suspected identity switch
- Truncation at the frame edge

## Review

Compare an annotator’s labels against an adjudicated reference subset and discuss disagreements before scaling annotation.
