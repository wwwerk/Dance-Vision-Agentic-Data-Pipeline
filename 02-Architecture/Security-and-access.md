---
project: dance-vision-agentic-data-pipeline
type: security
status: draft
---

# Security and access

## Principles

- Use least-privilege B2 credentials.
- Never commit secrets, signed URLs, session tokens, or private footage.
- Use separate credentials for local experimentation, VPS automation, and GPU workers when feasible.
- Restrict B2 writes to approved prefixes.
- Use non-root service accounts on VPS and GPU workers.
- Treat self-hosted CI runners and coding agents as privileged tools.

## Required controls

- SSH keys only; disable password and root login on VPS.
- Provider firewall or host firewall enabled.
- `.env` files excluded from Git.
- `.env.example` contains variable names only.
- B2 raw prefix has no delete/write permission for ordinary pipeline workers.
- GPU worker credentials are short-lived or scoped to one project prefix.
- Every agent tool has typed arguments and allowlisted operations.
- Human approval gates protect spending, deletion, publication, and rights-sensitive action.

## Incident checklist

- [ ] Revoke exposed credential
- [ ] Inspect Git history and logs
- [ ] Rotate affected token
- [ ] Identify impacted prefixes/runs
- [ ] Preserve evidence before cleanup
- [ ] Document prevention change in an ADR or risk record
