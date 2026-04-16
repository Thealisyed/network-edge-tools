# NID Sub-Area Taxonomy

## Router / HAProxy
The HAProxy-based router handles all ingress traffic in OpenShift. Issues in this area involve haproxy configuration, reload behavior, route annotations, route certificates, backend health checks, connection handling (408s, 503s), sticky sessions, and TLS termination modes (reencrypt, edge, passthrough). Key terms: router, haproxy, reload, backend, ingress controller, template, 503, 408, connection refused, health check, route annotation, route certificate, route shard, haproxy.config, haproxy template, router pod, router metrics, router canary, sticky session, reencrypt, edge route, passthrough.

## Cluster Ingress Operator (CIO)
The operator that manages IngressController custom resources. Issues here involve the ingresscontroller CR lifecycle, canary checks, default certificates, wildcard policies, route admission, publish strategies, and endpoint publishing. Key terms: ingress operator, ingresscontroller CR, ingresscontroller, canary, default certificate, wildcard policy, route admission, ingress controller operator, CIO, cluster-ingress-operator, admission policy, domain, publish strategy, endpointpublishingstrategy, ingresscontroller status.

## CoreDNS / DNS Operator
DNS resolution in the cluster. Issues involve CoreDNS configuration, dns resolution failures, nxdomain errors, custom forwarding rules, stub domains, and dns operator reconciliation. Key terms: coredns, dns, nxdomain, resolve, corefile, dns operator, cluster dns, forward plugin, stub domain, dns resolution, dns-default, bufsize, protobuf, cluster-dns-operator, node resolver, dns pods, dns daemonset.

## ExternalDNS
Manages DNS records for Route and Ingress resources using cloud provider APIs. Issues involve configuring external DNS providers, zone management, and record lifecycle. Key terms: external-dns, externaldns, dns provider, zone, infoblox, route53, azure dns, google dns, external-dns-operator, dns record, txtrecord, cname, dnsendpoint.

## Gateway API
Kubernetes Gateway API implementation for OpenShift. Issues involve Gateway, HTTPRoute, GRPCRoute, and related resources. Key terms: gateway, gatewayclass, httproute, grpcroute, referencegrant, gateway-api, istio gateway, gateway controller, tcproute, tlsroute, backendref, parentref, gateway listener, gateway status.

## Route Controller Manager
Manages route status updates and ingress-to-route conversion. Key terms: route-controller-manager, route status, admitted, ingress to route, route admission check, route controller, openshift-route-controller-manager.

## Non-functional Categories
If the issue is not about a functional problem in any sub-area above, classify as:
- **Documentation** -- AGENTS.md, README, docs, enhancement proposals, conventions
- **CI / Infrastructure** -- test infrastructure, prow jobs, CI config, Dockerfiles, build scripts
- **Tooling** -- developer tooling, scripts, automation, MCP server, plugins
- **Dependency Management** -- go.mod bumps, image updates, ART reconciliation
