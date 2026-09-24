---
project: dance-vision-agentic-data-pipeline
type: infrastructure
---

# Local Mac setup

## Role

The macOS 11.7 MacBook is the control plane, local editor, SSH client, Git workspace, review station, and modest CPU/media-processing machine.

## Recommended local responsibilities

- Git, SSH, terminal, editor
- Aider/Continue/Roo Code if compatible
- Manifest development and tests
- `ffprobe`, modest FFmpeg proxy work, and local fixture creation
- Small local SSD cache
- Optional local CVAT trial
- Reviewing overlays, clips, and annotations

## Avoid relying on it for

- Sustained modern GPU inference
- Large local LLM serving
- Permanent container services if thermal/RAM constrained
- Bulk full-archive transcoding

## Setup checklist

- [ ] Git configured with separate project identity if needed
- [ ] Modern isolated Python installed via supported method
- [ ] SSH key generated and backed up securely
- [ ] `.env` and project data paths excluded from Git
- [ ] External SSD working directory documented
- [ ] Editor has remote SSH capability if desired
