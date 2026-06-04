# Module 07 — Observability

OpenTelemetry collector patterns, Prometheus at scale, SLO design, distributed tracing, and log aggregation.

## Files

| File | Description |
|---|---|
| [opentelemetry-collector-patterns.md](opentelemetry-collector-patterns.md) | DaemonSet vs gateway vs sidecar deployment models, ADOT on EKS, memory_limiter as a production requirement |
| [prometheus-at-scale.md](prometheus-at-scale.md) | Remote write vs federation, AMP, cardinality explosion sources and mitigation, cross-cluster cluster_name label, scrape interval tuning |
| [slo-design.md](slo-design.md) | Product-centric vs vanity SLOs, error budgets as policy tools, multi-window burn rate alerting, symptom vs cause-based alerts |
| [distributed-tracing.md](distributed-tracing.md) | Auto vs manual instrumentation, head vs tail sampling tradeoffs, cost of 100% collection, W3C TraceContext propagation |
| [log-aggregation.md](log-aggregation.md) | Structured logging with SPIFFE enrichment, FluentBit vs ADOT, three-tier routing (CloudWatch/OpenSearch/S3), retention tiering |
