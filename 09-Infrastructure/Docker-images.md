# Docker images

## Policy

- Build reproducibly from versioned Dockerfiles.
- Pin base image, Python, CUDA, PyTorch, and key model dependencies where practical.
- Record image digest in run manifests.
- Separate development image from inference worker image.
- Do not place credentials, private keys, or raw source media inside images.

## Initial images

- `inventory-tools`: ffprobe/ffmpeg/Python/Pydantic
- `pose-worker`: CUDA/PyTorch/MMPose/detector/tracker/ffmpeg
- `annotation-tools`: CVAT conversion/validation utilities
- `agent-runtime`: optional PydanticAI/LangGraph/LiteLLM tooling
