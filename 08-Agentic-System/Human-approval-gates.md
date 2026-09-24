---
project: dance-vision-agentic-data-pipeline
type: agent-safety
---

# Human approval gates

## Approval required

- GPU job submission with real billing
- Any operation capable of deleting or overwriting data
- Export or sharing outside the private project environment
- Use of source footage with unclear consent/rights status
- Dataset publication or release
- Changes to permanent metadata classification

## Approval record

```text
approval_id
request_type
requested_by
related_plan_or_run_id
scope
estimated_cost
rights_status
human_decision
approver
timestamp
conditions
```

## Approval design

An agent may prepare a plan. A deterministic validator checks it. A human approves the exact batch and budget. Prefect then executes the approved payload without allowing the agent to modify it post-approval.
