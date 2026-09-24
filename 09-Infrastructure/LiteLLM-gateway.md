---
project: dance-vision-agentic-data-pipeline
type: infrastructure
status: future
---

# LiteLLM gateway

## Goal

Provide a unified OpenAI-compatible endpoint for coding agents and runtime agents while allowing model/provider changes without reconfiguring every client.

## Benefits

- Model aliases such as `coding-fast`, `coding-deep`, and `reviewer`
- Central cost and usage visibility
- API-key isolation from individual tools
- Future routing to local or GPU-hosted open-weight models
- Provider fallback where appropriate

## Initial scope

Start with direct provider credentials if necessary. Add a gateway after the base code workflow is stable, not before.

## Security

- Do not expose unauthenticated gateway publicly.
- Store provider secrets in server environment or secret manager.
- Set budgets and rate limits where available.
- Log metadata necessary for audit without storing sensitive source content unnecessarily.
