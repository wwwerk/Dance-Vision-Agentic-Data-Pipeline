# Agent evaluation

## Questions

- Are proposed batches valid and rights-compliant?
- Does the agent select diverse, informative clips rather than redundant easy clips?
- Are cost estimates close to actuals?
- Are QA summaries useful to annotators?
- Does the agent correctly identify missing data rather than hallucinating it?
- Does human review time decrease without compromising quality?

## Metrics

- Schema-valid plan rate
- Human acceptance/edit/rejection rate
- Budget-estimation error
- Rights/manifest validation failure rate
- Candidate diversity score
- Annotation-review precision of proposed difficult intervals
- Time saved per accepted plan

## Failure log

Record agent failures with input, output, model/prompt version, validator result, human decision, and remediation.
