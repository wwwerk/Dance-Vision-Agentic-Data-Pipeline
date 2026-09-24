# Public repository plan

## Include

- Architecture documentation
- Pydantic schemas
- Synthetic or cleared fixture data
- Pipeline code and dry-run mode
- Tests
- Dockerfiles without secrets
- Example manifests with redacted IDs
- Annotation schema and SOP
- Dataset card template
- Agent tool contracts and approval design
- Reproducibility instructions

## Exclude

- Raw archive video
- Private B2 locations
- Credentials and `.env` files
- Unreviewed labels
- Personally identifying metadata
- Commercial/private annotation exports

## Before publication

- [ ] Run secret scan
- [ ] Review Git history
- [ ] Check licenses
- [ ] Validate all examples use synthetic or cleared data
- [ ] Confirm README commands do not point to private infrastructure
