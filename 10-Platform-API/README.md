# Module 10 — Platform API

Internal developer portal design, golden path templates, service catalog, platform API abstractions, and the platform-as-a-product operating model.

## Files

| File | Description |
|---|---|
| [backstage-and-developer-portal.md](backstage-and-developer-portal.md) | Backstage as IDP framework vs product, catalog rot prevention via auto-discovery, portal-workflow integration requirement, scale thresholds |
| [golden-path-templates.md](golden-path-templates.md) | Template scope (full platform footprint), Helm vs Kustomize complementary roles, immutable base + post-renderer pattern, drift propagation strategies |
| [service-catalog-design.md](service-catalog-design.md) | Catalog entity content (live state, cost, API schema), automated discovery from Git/K8s/ArgoCD, ownership model (control vs data plane), ghost town prevention |
| [platform-api-design.md](platform-api-design.md) | CRDs as platform API surface, KRO vs Crossplane XRDs comparison, CEL-based resource graphs, admission policy enforcement on platform CRDs |
| [platform-as-a-product.md](platform-as-a-product.md) | Control/data plane ownership split, self-service vs ticket model, adoption metrics, shadow IT detection, internal SLAs, feature request management |
