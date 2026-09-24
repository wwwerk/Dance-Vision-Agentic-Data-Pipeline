---
project: dance-vision-agentic-data-pipeline
type: agentic-workflow
---

# Coding-agent workflow

## Goal

Use a coding agent to accelerate implementation while retaining understanding, review control, testing discipline, and Git history.

## Recommended loop

1. Write a short specification in Markdown.
2. Ask the agent for a plan before requesting edits.
3. Approve a narrowly scoped vertical slice.
4. Require tests, dry-run mode, and documentation updates.
5. Review diffs before committing.
6. Run the implementation on fixture data.
7. Commit small, understandable changes.
8. Record a decision or lesson when architecture changes.

## Compatible tools

- Aider in terminal, locally or via SSH to a VPS
- Continue in VS Code/VSCodium or JetBrains
- Roo Code in VS Code-compatible editor
- OpenHands hosted on a Linux VPS or disposable cloud worker

## Required instructions for agents

- Do not access or print secrets.
- Do not run destructive B2 commands.
- Do not edit raw data.
- Work on a branch or clearly scoped change set.
- Add or update tests for behavior changes.
- Use fixtures and dry runs before real cloud actions.
- Explain assumptions and unresolved risks.
