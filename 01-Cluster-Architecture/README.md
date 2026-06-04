# Module 01 — Cluster Architecture

Control plane design, node pool strategy, and the managed vs self-managed tradeoff.

## Files

| File | Description |
|---|---|
| [control-plane-ha.md](control-plane-ha.md) | API server HA on managed K8s, private endpoint design, etcd failure modes, hub-and-spoke vs flat fleet management topology |
| [node-pool-design.md](node-pool-design.md) | MNG vs EKS Auto Mode, workload isolation via taints/tolerations, instance selection for regulated workloads, Pod Identity failure domains |
| [managed-vs-self-managed.md](managed-vs-self-managed.md) | Cost physics comparison, identity scalability at fleet scale, cloud integration depth, org size thresholds |
| [cluster-upgrade-strategy.md](cluster-upgrade-strategy.md) | In-place rolling vs blue-green, OIDC trust boundary risk, configuration drift, add-on upgrade sequencing |
| [cluster-topology.md](cluster-topology.md) | Single vs multi-cluster decision triggers, hub-and-spoke vs flat fleet, Git structure for policy consistency |
