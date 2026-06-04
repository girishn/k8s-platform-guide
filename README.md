# Kubernetes Platform Engineering Guide

Enterprise-grade reference covering Kubernetes and cloud-native platform engineering decisions. Written for platform engineers and SREs past the tutorial stage — cluster architecture choices, multi-tenancy isolation models, CNI and networking decisions, security and admission control, GitOps patterns, autoscaling tradeoffs, observability design, and managed Kubernetes differences across EKS, AKS, and GKE.

## How to Use This Guide

Each module is self-contained. Navigate directly to the area matching your immediate problem: if you are designing a multi-tenant cluster, start in `02-Multi-Tenancy/`; if you are choosing between ArgoCD and Flux, go to `05-GitOps/`. Cross-references are explicit within files. No prescribed reading order — this is a reference, not a course.

---

## Design Principle

The platform team's customers are internal engineering teams. Every decision in this guide is evaluated through two lenses:

1. **Does it reduce cognitive load on product engineers?** — golden paths, self-service, sensible defaults
2. **Does it hold at enterprise scale?** — multi-tenancy, security posture, operational blast radius

Workloads should be portable across conformant Kubernetes clusters. Cloud-specific primitives are configuration, not architecture. Module 11 documents where that portability breaks down and why.

---

## Table of Contents

### [01 — Cluster Architecture](01-Cluster-Architecture/README.md)
Control plane high availability, node pool design for mixed workloads, managed vs self-managed tradeoffs, and cluster sizing.

---

### [02 — Multi-Tenancy](02-Multi-Tenancy/README.md)
Namespace isolation models, resource quotas and LimitRanges, tenant onboarding gates, and hard vs soft multi-tenancy tradeoffs.

---

### [03 — Networking](03-Networking/README.md)
CNI selection criteria, Ingress vs Gateway API, NetworkPolicy design, service mesh decision, and pod-to-pod encryption.

---

### [04 — Security](04-Security/README.md)
RBAC design and least-privilege principals, Pod Security Admission, admission webhook architecture, Secrets management, and supply chain security.

---

### [05 — GitOps](05-GitOps/README.md)
ArgoCD vs Flux decision criteria, app-of-apps and ApplicationSet patterns, multi-cluster sync, and GitOps promotion pipelines.

---

### [06 — Autoscaling](06-Autoscaling/README.md)
HPA vs VPA vs KEDA selection, cluster autoscaler vs Karpenter, node provisioning strategies, and cost-aware scaling.

---

### [07 — Observability](07-Observability/README.md)
OpenTelemetry instrumentation and collector topology, Prometheus operator and recording rules, SLO/SLI/error budget design, and distributed tracing.

---

### [08 — Multi-Cluster](08-Multi-Cluster/README.md)
Fleet management patterns, workload federation, active-active vs active-passive DR topology, and cross-cluster service discovery.

---

### [09 — Storage](09-Storage/README.md)
PV/PVC design, CSI driver selection, storage class configuration, stateful workload patterns, and backup strategies.

---

### [10 — Platform API](10-Platform-API/README.md)
Internal developer portal design with Backstage, golden path templates, service catalog, and developer experience metrics (DORA/SPACE).

---

### [11 — Cloud-Specific](11-Cloud-Specific/README.md)
Managed Kubernetes differences and cloud-native integrations: EKS (node groups, Karpenter, IAM for Service Accounts), AKS (node pools, AAD integration, Azure CNI), and GKE (Autopilot vs Standard, Workload Identity, GKE Dataplane V2).
