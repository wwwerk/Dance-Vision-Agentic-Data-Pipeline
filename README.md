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

## Objective

Designe a low-cost hybrid agentic data platform in which an older macOS workstation acts as a secure control plane and review environment; a Linux VPS provides persistent orchestration, agent sandboxing, and model routing; ephemeral GPU pods perform visual inference; and B2 stores source media and durable artifacts. The system uses structured-output agents, deterministic validation, human approval gates, and reproducible workflow execution.

##  Lowest Cost Configuration

MacBook Pro, macOS 11.7
  ├── Git
  ├── Homebrew Python 3.12 or pyenv Python 3.12
  ├── Aider
  ├── VS Code/VSCodium + Continue or Roo Code
  ├── SSH client
  └── external SSD for a small active working set

Small Linux VPS
  ├── Ubuntu 24.04
  ├── Docker Compose
  ├── LiteLLM Proxy
  ├── Prefect
  ├── Aider and/or OpenHands
  ├── DuckDB + Python environment
  └── optional CPU-only CVAT

Runpod/Vast.ai, only as required
  └── MMPose/tracker batch jobs

Backblaze B2
  └── archive and durable artifacts

## Initial Development Plan

- **Install Aider locally** if you can install a modern Python; otherwise install Aider on the VPS and use it via SSH.
    
- Add **Continue or Roo Code** to your compatible editor for interactive codebase work.
    
- Create a Git repository with test fixtures and a small sample manifest, not real archive credentials.
    
- Set up a **small VPS** as an agent/runtime box.
    
- Run **LiteLLM Proxy** there, initially routing to one paid API model.
    
- Implement one deterministic Prefect flow: `manifest → selected clip → ffprobe → Parquet output`.
    
- Use the coding agent to add tests, documentation, dry runs, and error handling.
    
- Add a temporary GPU-worker flow for `clip → MMPose → tracking → B2 artifacts`.
    
- Only then add PydanticAI planning agents and, later, LangGraph approval state.

## Best practical stack

Your macOS 11.7 MacBook Pro
  ├── Terminal / iTerm2
  ├── Git + SSH
  ├── Aider CLI
  ├── VS Code / VSCodium + Continue or Roo Code
  ├── local project checkout and external SSD cache
  └── optional local ffprobe and low-volume proxy creation

Low-cost Linux VPS
  ├── Docker / Docker Compose
  ├── OpenHands CLI or agent runtime
  ├── LiteLLM proxy
  ├── Prefect server / worker
  ├── Git clone + CI tools
  ├── optional CVAT CPU-only instance
  └── SSH-accessible agent workspace

Ephemeral GPU worker: Runpod / Vast.ai
  ├── MMPose
  ├── detector + tracker
  ├── FFmpeg batch job
  ├── local SSD scratch space
  └── B2 download → inference → B2 result upload → destroy

Backblaze B2
  ├── raw source video
  ├── manifests / Parquet catalogs
  ├── proxies and clips
  ├── inference outputs
  ├── annotation exports
  └── model checkpoints / reports

This avoids trying to make your 2012–2015-era Intel MacBook act like a modern Linux AI workstation. It remains your **control station**: terminal, editor, Git client, review screen, local SSD cache, and occasional CPU worker.

## Coding agents compatible with macOS 11.7

## 1. Aider: best local CLI choice

**Aider** is the clearest first recommendation. It is open source, terminal-native, Git-aware, model-agnostic, and comparatively lightweight. It can work with commercial API models, OpenAI-compatible gateways, and locally hosted model endpoints. Its official repository describes it as AI pair programming in the terminal and documents installation plus model selection through API credentials.[github](https://github.com/aider-ai/aider)

Aider supports Python 3.9–3.12, and an older macOS can use Homebrew Python or `pyenv` rather than the often-outdated system Python. It expects Git and can use either a cloud API key or a local/self-hosted LLM endpoint.deployhq+2

**Why Aider fits your situation**

- No need for a current native macOS app.
    
- Works in Terminal/iTerm2 over SSH.
    
- Keeps all work in ordinary Git repositories.
    
- Can edit code, create files, run tests, and make commits.
    
- Lets you use the model provider of your choice.
    
- You can run it locally against a remote API or run it _on the VPS_ over SSH.
    
- Its Git integration makes agent-generated changes reviewable and reversible.
    

A minimal local setup conceptually looks like:

bash

`# Install a modern isolated Python through Homebrew, pyenv, or uv. python3.12 -m pip install aider-chat# Work in a normal Git checkout. cd ~/Projects/dance-vision-archive git status # Point Aider at your chosen model provider. export ANTHROPIC_API_KEY="..." aider --model sonnet`

If your local Python setup proves difficult, run Aider entirely on a Linux VPS and access it from your MacBook:

bash

`ssh -t agentbox 'cd ~/projects/dance-vision-archive && aider'`

You still get a terminal-based interactive coding agent locally, while the dependencies, model calls, containers, and repository tools run remotely.

## 2. Continue: best lightweight editor agent

**Continue** is an open-source coding assistant with a VS Code extension, JetBrains integration, and a terminal-native CLI. It is model-agnostic and can connect to hosted APIs or OpenAI-compatible model endpoints.continue+1

Use Continue if you want:

- Codebase-aware chat and edit actions in an editor.
    
- Inline completions and quick code explanation.
    
- A local-first or remote-model workflow.
    
- Custom commands for recurring project tasks.
    
- A lower-autonomy assistant than a fully autonomous coding agent.
    

A practical configuration is:

Editor on Mac:
  VS Code or VSCodium
      ↓
Continue extension
      ↓
LiteLLM proxy on VPS
      ↓
Model APIs or remote/self-hosted coding model

Continue can use local Ollama, LM Studio, llama.cpp, hosted OpenAI-compatible endpoints, or direct cloud providers. But because your MacBook is resource-limited, I would treat local model serving as optional and generally route Continue to a VPS-hosted gateway or a commercial API.[sitepoint](https://www.sitepoint.com/continuedev-for-developers-the-complete-local-ai-coding-assistant-setup/)

## 3. Roo Code: best open-source “agent in the editor”

**Roo Code** is an open-source VS Code-based coding agent that can read/write workspace files, run terminal commands, use custom agent modes, and connect to OpenAI-compatible or custom LLM APIs. It is explicitly model-agnostic and supports multi-step workflows.roocodeinc+1

It is a good choice if you want to learn agentic patterns directly in an editor:

- **Architect mode:** creates a plan before touching code.
    
- **Code mode:** implements a bounded approved task.
    
- **Debug mode:** investigates test failures.
    
- **Review mode:** audits code, security, data contracts, and regressions.
    
- **Orchestrator mode:** delegates to narrower roles conceptually.
    

Roo Code can be installed from the VS Code Marketplace or, if you use VSCodium or avoid Marketplace access, from Open VSX or a downloaded VSIX package.[roocodeinc](https://roocodeinc.github.io/Roo-Code/getting-started/installing/)

**Important caution:** Roo Code can run terminal commands and edit files. Give it an isolated project workspace, use Git branches, require approval before commands, and never expose unrestricted B2 credentials in the environment it can access.

## 4. OpenHands: use remotely, not locally

**OpenHands** is an open-source, model-agnostic coding-agent platform that can run locally, in Docker, on remote VMs, or in a cloud backend. It is designed to work with closed APIs or open-weight models such as Qwen, DeepSeek, and Kimi.github+1

However, current OpenHands CLI requirements are Python 3.12+; its more full-featured runtime uses Docker sandboxing. That makes it a much better choice for a modern Linux VPS than an old Big Sur laptop.openhands+1

Use it as your second-stage system:

MacBook terminal
    ↓ SSH
Linux VPS
    ↓
OpenHands CLI / Docker sandbox
    ↓
Git repository + tests + controlled B2 tooling
    ↓
Model API through LiteLLM

This gives you a credible agentic engineering portfolio item: a self-hosted, auditable coding agent running in a sandboxed cloud environment, controlled from your local terminal.

OpenHands’ Docker runtime is specifically intended to sandbox arbitrary agent code execution, rather than giving a model unchecked access to the host.[openhands](https://docs.openhands.dev/openhands/usage/architecture/runtime)

## Model access without model lock-in

## LiteLLM on a VPS

Use **LiteLLM Proxy** as the model-access layer. It gives clients a single OpenAI-compatible endpoint while routing requests to many supported model providers. It can also be self-hosted and configured to track spend or apply budgets.litellm+2

Aider / Continue / Roo Code / OpenHands
                  │
                  ▼
          LiteLLM Proxy on VPS
                  │
     ┌────────────┼─────────────┐
     ▼            ▼             ▼
 Anthropic      OpenAI       OpenRouter /
 Claude APIs    APIs         other compatible provider

Benefits:

- Your tools point to one API base URL.
    
- You can switch models without reconfiguring every client.
    
- You can set model aliases such as `coding-fast`, `coding-deep`, or `reviewer`.
    
- You can maintain a usage/cost log.
    
- You can separate project API keys from individual tool configurations.
    
- You can later route to a self-hosted model on a Runpod/Vast GPU endpoint.
    

LiteLLM exposes OpenAI-compatible endpoints including chat completions, embeddings, transcription, image operations, and reranking, which is useful if the video archive project later combines code agents, metadata embeddings, and local/remote multimodal services.[litellm](https://docs.litellm.ai/docs/providers/litellm_proxy)

## Suggested model routing

|Use case|Recommended model class|Cost posture|
|---|---|---|
|Fast small edits, test fixes, boilerplate|Low-cost coding/API model|Use often|
|Architecture, schema design, tricky debugging|Strong reasoning/coding model|Use selectively|
|Code review, security/data-risk audit|Strong reasoning model|Use before merges|
|Manifest summaries, metadata normalization|Cheap structured-output model|Batch jobs|
|Video semantic analysis|Multimodal API or dedicated CV pipeline|Use only on selected clips|
|MMPose / CV inference|Not an LLM|Rent GPU worker only as needed|

Do not try to run a strong coding LLM locally on the old Intel MacBook unless you simply want an educational experiment. It will generally be slow and constrained by RAM. Your best low-cost approach is remote model access, using your Mac as the interface.

## Low-cost remote options

## Option A: A small Linux VPS: best always-on agent box

A basic VPS is enough for:

- Aider or OpenHands CLI
    
- LiteLLM proxy
    
- Git repository checkout
    
- Python environments
    
- Prefect worker/server
    
- Scheduled metadata jobs
    
- B2 inventory operations
    
- DuckDB/Parquet catalog work
    
- Lightweight web dashboards
    
- CPU-only CVAT for a small project
    

It is **not** where you should run MMPose at scale.

A reasonable minimum:

2–4 vCPU
8 GB RAM preferred
80–160 GB SSD
Ubuntu 24.04 LTS or Debian 12
Docker / Docker Compose
SSH access
Nightly encrypted backup of stateful volumes

A 4 vCPU / 8 GB RAM machine feels markedly better for Docker, Python tooling, LiteLLM, and a small Prefect deployment than a 2 GB instance.

Hetzner historically offered excellent price/performance. Its older published CX32 plan, for example, listed 4 vCPU, 8 GB RAM, and 80 GB disk at €6.80/month, but pricing and availability have changed since then; current regional availability and prices should be verified before purchase.hetzner+2

Other reasonable choices include:

- **Vultr:** potentially attractive if you want B2 egress-partner alignment.
    
- **DigitalOcean:** beginner-friendly UI and predictable documentation; commonly pricier.
    
- **Oracle Cloud:** useful for a free lightweight utility VM if capacity is available, but less friction-free.
    
- **Hetzner:** generally strong budget option if the region, availability, and network path work for you.
    

## Option B: Use a GPU pod as a temporary remote dev environment

Runpod or Vast.ai can host a temporary Linux GPU environment where you:

- Run MMPose and tracking.
    
- Run OpenHands in a disposable Docker sandbox.
    
- Run a stronger open-weight code model locally on the GPU.
    
- Prototype multimodal models.
    
- Perform batch video work from B2.
    
- Push code and results back to Git/B2 before terminating.
    

This is excellent for short experimental bursts but not ideal as your permanent “agent server.” You will need to manage ephemeral storage, checkpoints, credentials, and startup scripts carefully.

Use it for:

B2 selected clips
  → temporary GPU pod
  → pose / tracker / overlay / QA flags
  → B2 derived artifacts

or

Git branch
  → temporary agent sandbox
  → tests + code changes
  → Git commit / pull request
  → destroy pod

## Option C: GitHub Actions plus a self-hosted runner

You can turn your MacBook or VPS into a **GitHub Actions self-hosted runner**. GitHub explicitly supports self-hosted runners on macOS 11.0 and later, so your macOS 11.7 machine is compatible.[github](https://docs.github.com/en/actions/reference/runners/self-hosted-runners)

This is useful for:

- Unit tests triggered by Git pushes.
    
- Formatting and linting.
    
- Manifest schema validation.
    
- Smoke tests on sample clips.
    
- Packaging Docker images.
    
- Running low-priority metadata jobs when your laptop is available.
    

GitHub-hosted runners are also available for Ubuntu, Windows, and macOS, though they are not ideal for large persistent data jobs.[github](https://docs.github.com/actions/using-github-hosted-runners/about-github-hosted-runners)

Avoid exposing a self-hosted runner to untrusted pull requests or public repository contributions. A self-hosted runner has access to the machine and its credentials, so treat it like a privileged worker.

## Local CLI control

You can use your MacBook as a clean control surface even when every serious task runs remotely.

## Basic SSH workflow

# Work directly in a remote repository through an interactive shell.
ssh agentbox

# Launch Aider on the VPS, but use it from your Mac terminal.
ssh -t agentbox 'cd ~/projects/dance-vision-archive && aider'

# Start a long GPU or Prefect job in tmux.
ssh -t agentbox 'tmux new -A -s dance-pipeline'

# Pull a small result locally for review.
rsync -avP agentbox:~/projects/dance-vision-archive/reports/ ./reports/

Use `tmux` so long agent, Docker, or Prefect sessions remain alive if Wi‑Fi drops.

## Private networking

Use a private overlay network rather than opening public SSH ports wherever possible. Tailscale SSH provides authentication and authorization for SSH connections within a tailnet and lets you connect to a named machine with `ssh device` after configuring access controls.[tailscale](https://tailscale.com/docs/features/tailscale-ssh)

However, current mainstream Tailscale macOS client support requires macOS 12 Monterey or later, so do **not** assume the regular Mac App Store or standalone client will work on macOS 11.7. The documented open-source `tailscaled` CLI variant can work differently, but it is an advanced path.tailscale+1

For the MacBook on Big Sur, your practical choices are:

- Standard SSH keys plus a locked-down VPS firewall.
    
- A maintained older compatible VPN/Tailscale client only if you validate its security/support status.
    
- Use the VPS as the server and connect outbound over standard SSH.
    
- Upgrade the MacBook operating system if hardware and workflow constraints permit.
    
- Use a separate modern low-cost control device later, if needed.
    

At minimum, use:

SSH key authentication only
Password login disabled
Root SSH login disabled
UFW or provider firewall restricted to your IP if feasible
Fail2ban or equivalent
Separate non-root service accounts
B2 credentials scoped to project prefixes

## Framework and orchestration split

Use agents for **planning and interpretation**, not for raw execution.

|Concern|Recommended tool|Where it runs|
|---|---|---|
|Agentic code writing|Aider locally or on VPS|Mac terminal or Linux VPS|
|Editor-integrated coding|Continue or Roo Code|Mac editor, remote model endpoint|
|Full autonomous code sandbox|OpenHands|Linux VPS or disposable cloud VM|
|Model gateway and budgets|LiteLLM Proxy|VPS|
|Durable execution|Prefect|VPS, with workers on VPS/GPU pods|
|Agent planning logic|PydanticAI|VPS or local Python environment|
|Long-lived approval graph|LangGraph, later|VPS|
|Video inference|MMPose + tracker|Temporary GPU pod|
|Human annotation|CVAT|Local Mac if feasible, otherwise VPS|
|Source/derived storage|Backblaze B2|Cloud|

Prefect is a good first orchestration layer because it lets you use normal Python functions, while adding run state, retries, logging, and scheduling. It is explicitly designed for data, ML, and agent workflows.prefect+1

Use LangGraph only after your first Prefect flows work. Its value is stateful, durable, human-approved agent workflows—not replacing reliable video processing code. Its human-in-the-loop design allows an agent to pause for approval and resume after an explicit decision.

## Lowest Cost Configuration

MacBook Pro, macOS 11.7
  ├── Git
  ├── Homebrew Python 3.12 or pyenv Python 3.12
  ├── Aider
  ├── VS Code/VSCodium + Continue or Roo Code
  ├── SSH client
  └── external SSD for a small active working set

Small Linux VPS
  ├── Ubuntu 24.04
  ├── Docker Compose
  ├── LiteLLM Proxy
  ├── Prefect
  ├── Aider and/or OpenHands
  ├── DuckDB + Python environment
  └── optional CPU-only CVAT

Runpod/Vast.ai, only as required
  └── MMPose/tracker batch jobs

Backblaze B2
  └── archive and durable artifacts
## Development order

1. **Install Aider locally** if you can install a modern Python; otherwise install Aider on the VPS and use it via SSH.
    
2. Add **Continue or Roo Code** to your compatible editor for interactive codebase work.
    
3. Create a Git repository with test fixtures and a small sample manifest, not real archive credentials.
    
4. Set up a **small VPS** as an agent/runtime box.
    
5. Run **LiteLLM Proxy** there, initially routing to one paid API model.
    
6. Implement one deterministic Prefect flow: `manifest → selected clip → ffprobe → Parquet output`.
    
7. Use the coding agent to add tests, documentation, dry runs, and error handling.
    
8. Add a temporary GPU-worker flow for `clip → MMPose → tracking → B2 artifacts`.
    
9. Only then add PydanticAI planning agents and, later, LangGraph approval state.