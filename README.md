# What I build

## Agentic network operations

- [agentic-netops](https://github.com/mairp/agentic-netops): AGNTCY and LangGraph agents turn intent into Kubernetes CRs, controllers reconcile them onto a live SONiC EVPN/VXLAN fabric, and gNMI telemetry closes the loop. Runs in containerlab and kind.
- [agentic-netops-srl](https://github.com/mairp/agentic-netops-srl): the same approach on Nokia SR Linux: a declarative EVPN/VXLAN fabric control plane with a guarded multi-agent intent tier.
- [agentic-ops-bench](https://github.com/mairp/agentic-ops-bench): model-by-harness benchmark on real ops tasks (AIOps, NetDevOps, HPC, inference, RAG, tool loops). Local 30B-class models on one RTX 3090 against hosted frontier models.

## Agent harnesses and infrastructure

- [specstride](https://github.com/mairp/specstride): spec-driven autonomous coding orchestrator. Drives an agent through Spec Kit phases behind an LLM critic gate, diagnoses stuck phases, and tunes its own per-phase settings.
- [mixture-of-loops](https://github.com/mairp/mixture-of-loops): generates provenance-bound, unattended Specstride pipelines from Spec Kit artifacts.
- [agent-observability-stack](https://github.com/mairp/agent-observability-stack): self-hosted observability for LLM agents and the Linux host running them. Prometheus, Grafana, Tempo and OTel, with metrics for OpenClaw, LiteLLM, Claude Code and RAG.
- [qmd-memory-stack](https://github.com/mairp/qmd-memory-stack) and [qmd-gateway](https://github.com/mairp/qmd-gateway): local GPU-accelerated three-tier RAG memory for coding agents, and a shared writable MCP memory gateway for a multi-agent fleet.
- [claude-plugins](https://github.com/mairp/claude-plugins): Claude Code plugin marketplace, including [antares-scan](https://github.com/mairp/antares-scan), first-pass security triage of a code folder with a local Granite-4.0 1B model.

## Agents I use every day

- Linky: drafts a LinkedIn post in my voice every morning and publishes only after I approve it (public demo: [kedin](https://github.com/mairp/kedin)).
- Local AI analyst: a weekly buy-or-wait read on local inference hardware against hosted frontier models, checked against written buy triggers and a ledger.
- Observability digest: a daily Telegram summary of the agent fleet and its host, generated from [agent-observability-stack](https://github.com/mairp/agent-observability-stack).
- Portfolio sync: keeps [mairp.ai](https://mairp.ai) and its digital twin's knowledge base in step with my public repos, daily.
- Relay: a NetOps and infrastructure agent I reach over Telegram; it works cards from the kanban board.
- Eterna: agentic RAG over InfiniBand, RDMA, RoCE and HPC material.
- Havan: hunts flight deals and returns a ranked shortlist (public demo: [havan](https://github.com/mairp/havan)).
- Release watcher: polls upstream release tags every 15 minutes and fast-forwards my local clones, never merging or running repo code.
- Spec-driven batch: runs a Spec Kit command over a range of specs on a chosen harness and model, several features in parallel.
- [video-to-deck](https://github.com/mairp/video-to-deck): turns videos into Marp slide decks using local Whisper, OCR and a fresh agent per video.
- [kanban](https://github.com/mairp/kanban): persistent kanban board with a Claude and Telegram front end.
- Digital twin: answers questions about my work on [mairp.ai](https://mairp.ai).

## Lab tooling

- [kind-cilium-hubble-cluster](https://github.com/mairp/kind-cilium-hubble-cluster): observable Kubernetes cluster with kind, Cilium and Hubble from scratch.
- [gpu_rtx_3090](https://github.com/mairp/gpu_rtx_3090): safe power-cycle scripts for an RTX 3090 Thunderbolt eGPU.
- [certforge](https://github.com/mairp/certforge): small OpenSSL CLI for CSRs and self-signed certificates from a .cnf.

[mairp.ai](https://mairp.ai) · [LinkedIn](https://www.linkedin.com/in/marlon-paz-62b02366/)
