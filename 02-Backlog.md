---
project: dance-vision-agentic-data-pipeline
type: backlog
tags:
  - project/backlog
---

# Backlog

## Priority guide

| Priority | Meaning |
|---|---|
| P0 | Blocks the current milestone |
| P1 | Important for current phase |
| P2 | Valuable but can wait |
| P3 | Research, idea, or future exploration |

## Now

- [ ] T-001 Create Git repository and baseline project README #task #P0 #milestone/M0
- [ ] T-002 Create B2 storage-layout document and artifact naming policy #task #P0 #milestone/M0
- [ ] T-003 Define video, clip, run, and consent metadata schemas #task #P0 #milestone/M0
- [ ] T-004 Inventory 20 source videos using `ffprobe` metadata extraction #task #P0 #milestone/M0
- [ ] T-005 Select 20 representative candidate clips #task #P0 #milestone/M0
- [ ] T-006 Define a monthly compute/API budget and per-run GPU budget limit #task #P0 #milestone/M0
- [ ] T-007 Test a coding-agent workflow compatible with macOS 11.7 #task #P1 #milestone/M0
- [ ] T-008 Create a source-rights and performer-consent review ledger #task #P0 #governance #milestone/M0

## Next

- [ ] T-020 Implement `ffprobe` to Pydantic to Parquet inventory process #task #P0 #milestone/M1
- [ ] T-021 Add test fixtures using a non-sensitive sample video #task #P0 #testing #milestone/M1
- [ ] T-022 Build B2 download helper with allowlisted source prefixes #task #P0 #B2 #security #milestone/M1
- [ ] T-023 Implement clip extraction with source-time mapping #task #P0 #ffmpeg #milestone/M1
- [ ] T-024 Generate 720p annotation proxy and contact sheet #task #P1 #ffmpeg #milestone/M1
- [ ] T-025 Build a container image for MMPose and tracking #task #P0 #MMPose #GPU #milestone/M1
- [ ] T-026 Run MMPose baseline on five representative clips #task #P0 #MMPose #milestone/M1
- [ ] T-027 Add ByteTrack or BoT-SORT baseline #task #P1 #tracking #milestone/M1
- [ ] T-028 Generate overlay videos and JSON output validation #task #P0 #QA #milestone/M1
- [ ] T-029 Add B2 result uploader with versioned output prefixes #task #P0 #B2 #milestone/M1
- [ ] T-030 Measure GPU-minutes per source-minute and estimate batch costs #task #P0 #cost #milestone/M1

## Annotation pilot

- [ ] T-040 Define joint visibility and occlusion states #task #P0 #annotation #milestone/M2
- [ ] T-041 Define person-track and identity-uncertainty states #task #P0 #annotation #milestone/M2
- [ ] T-042 Draft annotation SOP with positive and negative examples #task #P0 #annotation #milestone/M2
- [ ] T-043 Install and test CVAT locally or on a CPU VPS #task #P1 #CVAT #milestone/M2
- [ ] T-044 Build prelabel import conversion for CVAT #task #P0 #CVAT #milestone/M2
- [ ] T-045 Label 10 minutes of representative material #task #P0 #annotation #milestone/M2
- [ ] T-046 Create difficult-frame adjudication queue #task #P1 #occlusion #milestone/M2
- [ ] T-047 Measure correction time with and without prelabels #task #P1 #metrics #milestone/M2

## Dataset and evaluation

- [ ] T-060 Define session-level train/validation/test split policy #task #P0 #dataset #milestone/M3
- [ ] T-061 Implement COCO keypoint plus temporal-track export #task #P0 #dataset #milestone/M3
- [ ] T-062 Implement dataset validation checks #task #P0 #QA #milestone/M3
- [ ] T-063 Create gold-set review checklist #task #P1 #annotation #milestone/M3
- [ ] T-064 Draft dataset card v0.1 #task #P1 #documentation #milestone/M3
- [ ] T-065 Create baseline evaluation harness #task #P0 #metrics #milestone/M3
- [ ] T-066 Track visible and occluded joint metrics separately #task #P1 #occlusion #milestone/M3
- [ ] T-067 Measure identity switches and track fragmentation #task #P1 #tracking #milestone/M3

## Agentic system

- [ ] T-080 Set up LiteLLM gateway or direct model routing #task #P1 #agentic #milestone/M4
- [ ] T-081 Create typed `BatchPlan` schema with Pydantic #task #P0 #PydanticAI #milestone/M4
- [ ] T-082 Implement read-only manifest query tools #task #P0 #agentic #milestone/M4
- [ ] T-083 Build Archive Curator planning agent #task #P0 #PydanticAI #milestone/M4
- [ ] T-084 Add independent cost and rights validation to plans #task #P0 #safety #milestone/M4
- [ ] T-085 Require human approval before GPU job submission #task #P0 #human-in-the-loop #milestone/M4
- [ ] T-086 Wrap inference job in Prefect flow #task #P0 #Prefect #milestone/M4
- [ ] T-087 Add run audit log: prompt, plan, approval, job, outputs #task #P1 #observability #milestone/M4
- [ ] T-088 Prototype LangGraph approval workflow only after M4 base flow works #task #P2 #LangGraph

## Future research

- [ ] T-100 Test pose models on floor work, inversions, and contact-heavy scenes #task #P2 #research
- [ ] T-101 Compare MMPose, YOLO-Pose, OpenPose, and MediaPipe baseline behavior #task #P2 #research
- [ ] T-102 Test ReID embeddings for post-occlusion identity recovery #task #P2 #tracking
- [ ] T-103 Investigate instance segmentation for overlapping bodies #task #P2 #segmentation
- [ ] T-104 Design a multi-camera synchronization and 3D reconstruction pilot #task #P3 #multicam #3D
- [ ] T-105 Explore movement phrase search and semantic archive navigation #task #P3 #retrieval
- [ ] T-106 Investigate a voice-directed camera-control extension using pose regions #task #P3 #creative-tools
