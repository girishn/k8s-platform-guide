# Module 05 — GitOps

ArgoCD vs Flux, app-of-apps and ApplicationSets, multi-cluster sync patterns, environment promotion pipelines, and drift detection.

## Files

| File | Description |
|---|---|
| [argocd-vs-flux.md](argocd-vs-flux.md) | Monolithic vs modular architecture, AppProject vs Kubernetes-native RBAC, fleet management models, resource footprint tradeoffs |
| [app-of-apps-and-applicationsets.md](app-of-apps-and-applicationsets.md) | Hierarchical app-of-apps for controlled onboarding, ApplicationSet generators for fleet-scale automation, blast radius risk |
| [multi-cluster-sync.md](multi-cluster-sync.md) | Hub-and-spoke ArgoCD vs decentralized Flux, deployment paralysis risk, spoke registration, network connectivity requirements |
| [promotion-pipelines.md](promotion-pipelines.md) | PR-based vs automated promotion, hybrid auto-dev/manual-prod pattern, testing gates, GitOps-native rollback via git revert |
| [drift-detection-reconciliation.md](drift-detection-reconciliation.md) | Event-driven vs interval reconciliation, self-healing conflict with incident response, suspend patterns, Day 2 config rot, Helm random value problem |
