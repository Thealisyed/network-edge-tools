# Bugs That Don't Belong to NID

When triaging OCPBUGS issues, scan for keywords that indicate the bug was misrouted to NID (Network Ingress & DNS) when it actually belongs to a different networking sub-team.

## OVN / SDN
Keywords: ovn, ovs, sdn, networkpolicy, egressip, egressfirewall, egressnetworkpolicy, multus, whereabouts, macvlan, ipvlan, ovn-kubernetes, ovnkube, ovs-configuration, br-ex, br-int, geneve, hybrid overlay, ipsec
Suggested component: Networking / ovn-kubernetes

## Load Balancer / Cloud
Keywords: metallb, load balancer type, cloud-provider, CCM, cloud controller, cloud-controller-manager, keepalived, IPVS, speaker, frr, bgp peer
Suggested component: Networking / metal or Cloud Compute / CCM

## Service Mesh
Keywords: istio sidecar, service mesh, envoy proxy, ossm, maistra, kiali, jaeger tracing, service mesh control plane
Suggested component: Networking / service-mesh

## Other Networking
Keywords: kuryr, calico, cilium, nmstate, nodeNetworkConfigurationPolicy, nncp, sriov, sr-iov, dpdk, network-metrics-daemon
Suggested component: Networking / {matched-area} (e.g., Networking / sriov, Networking / kubernetes-nmstate)
