# Module 06 — Autoscaling

HPA vs VPA vs KEDA, Karpenter vs Cluster Autoscaler, NodePool design, cost-aware scaling patterns, and stateful workload scaling.

## Files

| File | Description |
|---|---|
| [hpa-vpa-keda.md](hpa-vpa-keda.md) | When to use each pod scaler, HPA+VPA conflict on shared metrics, KEDA scale-to-zero with cold-start tradeoffs |
| [karpenter-vs-cluster-autoscaler.md](karpenter-vs-cluster-autoscaler.md) | Groups-less vs ASG-based provisioning, speed and bin-packing comparison, migration approach |
| [karpenter-nodepool-design.md](karpenter-nodepool-design.md) | NodePool and EC2NodeClass design patterns, consolidation policy with PDB dependency, spot interruption handling, node drift remediation |
| [cost-aware-scaling.md](cost-aware-scaling.md) | Spot vs on-demand workload segregation, scale-to-zero economics, Savings Plans interaction, consolidation scheduling |
| [scaling-stateful-workloads.md](scaling-stateful-workloads.md) | StatefulSet scale-down risks, orphaned PVC accumulation, ACK/Crossplane for database scaling, one-way transition rules, Kafka scaling patterns |
