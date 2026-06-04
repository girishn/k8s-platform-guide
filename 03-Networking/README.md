# Module 03 — Networking

CNI selection, Ingress vs Gateway API, NetworkPolicy limitations, service mesh selection, and egress traffic control.

## Files

| File | Description |
|---|---|
| [cni-selection.md](cni-selection.md) | AWS VPC CNI vs Calico vs Cilium — eBPF vs iptables performance, Security Groups for Pods, when each CNI is the right choice |
| [ingress-vs-gateway-api.md](ingress-vs-gateway-api.md) | Gateway API role-oriented design, incremental migration strategy with AWS LBC, VPC Lattice integration |
| [networkpolicy-and-service-mesh.md](networkpolicy-and-service-mesh.md) | L3/L4 identity gap, when NetworkPolicy alone is sufficient, layering mesh on top of NetworkPolicy, forensic visibility gap |
| [service-mesh-selection.md](service-mesh-selection.md) | Istio vs Cilium Mesh (sidecarless) vs Linkerd — resource overhead, L7 depth, operational complexity, observability requirements |
| [egress-control.md](egress-control.md) | NAT Gateway vs Cilium Egress Gateway vs Istio Egress Gateway, VPC Endpoints for AWS services, identity-aware egress tradeoffs |
