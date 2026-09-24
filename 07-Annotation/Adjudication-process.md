# Adjudication process

## Use when

- Two annotators disagree materially.
- Identity continuity through overlap cannot be determined.
- An occluded joint is uncertain enough to affect the dataset.
- The source video is too ambiguous for defensible ground truth.

## Possible outcomes

- Confirm original annotation
- Correct annotation
- Mark lower confidence
- Mark identity uncertain
- Mark joint unlabelled
- Exclude interval from gold set

## Record

```text
clip_id
frame/time range
issue type
people/tracks involved
original label
reviewer decision
reasoning
adjudicator
schema version
```

## Principle

A smaller, honest gold set is more valuable than a larger one with unrecorded ambiguity.
