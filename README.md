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

StorageClass and PVC design (WaitForFirstConsumer, reclaim policies, encryption), CSI driver selection (EBS vs EFS vs S3), stateful workload patterns (managed RDS as golden path, StatefulSets for distributed systems), backup and snapshots (VolumeSnapshot API, Velero hooks, AWS Backup for EKS), and storage performance (gp3 vs io2, online resize, StorageClass migration).

---

### [10 — Platform API](10-Platform-API/README.md)

Backstage and internal developer portal design (catalog rot prevention, workflow integration, scale thresholds), golden path templates (Helm vs Kustomize post-renderer pattern, drift propagation), service catalog design (automated discovery, ownership model), platform API via CRDs (KRO vs Crossplane XRDs), and platform as a product (self-service model, adoption metrics, internal SLAs).

---

### [11 — Cloud-Specific](11-Cloud-Specific/README.md)

EKS: Auto Mode vs managed node groups, Pod Identity vs IRSA fleet tradeoffs, VPC CNI and Security Groups for Pods. AKS: Azure Workload Identity, Azure CNI Overlay, ACNS Cilium networking. GKE: Autopilot vs Standard, Dataplane V2 eBPF networking, Config Connector. Cloud portability: what is portable across clouds, where portability breaks (identity, StorageClass, load balancer annotations), and how to document deliberate lock-in.
