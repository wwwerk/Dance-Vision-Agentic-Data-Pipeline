# Dance Vision Agentic Data Pipeline — Obsidian Vault

This is a Markdown-first project-management and knowledge-management vault for building a human-governed computer-vision dataset pipeline from an archive of human movement video.

## Use in Obsidian

1. Extract this folder anywhere on a local SSD or a Git-synchronized project directory.
2. In Obsidian, choose **Open folder as vault**.
3. Start at [[00-Project-Home]].
4. Optionally install the Obsidian Tasks and Dataview community plugins for dynamic dashboards. The vault remains usable without plugins.

## Use in Logseq

Open the folder as a local graph. The Markdown files, headings, checkboxes, tags, and links are portable. Logseq-specific block queries are not required for core use.

## Recommended first actions

1. Edit `00-Project-Home.md` with your actual budget and first milestone dates.
2. Read `01-Roadmap.md` and `02-Backlog.md`.
3. Complete tasks T-001 through T-008 before provisioning expensive compute.
4. Use task, experiment, decision, risk, and weekly-review templates as the project grows.
5. Keep secrets, private B2 identifiers, restricted media links, and sensitive performer information out of this vault if it may ever be published or synchronized to a public repository.

## Structure

- `01-Planning/`: charter, criteria, budget, learning plan
- `02-Architecture/`: technical design
- `03-Data-Governance/`: rights, privacy, classification, dataset card
- `04-Data-Inventory/`: B2 layout, metadata, sampling, splits
- `05-Video-Pipeline/`: media-processing runbooks
- `06-Computer-Vision/`: pose/tracking/QA/evaluation plans
- `07-Annotation/`: schema, SOP, CVAT workflow
- `08-Agentic-System/`: coding agents, typed tools, approvals, runtime agents
- `09-Infrastructure/`: Mac, VPS, GPU workers, orchestration, secrets
- `10-Experiments/`: experiment index and planned experiments
- `11-Meetings-and-Reviews/`: weekly reviews and retrospectives
- `12-Portfolio/`: case study and public-release preparation
- `99-Templates/`: reusable note templates
- `Tasks/`: detailed notes for initial backlog tasks

## Important project rule

LLMs can plan and summarize. Deterministic, validated code executes B2 transfers, GPU jobs, data transformations, and storage writes. Human approval is required for spending, destructive actions, and external release.
