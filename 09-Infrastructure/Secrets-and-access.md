# Secrets and access

## Never store in Git or public notes

- B2 application keys
- Cloud provider API tokens
- Model provider API keys
- CVAT admin passwords
- SSH private keys
- Signed URLs
- Unredacted private footage links

## Recommended pattern

```text
.env.example      variable names only
.env              local/private; excluded from Git
VPS environment   managed service secrets
GPU runtime       short-lived/scoped environment injection
```

## Access review checklist

- [ ] Identify every credential and owner
- [ ] Confirm minimum required scope
- [ ] Record expiration/rotation policy
- [ ] Remove credentials from terminated workers
- [ ] Audit code/logs/screenshots before publication
