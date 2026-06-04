# Module 11 — Cloud-Specific

Managed Kubernetes differences and cloud-native integrations across EKS, AKS, and GKE, and the portability boundary between them.

## Files

| File | Description |
|---|---|
| [eks-compute-and-addons.md](eks-compute-and-addons.md) | EKS Auto Mode vs managed node groups vs self-managed, EKS managed add-ons, EKS Capabilities (ArgoCD, ACK, KRO) |
| [eks-identity-and-networking.md](eks-identity-and-networking.md) | Pod Identity vs IRSA (fleet sprawl tradeoff), VPC CNI IP model, Security Groups for Pods, IP address management at scale |
| [aks-patterns.md](aks-patterns.md) | Azure Workload Identity (Entra federation), Azure CNI Overlay, ACNS Cilium networking, managed add-ons, external OIDC limitation |
| [gke-patterns.md](gke-patterns.md) | Autopilot vs Standard mode, GKE Workload Identity, Dataplane V2 (eBPF/Cilium), Config Connector (KCC), OIDC Identity Service |
| [cloud-portability.md](cloud-portability.md) | What is portable across clouds, where portability breaks (identity, StorageClass, LB annotations, cloud infra APIs), deliberate lock-in decisions |
