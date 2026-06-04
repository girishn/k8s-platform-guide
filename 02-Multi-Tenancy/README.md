# Module 02 — Multi-Tenancy

Namespace isolation models, resource governance, tenant onboarding automation, admission control, and network policy enforcement.

## Files

| File | Description |
|---|---|
| [namespace-isolation-models.md](namespace-isolation-models.md) | Soft vs hard multi-tenancy, dedicated node pools as middle ground, what namespace isolation doesn't provide |
| [resource-quotas-limitranges.md](resource-quotas-limitranges.md) | Tiered t-shirt size blueprint pattern, LimitRange as ResourceQuota prerequisite, VPA in recommendation mode, object count quotas |
| [tenant-onboarding.md](tenant-onboarding.md) | GitOps apps-of-apps pattern, CRD-based onboarding with KRO/Crossplane, Pod Identity race condition mitigation, self-service vs gated models |
| [admission-control-policy.md](admission-control-policy.md) | OPA/Gatekeeper vs Kyverno, fail-open vs fail-closed tradeoff, webhook HA design, cross-account provisioning via ACK |
| [network-policy-isolation.md](network-policy-isolation.md) | Default-deny baseline, CNI enforcement requirements, iptables vs eBPF at scale, admission-enforced policy presence |
