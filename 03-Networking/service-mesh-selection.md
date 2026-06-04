# Service Mesh Selection

## The core tradeoff: features vs resource overhead

Every service mesh adds latency and resource consumption in exchange for mTLS, observability, and traffic management. The question is how much overhead is acceptable and how much of the feature set you'll actually use.

The three production-grade options occupy distinct positions:

```mermaid
flowchart LR
    LINKERD["Linkerd\nLight, simple\nmTLS + basic observability\nlow ops overhead"]
    ISTIO["Istio\nFull-featured\nmTLS + L7 routing + egress\nhigh ops overhead"]
    CILIUM["Cilium Mesh\nSidecarless\neBPF-native\nrequires Cilium CNI"]

    LINKERD -->|"more features"| ISTIO
    CILIUM -. "different model\n(no sidecars)" .-> ISTIO
```

## Istio

The most feature-complete mesh. Istio injects an Envoy sidecar proxy into every pod. All traffic in and out of the pod is transparently intercepted by the sidecar.

```mermaid
flowchart LR
    subgraph pod_a["Pod A"]
        APP_A["App container"]
        SIDECAR_A["Envoy sidecar"]
        APP_A <--> SIDECAR_A
    end
    subgraph pod_b["Pod B"]
        SIDECAR_B["Envoy sidecar"]
        APP_B["App container"]
        SIDECAR_B <--> APP_B
    end

    SIDECAR_A <-->|"mTLS"| SIDECAR_B
    ISTIOD["istiod\ncontrol plane\ncert distribution\npolicy push"] --> SIDECAR_A & SIDECAR_B
```

**Capabilities:**

- mTLS between all services (SPIFFE/SPIRE certificates)
- L7 traffic management: weighted routing, retries, timeouts, circuit breaking, fault injection
- Ingress and egress gateways
- Rich Envoy metrics: P50/P99 latency, request rate, error rate per route
- JWT/OIDC validation at the proxy layer

**Costs:**

- **Sidecar overhead**: each Envoy proxy consumes ~50–100 MiB memory and ~0.1–0.5 vCPU under load, per pod
- **First-packet latency**: mTLS handshake adds latency on new connection establishment
- **Operational complexity**: istiod, CRDs, webhook injector, gateway pods — significant surface area
- **Version upgrades**: Istio minor version upgrades require careful coordination with sidecar versions

**When to use Istio (sidecar):** You need the full L7 feature set for complex canary rollouts, fault injection, or egress gateway with FQDN filtering — and have Envoy expertise. For new Istio deployments, evaluate Ambient mode first.

## Istio Ambient mode

Ambient mode is Istio's sidecarless architecture, production-ready in 2026. It splits the mesh into two layers:

```mermaid
flowchart TD
    subgraph node["Node (any node)"]
        ZT["ztunnel DaemonSet\nL4 mTLS + SPIFFE identity\nfor all pods on this node"]
    end

    subgraph ns["Namespace (optional L7)"]
        WP["Waypoint proxy\nper-namespace Envoy\nonly needed for L7 features"]
    end

    subgraph pods["Pods (no sidecar injection)"]
        A["Pod A"]
        B["Pod B"]
    end

    A & B <-->|"transparent L4 mTLS\nvia ztunnel"| ZT
    ZT <-->|"only if HTTPRoute / AuthorizationPolicy\nrequires L7 inspection"| WP
```

**ztunnel** (per-node DaemonSet): handles L4 mTLS and SPIFFE identity for all pods on the node. No sidecar injection — pods restart-free during mesh upgrades.

**Waypoint proxy** (per-namespace, opt-in): an Envoy proxy deployed only when a namespace needs L7 features (weighted routing, retries, JWT validation). Namespaces that only need mTLS run ztunnel only.

**Resource impact**: the sidecar model in a 1,000-pod cluster consumes ~70 GB of memory for proxy containers alone. Ambient reduces this to a few hundred MB (one ztunnel per node, Waypoint proxies only where needed).

**Latency**: Ambient P50 inter-service latency is ~2.1 ms vs ~3.8 ms in sidecar mode. P99 is 3–5 ms (sidecar) vs slightly lower in Ambient depending on workload.

**When to use Istio Ambient:** New Istio deployments in 2026. Teams that previously ruled out Istio due to sidecar overhead should re-evaluate Ambient — it eliminates the per-pod memory tax while retaining full Istio L7 capabilities where needed.

## Cilium Mesh (sidecarless mTLS)

Cilium Mesh implements mTLS at the node level via a lightweight Rust proxy (`ztunnel`) in the eBPF datapath — no sidecar injected into pods.

```mermaid
flowchart LR
    subgraph node_a["Node A"]
        APP_A["Pod A\n(no sidecar)"]
        ZT_A["ztunnel\nnode-level proxy"]
        APP_A <--> ZT_A
    end
    subgraph node_b["Node B"]
        ZT_B["ztunnel\nnode-level proxy"]
        APP_B["Pod B\n(no sidecar)"]
        ZT_B <--> APP_B
    end

    ZT_A <-->|"mTLS via SPIRE"| ZT_B
```

**Advantages:**

- No per-pod sidecar: eliminates the memory/CPU tax on application pods
- Identity via SPIRE: cryptographic workload identity without sidecar lifecycle management
- eBPF-native: policy evaluation in kernel, not userspace proxy
- Hubble integration: flow-level observability natively
- Single CNI + mesh stack (no two systems to operate)

**Cilium node-to-node encryption**: Cilium also supports WireGuard or IPsec encryption at the node level — independent of the service mesh layer. This encrypts all pod-to-pod traffic on the wire, including traffic from non-mesh-aware services, without any proxy. Use this as a complement to (or instead of) mTLS for network-layer encryption.

**Performance**: Cilium adds 0.5–1 ms P99 latency (eBPF socket-layer interception, no user-space proxy hop) and ~10–15 MB per node (not per pod).

**Limitations:**

- Requires Cilium as the CNI — not an add-on to an existing CNI
- L7 traffic management is less mature than Istio (Cilium's `Ingress` and `HTTPRoute` via Envoy gateway are improving but not at Istio's depth)
- Troubleshooting kernel-level eBPF programs requires Linux kernel expertise that user-space proxy debugging does not

**When to use Cilium Mesh:** Greenfield clusters already using Cilium CNI that need mTLS and basic L7 policy without the sidecar tax. Right choice when reducing compute overhead is a priority and Istio's advanced L7 features aren't required.

## Linkerd

Linkerd uses lightweight Rust-based micro-proxies (not Envoy) as sidecars, with a significantly smaller per-pod resource footprint than Istio.

**Advantages:**

- 15–25 MB per sidecar vs 50–100 MB for Envoy — meaningful at scale; P99 latency under 1–2 ms
- Simpler operational model than Istio (fewer CRDs, simpler control plane)
- Automatic mTLS with no configuration required after install
- Strong default observability (golden metrics out of the box)

**Limitations:**

- Less L7 traffic management capability than Istio
- No built-in egress gateway
- Smaller ecosystem and fewer integrations

**When to use Linkerd:** Teams that need mTLS and request-level observability but can't justify Istio's operational overhead or sidecar cost. A common choice for smaller engineering orgs moving to zero-trust.

## Decision matrix

| Factor | Istio (sidecar) | Istio Ambient | Cilium Mesh | Linkerd |
|---|---|---|---|---|
| mTLS | Yes | Yes | Yes (SPIRE / WireGuard) | Yes |
| L7 traffic management depth | High | High (via Waypoint) | Medium (improving) | Low–Medium |
| Sidecar required | Yes (Envoy) | No | No | Yes (Rust micro-proxy) |
| Per-pod memory overhead | ~50–100 MB | None (ztunnel per node) | ~10–15 MB per node | 15–25 MB per pod |
| P99 latency per hop | 3–5 ms | ~2 ms | 0.5–1 ms | 1–2 ms |
| Egress gateway | Yes | Yes | Partial | No |
| Observability | Rich (Envoy metrics) | Rich (Envoy + Hubble) | Hubble (flow-level) | Golden metrics |
| Operational complexity | High | Medium | Medium (requires Cilium CNI) | Low |
| Requires specific CNI | No | No | Yes (Cilium) | No |
| Best fit | Multi-cluster, compliance, full L7 | New Istio deployments | Cilium-native stacks | Simplicity-first |

## The forensic visibility gap — across all meshes

Transparent mTLS means packet capture tools see only encrypted bytes. This is true for all three mesh options.

**Required for production:**

- **Istio**: enable Envoy access logging; export to SIEM. Access logs include source identity, method, path, response code — without decrypting payload.
- **Cilium/Hubble**: configure Hubble to export flow events (policy verdicts, connection metadata) to Elasticsearch or S3.
- **Linkerd**: tap and access logs provide request metadata.

Verify your security operations team can reconstruct network-layer decisions post-incident before going live with any mesh. "We have mTLS" is not the same as "we can investigate a breach."

See [networkpolicy-and-service-mesh.md](networkpolicy-and-service-mesh.md) for when a service mesh is necessary.
See [cni-selection.md](cni-selection.md) for Cilium CNI as the prerequisite for Cilium Mesh.
