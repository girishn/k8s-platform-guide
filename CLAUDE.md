# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

This is a pure-markdown reference guide for engineers making production decisions about Kubernetes and cloud-native platform engineering. The audience is platform engineers and SREs past the tutorial stage — the content targets precise technical decisions: cluster architecture choices, multi-tenancy isolation models, CNI selection, admission controller design, GitOps patterns, autoscaling tradeoffs, and managed Kubernetes (EKS, AKS, GKE) configuration differences.

There is no build system, test suite, or CI pipeline. All content is markdown.

## Module Structure

Eleven numbered modules, each a self-contained directory:

| # | Module | Status |
|---|--------|--------|
| 01 | Cluster Architecture — Control plane HA, node pool design, managed vs self-managed | Pending |
| 02 | Multi-Tenancy — Namespace isolation, resource quotas, LimitRanges, tenant onboarding | Pending |
| 03 | Networking — CNI selection, Ingress vs Gateway API, NetworkPolicy, service mesh | Pending |
| 04 | Security — RBAC design, Pod Security Admission, admission webhooks, Secrets management | Pending |
| 05 | GitOps — ArgoCD vs Flux, app-of-apps pattern, multi-cluster sync | Pending |
| 06 | Autoscaling — HPA vs VPA vs KEDA, cluster autoscaler vs Karpenter | Pending |
| 07 | Observability — OpenTelemetry, Prometheus operator, SLO design, distributed tracing | Pending |
| 08 | Multi-Cluster — Fleet management, workload federation, DR topology | Pending |
| 09 | Storage — PV/PVC design, CSI drivers, stateful workload patterns | Pending |
| 10 | Platform API — Backstage, golden path templates, service catalog, developer portal | Pending |
| 11 | Cloud-Specific — EKS, AKS, GKE managed K8s differences, cloud-native integrations | Pending |

Each module has a `README.md` listing its files with one-line descriptions, and individual `.md` files for each topic.

## Content Conventions

**File naming:** `kebab-case.md`, descriptive and specific (e.g., `karpenter-vs-cluster-autoscaler.md`, not `autoscaling.md`).

**Depth target:** Production-decision level. Each file should answer "what do I choose and why?" with the tradeoffs that matter at scale — not a tutorial walkthrough. Lead with the decision, not the definition. Include concrete configuration examples where they change the decision.

**Structure within files:** Use H2 sections. Lead with what the technology/feature is (concisely), then decision factors, cost/tradeoff tables where useful, and concrete configuration implications. Avoid padding with definitions that the audience already knows.

**Cross-references:** When a file depends on a concept in another module, link explicitly by relative path. The guide is non-linear — readers jump to a specific problem area, so cross-references must be self-sufficient.

**No prescribed reading order:** The `README.md` describes this as a reference, not a course. Don't write content that requires previous modules to be read first.

## Key Architectural Concept (The "Platform as a Product" Model)

The central design principle this guide advocates: the **platform team's customers are internal engineering teams**. The platform is the product — every decision is evaluated through the lens of reducing cognitive load on product engineers while maintaining enterprise-grade security and reliability.

This has a concrete implication: **workloads should be portable across conformant Kubernetes clusters**. Cloud-specific primitives (EKS node groups, AKS node pools, GKE Autopilot) are configuration, not architecture. The design questions start with "what does the workload need?" not "what does the cloud provider offer?" Cloud-specific modules document where this portability breaks down and why.

## Ingest workflow

The RAG system behind this project is a NotebookLM notebook with ID `8614f30f-ef1c-40ae-938a-68bf4ddd56a1`.

1. Query NotebookLM for inputs to create the docs in the project. While querying ensure that the number of calls and number of tokens is optimized to not to exhaust the notebooklm rate limits.
2. Discuss key takeaways with the user before writing anything.

## Question answering

When the user asks a question:

1. Read existing repo first to find relevant pages
2. Read those pages and synthesize an answer
3. Cite specific pages in your response
4. If the answer is not present in the project, say so clearly.
5. If the answer is not in the docs in the project, make a notebook query.
6. If answer is found in the notebook, provide the answer and update the docs in the project.
7. If the answer is not found in the notebook, do a web search and find the most relevant and recent resource for that and provides it.
8. Based on the web search provide the answer and also the source.
9. Check if the new source is worth adding to the notebook.
10. If it is worth adding, let the user know and user will manually add it.
11. If it is not worth adding, discard the new source, update the docs in the project log and remember the decision.
