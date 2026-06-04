# Module 04 — Security

RBAC design, Pod Security Admission, Secrets management, supply chain security, and IAM federation for human access.

## Files

| File | Description |
|---|---|
| [rbac-design.md](rbac-design.md) | Role vs ClusterRole scope, one-SA-per-workload enforcement, ClusterAdmin sprawl patterns, aggregated roles for platform tiers |
| [pod-security-admission.md](pod-security-admission.md) | PSP migration to PSA, three enforcement levels, namespace label strategy, securityContext requirements for Restricted |
| [secrets-management.md](secrets-management.md) | Native Secrets vs ESO vs Sealed Secrets vs Vault vs SPIFFE/SPIRE — decision guide by use case and maturity |
| [supply-chain-security.md](supply-chain-security.md) | Cosign image signing, SBOM generation, admission-enforced verification, IRSA signing permission risk, shift-left CI/CD |
| [iam-federation.md](iam-federation.md) | OIDC federation to K8s RBAC, username prefix spoofing prevention, email vs sub claim, IAM Identity Center fleet-scale access |
| [runtime-security.md](runtime-security.md) | Falco vs eBPF (O(n) vs O(1) rule evaluation), syscall-level detection, alert fatigue prevention, audit log + runtime correlation |
