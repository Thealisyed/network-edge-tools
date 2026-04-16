# NID Plugin

Tools for the Network Ingress & DNS (NID) team to automate bug triage and diagnostics.

## Commands

- **`/nid:bug-scrub`** — Analyze untriaged OCPBUGS and post AI triage comments directly on each issue before bug scrub meetings.

## Installation

### From ai-helpers marketplace (once upstreamed)

```bash
/plugin marketplace add openshift/network-edge-tools
/plugin install nid@network-edge-tools
```

### Manual

```bash
git clone git@github.com:openshift/network-edge-tools.git
# Add plugins/nid to your Claude Code commands path
```

## Components

The NID team owns these Jira components in the OCPBUGS project:
- `Networking / router` — HAProxy router, cluster-ingress-operator, Gateway API, route-controller-manager
- `Networking / DNS` — CoreDNS, dns-operator, DNS resolution
