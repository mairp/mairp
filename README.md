<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/hero-light.svg">
  <img src="assets/hero-dark.svg" alt="What I build. Agents, networks and the harnesses that run them." width="100%">
</picture>

<p align="center"><code>Open source</code> · <code>Self-hosted</code> · <code>Spec-driven with <a href="https://specstride.ai">Specstride</a></code></p>

<sub><code>// 01 · the loop</code></sub>

## Agentic network operations

```text
 intent ─▶ ┌────────┐  CRs  ┌─────────────┐ reconcile ┌────────┐
           │ agents │ ────▶ │ controllers │ ────────▶ │ fabric │
           └───▲────┘       └─────────────┘           └───┬────┘
               │              gNMI telemetry              │
               └──────────────────────────────────────────┘
```

- [agentic-netops](https://github.com/mairp/agentic-netops): AGNTCY and LangGraph agents turn intent into Kubernetes CRs, controllers reconcile them onto a live SONiC EVPN/VXLAN fabric, and gNMI telemetry closes the loop. Runs in containerlab and kind.
- [agentic-netops-srl](https://github.com/mairp/agentic-netops-srl): the same approach on Nokia SR Linux: a declarative EVPN/VXLAN fabric control plane with a guarded multi-agent intent tier.
- [agentic-ops-bench](https://github.com/mairp/agentic-ops-bench): model-by-harness benchmark on real ops tasks (AIOps, NetDevOps, HPC, inference, RAG, tool loops). Local 30B-class models on one RTX 3090 against hosted frontier models.

<sub><code>// 02 · specstride</code></sub>

## Specstride: loop engineering for coding agents

An agent that grades its own work says "done" when it isn't. [Specstride](https://specstride.ai) takes a Spec Kit feature to done phase by phase, unattended: the engine runs the tests first, then a separate reviewer, [an LLM judge with no tools](https://specstride.ai/#judge), must approve the change, and every approval is a signed record and its own commit. [Every loop has an end](https://specstride.ai/#engineering): capped attempts, named stop reasons, and a diagnosis before a retry.

```text
 ┌────────────────────┐   ┌────────────────────┐   ┌────────────────────┐
 │ Claude Code plugin │   │      dsh host      │   │    plain shell     │
 └─────────┬──────────┘   └─────────┬──────────┘   └─────────┬──────────┘
           └────────────────────────┼────────────────────────┘
                 CLI protocol v1 · argv in, exit code out
                         ┌──────────▼──────────┐
                         │   specstride-core   │  one pinned engine
                         └─────────────────────┘
          implement ─▶ verify ─▶ review ─▶ commit ─▶ next phase
```

| Variant | Runs in | Pick it when |
|---|---|---|
| [specstride-plugin](https://github.com/mairp/specstride-plugin) · [page](https://specstride.ai/products/claude-code-plugin/) | Claude Code | You work in Claude Code. Two skills, installed with two `/plugin` commands. |
| [specstride-dsh](https://github.com/mairp/specstride-dsh) · [page](https://specstride.ai/products/specstride-dsh/) | dsh, the DeepSeek Harness | You work in dsh. Three skills, a shim, a doctor and an eval driver over the pinned core. |
| [specstride-core](https://github.com/mairp/specstride-core) · [page](https://specstride.ai/products/specstride-core/) | Your shell | You run the `specstride` CLI on its own, or build a host for another agent. The engine, its contracts, loop layers, runtime and adapters. |

Install the plugin with `/plugin marketplace add mairp/specstride-plugin`, then `/plugin install specstride@specstride-marketplace`. All three are Apache-2.0 and run the same loop: same gates, same records, same commits.

- [specstride-example](https://github.com/mairp/specstride-example): try it in five minutes on a tiny three-phase Spec Kit feature.
- [specstride.ai](https://github.com/mairp/specstride.ai): the website, with the loop, the judge and the three variants explained.
- [specstride (Python)](https://github.com/mairp/specstride): the earlier Python orchestrator, with an LLM critic gate, stuck-phase diagnosis and self-tuned per-phase settings. It built the core.

<sub><code>// 03 · built with specstride</code></sub>

## Built with Specstride

The evidence is in each repository's history: the engine commits every approved phase itself, as `specstride: phase N approved`.

| Repository | What it is | Evidence |
|---|---|---|
| [agentic-netops](https://github.com/mairp/agentic-netops) | Intent to a live SONiC EVPN/VXLAN fabric, with agents, controllers and gNMI telemetry | [approved-phase commits](https://github.com/mairp/agentic-netops/search?q=%22phase%22+%22approved%22&type=commits), the early ones under the tool's former name |
| [agentic-netops-srl](https://github.com/mairp/agentic-netops-srl) | The same approach on Nokia SR Linux | [approved-phase commits](https://github.com/mairp/agentic-netops-srl/search?q=%22phase%22+%22approved%22&type=commits) |
| [specstride-core](https://github.com/mairp/specstride-core) | The Specstride engine, built by the earlier Python Specstride | [approved-phase commits](https://github.com/mairp/specstride-core/search?q=%22phase%22+%22approved%22&type=commits) |
| [specstride-dsh](https://github.com/mairp/specstride-dsh) | The dsh host and its Kanban tab | [approved-phase commits](https://github.com/mairp/specstride-dsh/search?q=%22phase%22+%22approved%22&type=commits) |
| [mixture-of-loops](https://github.com/mairp/mixture-of-loops) | Generates unattended Specstride pipelines from Spec Kit artifacts | the badge in its [README](https://github.com/mairp/mixture-of-loops#readme) |
| [trustcircle](https://github.com/mairp/trustcircle) | AI governance control plane | [approved-phase commits](https://github.com/mairp/trustcircle/search?q=%22phase%22+%22approved%22&type=commits), from the same critic gate under the loop's earlier name |

<sub><code>// 04 · governance</code></sub>

## AI governance

```text
             ┌───────────┐ package ┌──────────┐ decide ┌──────────────┐
 discover ─▶ │ inventory │ ──────▶ │ approver │ ─────▶ │ audit ledger │
             └─────▲─────┘         └──────────┘        └──────┬───────┘
                   │   controls · evidence · readiness        │
                   └──────────────────────────────────────────┘
```

- [trustcircle](https://github.com/mairp/trustcircle): AI governance control plane. Keeps a continuously reconciled inventory of every AI asset inside a declared boundary, routes decision packages to people who actually hold the authority (separation of duties, no self-approval), turns failing controls into owned cases, and exports signed evidence packages an auditor can verify. Maps controls to ISO/IEC 42001, the EU AI Act and NIST AI RMF, and reports readiness, never certification. One script provisions it on Docker Compose or Kubernetes. Apache-2.0; [UI tour, including the decision screens](https://github.com/mairp/trustcircle#see-it-running).

<sub><code>// 05 · harnesses</code></sub>

## Agent harnesses and infrastructure

- [mixture-of-loops](https://github.com/mairp/mixture-of-loops): generates provenance-bound, unattended Specstride pipelines from Spec Kit artifacts, and ships [specstride-batch](https://github.com/mairp/mixture-of-loops/tree/main/skills/specstride-batch) to run that pipeline over batches of features at once.
- [agent-observability-stack](https://github.com/mairp/agent-observability-stack): self-hosted observability for LLM agents and the Linux host running them. Prometheus, Grafana, Loki, Tempo and OTel, with Arize Phoenix as a second trace backend for LLM calls. Metrics and traces for OpenClaw, LiteLLM, Claude Code and RAG.
- [qmd-memory-stack](https://github.com/mairp/qmd-memory-stack) and [qmd-gateway](https://github.com/mairp/qmd-gateway): local GPU-accelerated three-tier RAG memory for coding agents, and a shared writable MCP memory gateway for a multi-agent fleet.
- [claude-plugins](https://github.com/mairp/claude-plugins): Claude Code plugin marketplace: antares-scan, mixture-of-loops, qmd-recall, gpu-ops, video-to-deck, speckit-batch and specstride. [antares-scan](https://github.com/mairp/antares-scan) does first-pass security triage of a code folder with a local Granite-4.0 1B model.

<sub><code>// 06 · labs</code></sub>

## Network labs

Containerlab labs for Nokia SR OS and SR Linux, built at Nokia and published under [srl-labs](https://github.com/srl-labs).

- [srl-sros-telemetry-lab](https://github.com/srl-labs/srl-sros-telemetry-lab): interactive streaming telemetry lab with SR Linux and SR OS, gNMI into Prometheus and Grafana.
- [sros-anysec-lab](https://github.com/srl-labs/sros-anysec-lab): quantum-safe ANYsec encryption demo on SR OS FP5 vSIMs.
- [sros-anysec-macsec-lab](https://github.com/srl-labs/sros-anysec-macsec-lab): quantum-safe ANYsec and MACsec together in one lab.

<sub><code>// 07 · physical ai</code></sub>

## Physical AI

- [nb-robotic-ai-hk](https://github.com/mairp/nb-robotic-ai-hk): our team's work from the NVIDIA × Nebius "Sim to Table" hackathon (Berlin, October 2026): an SO-101 arm, Isaac Sim demos, Cosmos Reason curation, and GR00T N1.7 training on Nebius. The write-up is the honest account handed to the judges, including the closed-loop result of 0 of 9.

<sub><code>// 08 · the fleet</code></sub>

## Agents and skills I use every day

Skills, curated per session through `skillOverrides` profiles — these are the ones that stay on; the host-ops ones live in [agent-skills](https://github.com/mairp/agent-skills):

- [gpu-ops](https://github.com/mairp/agent-skills/tree/main/gpu-ops): operates and inspects the RTX 3090 eGPU — status, free VRAM, drain, safe power cycles — through proven scripts, never ad-hoc commands.
- [speckit-batch](https://github.com/mairp/claude-plugins/tree/master/plugins/speckit-batch): runs a Spec Kit command over a range of specs on a chosen harness and model, several features in parallel.
- [speckit-* suite](https://github.com/github/spec-kit): the Spec Kit workflow I run daily across Claude Code and dsh — specify, clarify, constitution, plan, tasks, implement, analyze, checklist, converge, taskstoissues — one skill per artifact.
- [specstride-reverse](https://github.com/mairp/agent-skills/tree/main/specstride-reverse): reverse-engineers an existing codebase into a complete as-is Spec Kit feature (constitution, spec, checklist, plan, research, data model, contracts, ticked tasks) with `specstride reverse`, so the pipeline can run on projects with no specs yet.
- [Specstride batch](https://github.com/mairp/mixture-of-loops/tree/main/skills/specstride-batch): runs the full Specstride / Mixture of Loops pipeline over a range of specs — one launch contract per feature, derived and executed unattended on Claude Code or dsh, model and reasoning pinned per run, a shared queue so two harnesses drain batches side by side.
- [mixture-of-loops](https://github.com/mairp/mixture-of-loops): derives the provenance-bound, unattended Specstride pipelines that Specstride batch launches.
- [specstride-curate](https://github.com/mairp/agent-skills/tree/main/specstride-curate): curates and reconciles a Spec Kit spec corpus for a target host, unattended end to end — auto-research agents verify the host facts and distill aesthetic references into cited briefs, a deterministic script backs up and cross-checks, curation agents apply the retargeting rules, analyze reports refresh.
- [jupyter-pull](https://github.com/mairp/agent-skills/tree/main/jupyter-pull): pulls every file off a remote Jupyter server I am logged into, given only the pasted session cookie.
- [spec-reconcile](https://github.com/mairp/agent-skills/tree/main/spec-reconcile): writes a dated spec-vs-deployed sheet, read-only and in a fixed vocabulary — the drift audit between what a spec says and what is running.
- [qmd-recall](https://github.com/mairp/agent-skills/tree/main/qmd-recall): recall from and write to the shared fleet memory, so every agent on the host inherits prior context and durable gotchas.
- [fleet-control](https://github.com/mairp/agent-skills/tree/main/fleet-control): brings the LLM and observability stack up or down and returns a fleet health digest.
- [proxmox-ops](https://github.com/mairp/agent-skills/tree/main/proxmox-ops) and [proxmox-triage](https://github.com/mairp/agent-skills/tree/main/proxmox-triage): guarded lifecycle operations (snapshot before risky changes) and read-only diagnosis of Proxmox VMs and containers.
- [local-model-ops](https://github.com/mairp/agent-skills/tree/main/local-model-ops): which local model to pick on the 3090, when to think longer, and when to escalate to a hosted frontier model.

Agents:

- [Linky](https://github.com/mairp/kedin): drafts a LinkedIn post in my voice every morning and publishes only after I approve it (the link is the public demo).
- Local AI analyst: a weekly buy-or-wait read on local inference hardware against hosted frontier models, checked against written buy triggers and a ledger.
- [Observability digest](https://github.com/mairp/agent-observability-stack): a daily Telegram summary of the agent fleet and its host.
- [Portfolio sync](https://mairp.ai): keeps mairp.ai and its digital twin's knowledge base in step with my public repos, daily.
- Relay: a NetOps and infrastructure agent I reach over Telegram; it works cards from the [kanban](https://github.com/mairp/kanban) board.
- Eterna: agentic RAG over InfiniBand, RDMA, RoCE and HPC material.
- [Havan](https://github.com/mairp/havan): hunts flight deals and returns a ranked shortlist (the link is the public demo).
- Release watcher: polls upstream release tags every 15 minutes and fast-forwards my local clones, never merging or running repo code.
- [video-to-deck](https://github.com/mairp/video-to-deck): turns videos into Marp slide decks using local Whisper, OCR and a fresh agent per video.
- [kanban](https://github.com/mairp/kanban): persistent kanban board with a Claude and Telegram front end.
- [Digital twin](https://mairp.ai): answers questions about my work on mairp.ai.
- [duby](https://github.com/mairp/duby): investment-analysis agent that monitors Telegram trading signals, enriches them with live market data, and serves position-sized analysis through a dashboard and a Telegram bot.

<sub><code>// 09 · sites</code></sub>

## Sites

- [mairp.ai](https://github.com/mairp/mairp.ai): the website of my consulting practice, Network & AI Systems Consulting, live at [mairp.ai](https://mairp.ai). Built on the specstride.ai template.
- [specstride.ai](https://github.com/mairp/specstride.ai): the Specstride website, live at [specstride.ai](https://specstride.ai). Products, hosts and FAQ entries are data, so it doubles as a reusable Astro template (MIT).

<sub><code>// 10 · tooling</code></sub>

## Lab tooling

- [kind-cilium-hubble-cluster](https://github.com/mairp/kind-cilium-hubble-cluster): observable Kubernetes cluster with kind, Cilium and Hubble from scratch.
- [gpu_rtx_3090](https://github.com/mairp/gpu_rtx_3090): safe power-cycle scripts for an RTX 3090 Thunderbolt eGPU.
- [certforge](https://github.com/mairp/certforge): small OpenSSL CLI for CSRs and self-signed certificates from a .cnf.

---

<p align="center"><code><a href="https://mairp.ai">mairp.ai</a></code> · <code><a href="https://specstride.ai">specstride.ai</a></code> · <code><a href="https://www.linkedin.com/in/marlon-paz-62b02366/">LinkedIn</a></code></p>
